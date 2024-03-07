mode: #mode/praxis 
kind:: #code
status:: #status/seed
language:: [[Linux]], [[SQL]]
platform:: [[Hadoop]], [[Hive]]

**To run a file:**

	hive2 -f name_of_file.sql

**To run a query:**

	hive2 -e "select * from test_db.sample;"

**To run the query without the massive output as it loads**

	hive2 --silent=true --verbose=false --showWarnings=false -e "query"

**To run a query and output it as a csv file**

```bash

QUERY="SELECT icd_cd, icd_group_nbr, icd_group_dscrptn, n_claims, median_cost FROM dev_nba_enc.auto_sme_all_icd WHERE icd_type_cd = '0'"

OUT_PATH="../data/aetna_icd.csv"

beeline \
--verbose=false \
-u "jdbc:hive2://xhadhbasem1p.aetna.com:2181,"`
`"xhadhivem1p.aetna.com:2181,xhadnmgrm1p.aetna.com:2181,"`
`"xhadnnm1p.aetna.com:2181,xhadnnm2p.aetna.com:2181/;"`
`"serviceDiscoveryMode=zooKeeper;zooKeeperNamespace=hiveserver2-lb" \
--outputformat=csv2 \
--silent=true \
--showHeader=false \
-f "$QUERY" | sed -u '/^$/d' > $OUT_PATH
```

