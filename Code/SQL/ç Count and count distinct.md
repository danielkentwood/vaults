# ç Count and count distinct
created:: 2022-08-31 05:16
modified:: <%+ tp.file.last_modified_date() %>
mode: #mode/praxis 
kind:: #code
status:: #status/seed
language:: [[SQL]]
platform:: [[HackerRank]]
***


## Problem

![Weather%20Observation%20Station%204%20167a8fc685ce4074839a1e747d4a80ee/Untitled.png](Untitled%2014.png)

## Solution

```sql
SELECT (COUNT(*)-COUNT(DISTINCT CITY)) FROM STATION
```