# import from local sibling package
created:: 2022-07-22 13:07
modified:: <%+ tp.file.last_modified_date() %>
mode: #mode/praxis 
kind:: #code
status:: #status/seed
language:: [[ç Python]]
platform::
***

Here is a hack if you have a package (with an `__init__.py`) in a sister directory. Suppose your package directory is called "auto_sme", and you have a .py file "icd_hierarchy" that is full of functions that you want to import:

```python
from sys import path
from os.path import dirname as dir
path.append(dir(path[0]))
__package__ = "auto_sme"

from auto_sme.icd_hierarchy import *
```

