# get name and size of python vars in jupyter state

##### Metadata
created:: 2023-12-20 17:21
modified:: <%+ tp.file.last_modified_date() %>
mode: #mode/praxis 
kind:: #code
status:: #status/seed
language:: [[ç Python]]
platform:: [[Jupyter]]
***


```python
import sys

local_vars = list(locals().items())
var_lol = []
for var, obj in local_vars:
    var_lol.append([var, sys.getsizeof(obj)/1000000])
pd.DataFrame(var_lol, columns=['var','MB']).sort_values(by='MB', ascending=False).reset_index(drop=True)
```

This will output a dataframe with the name of the variable and its size in MB.