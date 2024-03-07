# ç Complex case-when in SQL
created:: 2022-08-31 05:16
modified:: <%+ tp.file.last_modified_date() %>
mode: #mode/praxis 
kind:: #code
status:: #status/seed
language:: [[SQL]]
platform:: [[HackerRank]]
***


## Problem

![Type%20of%20Triangle%200bb4a077282b40158f491bd202967ad6/Untitled.png](Untitled%2013.png)

## Solution

```sql
SELECT  CASE
            WHEN A + B > C AND B + C > A AND A + C > B THEN
                CASE
                    WHEN A = B AND B = C THEN 'Equilateral'
                    WHEN A = B OR A = C or B = C THEN 'Isosceles'
                    ELSE 'Scalene'
                END
            ELSE 'Not A Triangle'
        END
FROM TRIANGLES;
```