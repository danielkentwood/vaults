# ç Find symmetric pairs (x1 = y2 and x2 = y1) in SQL
created:: 2022-08-31 05:16
modified:: <%+ tp.file.last_modified_date() %>
mode: #mode/praxis 
kind:: #code
status:: #status/seed
language:: [[SQL]]
platform:: [[HackerRank]]
***


## Problem

![Symmetric%20Pairs%20ad4d853e980a41d497247713d37f0fe2/Untitled.png](Untitled%2010.png)

## Solution

```sql
SELECT 
	f1.X, 
	f1.Y 
FROM Functions f1
INNER JOIN Functions f2 
	ON f1.X=f2.Y AND f1.Y=f2.X
GROUP BY 
	f1.X, 
	f1.Y
HAVING COUNT(f1.X)>1 or f1.X<f1.Y
ORDER BY f1.X
```