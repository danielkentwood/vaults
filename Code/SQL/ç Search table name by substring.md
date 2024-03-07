# ç Search table name by substring
created:: 2022-07-09 23:36
modified:: <%+ tp.file.last_modified_date() %>
mode: #mode/praxis 
kind:: #code
status:: #status/seed
language:: [[SQL]]
platform::
***


INPUT:
```
use dev_segmentation_enc;
show tables like '*prc_scoring';
```

OUTPUT:

|     | table name |
| --- | --- | 
|     | stg_prc_scoring |
|     | test_prc_scoring | 



