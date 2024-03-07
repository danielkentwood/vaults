# ç Find where a package is being imported from
created:: 2022-05-09 14:43
modified:: <%+ tp.file.last_modified_date() %>
mode: #mode/praxis 
kind:: #code
status:: #status/seed
language:: [[ç Python]]
platform::
***

Commands:

	import pyconnect.utils as pu
	pu.__file__

Result:

	'/users/a522860/.local/lib/python3.7/site-packages/pyconnect/utils.py'