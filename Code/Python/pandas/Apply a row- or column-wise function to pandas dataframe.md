# Apply a row- or column-wise function to pandas dataframe
created:: 2022-06-30 16:36
modified:: <%+ tp.file.last_modified_date() %>
mode: #mode/praxis 
kind:: #code
status:: #status/seed
language:: [[ç Python]]
platform:: [[Pandas]]
***

### Apply a row- or column-wise function to a Pandas dataframe

create your function
```python
def row_function(row):
	return row['col_x'] * row['col_y'] if row['col_z']==10 else 0
```

apply it to your dataframe
```python
df['new_col'] = df.apply(row_function, axis=1)
```

