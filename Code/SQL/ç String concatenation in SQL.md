# ç String concatenation in SQL
created:: 2022-08-31 05:16
modified:: <%+ tp.file.last_modified_date() %>
mode: #mode/praxis 
kind:: #code
status:: #status/seed
language:: [[SQL]]
platform:: [[HackerRank]]
***

## Problem

![The%20Pads%20b50ccce3ab024487b20922f2578d99fe/Untitled.png](Untitled%2011.png)

![The%20Pads%20b50ccce3ab024487b20922f2578d99fe/Untitled%201.png](Untitled%201%204.png)

## Solution

```sql

SELECT CONCAT(
	Name, 
	'(', 
	SUBSTRING(Occupation,1,1), 
	')'
) AS Name
FROM OCCUPATIONS
ORDER BY Name;


SELECT CONCAT(
	'There are a total of ', 
	COUNT(Occupation), 
	' ', 
	LOWER(Occupation), 
	's.'
) AS total
FROM OCCUPATIONS
GROUP BY Occupation
ORDER BY total;

```