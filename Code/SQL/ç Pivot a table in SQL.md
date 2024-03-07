# ç Pivot a table in SQL
created:: 2022-08-31 05:16
modified:: <%+ tp.file.last_modified_date() %>
mode: #mode/praxis 
kind:: #code
status:: #status/seed
language:: [[SQL]]
platform:: [[HackerRank]]
***

## Problem

![Occupations%2040e80218efad4d3987967bd270524408/Untitled.png](Untitled%208.png)

## Solution

```sql
set @r1=0, @r2=0, @r3=0, @r4=0;

select min(Doctor), min(Professor), min(Singer), min(Actor)
from (
  select case when Occupation='Doctor' then (@r1:=@r1+1)
            when Occupation='Professor' then (@r2:=@r2+1)
            when Occupation='Singer' then (@r3:=@r3+1)
            when Occupation='Actor' then (@r4:=@r4+1) end as RowNumber,
    case when Occupation='Doctor' then Name end as Doctor,
    case when Occupation='Professor' then Name end as Professor,
    case when Occupation='Singer' then Name end as Singer,
    case when Occupation='Actor' then Name end as Actor
  from OCCUPATIONS
  order by Name
) temp
group by RowNumber;
```