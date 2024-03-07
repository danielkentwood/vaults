## Setup
> [!Note]
> These instructions assume you're operating in bash on a mac

1. Get your proxy details ready
2. Set up your .bashrc file
3. Set up proxies for conda and pip
	1. [[Set up pip to work with Aetna proxy]]
	2. [[Set up conda to work with Aetna proxy]]
4. Install and setup gcloud SDK (instructions: https://cloud.google.com/sdk/docs/install). The last step of the instructions is to run `gcloud init`. This should do two things:
	1. add the gcloud binary path to your .bashrc or .bash_profile (if you have a preference, you can manually move the new code to where you want it)
	2. set up a gcloud 
- set up SSH handshake with enterprise github
- set up anaconda (or mamba)
- set up dedicated conda/mamba env for jupyter lab
- set up conda/mamba env for gcp
	```bash
> conda create --name gcp python=3.11
> conda activate gcp
> conda install -c pandas conda-forge pandas-gbq google-cloud-bigquery ipykernel
```

- use ipykernel to make a kernel for this env

## Usage
1. If you want to pull data from BigQuery, you have to have an active token on your local computer. These only last 24 hours, so you should get a new one at the start of the day. Just run `gcloud auth application-default login` (this will redirect you to sign in to google cloud in your browser) and check the terminal output to confirm that it worked. To see if you have a current token, you can always run  `gcloud auth list`.
2. In JupyterLab, open a new notebook with your `gcp` kernel. 
3. Sample code:
	1. Pull data from BigQuery
   ```python
from google.cloud import bigquery as bq
import pandas as pd

# invoke client
client = bq.Client()

# pull some data from bigquery
sql = """
select member_id 
from `edp-prod-hcbstorage.edp_hcb_core_cnsv.EMIS_CLAIM_LINE` 
where extract(year from srv_start_dt) = extract(year from CURRENT_DATE)
LIMIT 10
"""

df = client.query(sql).to_dataframe()
```
	
	2. Pull data from BigQuery with parameterization
	   ```python
from google.cloud import bigquery as bq
import pandas as pd

# invoke client
client = bq.Client()

# pull some data from bigquery with parameterization
job_config = bq.QueryJobConfig(
    query_parameters=[
        bq.ArrayQueryParameter("adrd_icd_cds", "STRING", [
            'G30.0', 'G30.1', 'G30.8', 'G30.9', 'F02.80', 
            'F02.81', 'F02.90', 'F03.91', 'F04', 'F06.0', 
            'F06.8', 'G31.01', 'G31.09', 'G31.1', 'G31.83', 
            'G31.84', 'G31.85', 'G31.89', 'G31.9', 'G45.4', 
            'G93.7', 'G94', 'I67.5', 'G91.0', 'G91.1', 
            'G91.2', 'F01.50', 'F01.51', 'I67.1', 'I67.2', 
            'I67.4', 'I67.6', 'I67.7', 'I67.81', 'I67.82', 
            'I67.89', 'I67.9'
        ]),
        bq.ScalarQueryParameter("year_filt", "STRING", '2024'),
    ]
)

sql = """
select member_id 
from `edp-prod-hcbstorage.edp_hcb_core_cnsv.EMIS_CLAIM_LINE` 
where 1=1
	AND extract(year from srv_start_dt) = @year_filt
	AND trim(pri_icd9_dx_cd) in unnest(@adrd_icd_cds)
LIMIT 10
"""

df = client.query(sql, job_config=job_config).to_dataframe()
```
	
	3. Write to BigQuery
   ```python
from google.cloud import bigquery as bq
from google.cloud.exceptions import NotFound
import pandas as pd

# invoke client
client = bq.Client()

# Write to BigQuery
def df_to_bq(
	df: pd.DataFrame, 
	table_name: str, 
	labels: dict, 
	client=None, 
	table_schema=None, 
	mode='write'
):
	"""
	Takes a dataframe, a table name, a dictionary of labels, 
	a BQ client object (if already exists), a table schema 
	(optional), and a mode (default is 'write'). 

	Writes (or inserts) the dataframe to a bigquery table at table_name.
	"""

    # set up client if not passed
    if not client:
        client = bq.Client()

    # set up table
    if table_schema:
        table = bq.Table(table_name, schema=table_schema)
    else:
        table = bq.Table(table_name)
    # add labels
    table.labels = labels
    
    try: 
        if mode=='insert':
            client.create_table(table, exists_ok=True)
        elif mode=='write':
            try:
                client.get_table(table_id)
                client.delete_table(table_id)
                client.create_table(table)
            except NotFound:
                client.create_table(table)
        else:
            raise Exception("'mode' parameter must be one of ['write', 'insert']")
    except Exception as e:
        res = e
        print(e)
    else:
        res = df.to_gbq(table_name, if_exists="append", reauth=True)
    return res


labels = {
    'tenant': 'ca-nba-pods',
    'owner': 'woodd1_aetna_com',
    'costcenter': '14621',
    'user': 'daniel_wood',
    'lob': 'hcb',
    'nba_name': 'adrd_core',
    'org': 'anbc-hcb-cebc',
    'business_owner': 'shikha_kanwar',
    'points_of_contact0': 'woodd1_aetna_com',
    'points_of_contact1': 'kanwars_aetna_com',
    'dataset_id': 'ca_nba_pods_hcb_dev',
    'project_id': 'anbc-hcb-dev',
    'campaign_ids0': '102_3',
    'campaign_ids1': '102_4',
    'campaign_ids2': '102_5',
    'dataclassification':'confidential',
}

sql = """
WITH ss AS (
    SELECT
        sm.individual_id
        , sm.strategic_score_value
        , ROW_NUMBER() OVER(
            PARTITION BY
                sm.individual_id
            ORDER BY
                sm.run_dt DESC
        ) AS rnk
    FROM `anbc-hcb-prod.clin_analytics_share_hcb_prod.strategic_stratification_monthly` sm
    INNER JOIN `anbc-hcb-dev.ca_nba_pods_hcb_dev.adrd_add_member_info` mi 
        ON sm.individual_id = CAST(mi.individual_id AS INT64)
    WHERE sm.business_ln_cd = 'ME'
),

ss_last AS (
    SELECT
        individual_id
        , strategic_score_value AS ss_score
    FROM ss
    WHERE rnk = 1
)

SELECT
    individual_id
    , ss_score
    , NTILE(100) OVER(
        ORDER BY ss_score
     ) AS ss_percentile
FROM ss_last
"""
df = client.query(sql).to_dataframe()
table_id = 'anbc-hcb-dev.ca_nba_pods_hcb_dev.adrd_add_cm_ss_score'
print(f'writing to BQ table `{table_id}`')
df_to_bq(df, table_name=table_id, client=client, labels=labels, mode='write')
```
