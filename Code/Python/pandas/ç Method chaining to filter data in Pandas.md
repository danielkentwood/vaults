# ç Method chaining to filter data in Pandas
created:: 2022-11-08 08:30
modified:: <%+ tp.file.last_modified_date() %>
mode: #mode/praxis 
kind:: #code
status:: #status/seed
language:: [[ç Python]]
platform::
***

This is an example I stole from twitter -- can't remember the source, but the code is not mine. It demonstrates the following in [[Pandas]]:
* method chaining via .pipe
* adding  lambda functions as custom methods to the dataframe class

```python
import pandas as pd

# download some data
repo = "https://github.com/PacktPublishing"
project = "Pandas-Cookbook/raw/master/data/flights.csv"
df_raw = pd.read_csv(f"{repo}/{project}")
df_rw = df_raw[["MONTH", "ORG_AIR", "DEST_AIR", "CANCELLED"]]

# Patch a custom method in
select = lambda self, col, val: self[self[col] == val]
pd.DataFrame.select = select

# and then pick your favorite
df = (
	# you can use query
	df_raw.query("DEST_AIR == 'LAX'")
	# a custom patched method
	.select("MONTH", 1)
	# the same method via pipe
	.pipe(select, "ORG_AIR", "SFO")
	# or pass a function to loc
	.loc[lambda x: x["CANCELLED"] == 0]
)
```


## Resources

