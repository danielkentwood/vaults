# drop rows from a formatted table
created:: 2022-12-02 15:30
modified:: <%+ tp.file.last_modified_date() %>
mode: #mode/praxis 
kind:: #code
status:: #status/seed
language:: [[SQL]]
platform::
***


How to drop rows from a formatted table (in this case I'm dropping records from NAED and CRMJS tables for a specific campaign_id):

```sql
SET hivevar:CAMPAIGN_ID='17.5'; 
use cpl_hcb_staging; 
ALTER TABLE nba_analytics_exp_design 
DROP IF EXISTS PARTITION(campaign_id = ${hivevar:CAMPAIGN_ID});
ALTER TABLE campaign_run_member_journey_step 
DROP IF EXISTS PARTITION(campaign_id = ${hivevar:CAMPAIGN_ID});
ALTER TABLE cpl_recommender_input
DROP IF EXISTS PARTITION(campaign_id = ${hivevar:CAMPAIGN_ID});
```

More generally, how to drop rows from any table:

```sql
delete from cpl_hcb_staging.nba_analytics_exp_design
where campaign_id = '17.5' and last_updated = '2022-09-12';
```

