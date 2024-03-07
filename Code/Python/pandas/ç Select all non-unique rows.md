# ç Select all non-unique rows
title:: ç Select all non-unique rows
created:: 2022-09-21 14:45
modified:: <%+ tp.file.last_modified_date() %>
mode: #mode/praxis 
kind:: #code
status:: #status/seed
language:: [[ç Python]]
platform:: [[Pandas]]
***

**Select all non-unique rows**
In Pandas, the df.duplicated() method only returns the duplicate for each pair (or more if there are more than 2 matching rows), leaving just one unique row for each case. But what if I want to see all of the rows that were duplicated? In the example below, I want to find all non-unique rows across the two colums `col_1` and `col_2`:

```python
pd.concat(g for _, g in df.groupby(['col_1','col_2']) if len(g) > 1)
```

Update: it looks like df.duplicated() can handle this case after all:

```python
df.duplicated(subset=['col_1','col_2'], keep=False)
```

In both cases, you'll probably want to sort the resulting table by the subset columns so that you can inspect the duplications.

## Resources


