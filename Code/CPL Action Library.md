# CPL Action Library

##### Metadata
created:: 2023-04-19 11:57
modified:: <%+ tp.file.last_modified_date() %>
mode: #mode/praxis #aetna 
kind:: #code
status:: #status/seed
language:: [[SQL]]
platform::
***

#### My actions (prod)
- cognitive care planning completed = 346
- minicog assessment scores = 403
- Insights maternity fetal demise check = 245
- Maternity Engine adverse outcomes = 276
- Maternity Engine adverse outcomes check = 277

#### Example query
```sql
select
	individual_id
	, date(action_dts) AS diagnosis_dt
	, get_json_object(action_atts, '$.minicog_score') as minicog_score
from prod_nba_enc.nba_action_library
where action_id = 403
AND get_json_object(action_atts, '$.minicog_score') < 3
```

  