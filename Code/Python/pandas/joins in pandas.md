# Joins in Pandas
mode: #mode/praxis 
kind:: #code
status:: #status/seed
language:: [[ç Python]]
platform:: [[Pandas]]

Suppose you want to join two tables, `df` and `df_member`:

```python
df = df.merge(
	df_member, 
	how = 'left', 
	left_on = 'cl_member_id', 
	right_on = 'member_id'
)
```





