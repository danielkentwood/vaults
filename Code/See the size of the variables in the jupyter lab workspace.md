# See the size of the variables in the jupyter lab workspace

##### Metadata
created:: 2024-01-25 13:39
modified:: <%+ tp.file.last_modified_date() %>
mode: #mode/praxis 
kind:: #code
status:: #status/seed
language:: [[ç Python]]
platform:: [[Jupyter]]
***



```python
import sys
import pandas as pd


local_vars = list(locals().items())
var_lol = []
for var, obj in local_vars:
    var_lol.append([var, sys.getsizeof(obj)/1000000])
pd.DataFrame(var_lol, columns=['var','MB']).sort_values(by='MB', ascending=False).reset_index(drop=True)
```