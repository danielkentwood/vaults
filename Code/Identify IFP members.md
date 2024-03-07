# Identify IFP members

##### Metadata
created:: 2024-01-10 16:16
modified:: <%+ tp.file.last_modified_date() %>
mode: #mode/praxis #Aetna/data 
kind:: #code
status:: #status/seed
language:: [[SQL]]
platform:: [[Hive]]
***

**Insights**
```sql
from prod_insights_conformed_enc.enriched_membership mem
where UPPER(TRIM(customer_sub_segment_code)) IN ('CBH','CBI')
	AND UPPER(TRIM(source)) IN ('HRP')
	AND business_effective_date <= CURRENT_DATE
	AND business_expiration_date > CURRENT_DATE
	AND TRIM(funding_category) = 'A'
	AND TRIM(business_line_code) = 'Commercial'
```


**EDW**
```sql
from edw_enc.edw_emis_membership mem
where trim(cust_segment_cd) ='IND'
	and trim(cust_subseg_cd) in ('CBH', 'CBI')
```

Note that IFP members can be uniquely identified just from `source='HRP'` and `business_line_code='Commercial'`. 