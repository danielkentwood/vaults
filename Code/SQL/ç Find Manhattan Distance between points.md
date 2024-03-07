# ç Find Manhattan Distance between points
created:: 2022-08-31 05:16
modified:: <%+ tp.file.last_modified_date() %>
mode: #mode/praxis 
kind:: #code
status:: #status/seed
language:: [[SQL]]
platform:: [[HackerRank]]
***

Find the [[Manhattan Distance]] between points.

## Problem

![Manhattan%20Distance%20acec90c48e0f40ac84a7148a1ce76895/Untitled.png](Media/Untitled%205.png)

## Solution

```sql
SELECT ROUND(ABS(MAX(LAT_N)-MIN(LAT_N)) + ABS(MAX(LONG_W)-MIN(LONG_W)), 4)
FROM STATION
```