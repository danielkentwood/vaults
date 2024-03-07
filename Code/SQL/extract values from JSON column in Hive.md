# extract values from JSON column in Hive

##### Metadata
created:: 2023-02-24 16:52
modified:: <%+ tp.file.last_modified_date() %>
mode: #mode/praxis 
kind:: #code
status:: #status/seed
language:: [[Hive]], [[SQL]]
platform::
***
You can use the `get_json_object` function to extract values from a JSON column in a hive/SQL table. It takes two arguments (column name, dictionary key) and returns the dictionary value. The dictionary key is passed as a string with a dollar sign prefix (e.g., `'$.keyname'`). Example usage:

```SQL
SELECT
	get_json_object(custom_atts, '$.lob') AS lob
FROM prod_nba_enc.nba_analytics_exp_design
WHERE campaign_id = '91.12';

```
