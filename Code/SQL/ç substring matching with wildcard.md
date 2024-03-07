# ç substring matching with wildcard
created:: 2022-06-29 11:20
modified:: <%+ tp.file.last_modified_date() %>
mode: #mode/praxis 
kind:: #code
status:: #status/seed
language:: [[SQL]]
platform::
***


You can use the `LIKE` function to filter on substring matches. For example, if I want to return all rows from `fu_db.bar_table` where the column `call_transcript` contains the term `hotdogs`, with any other characters before or after it:

```
SELECT * FROM fu_db.bar_table WHERE call_transcript LIKE %hotdogs%;
```

