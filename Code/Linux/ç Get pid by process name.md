# ç Get pid by process name
created:: 2022-11-11 09:31
modified:: <%+ tp.file.last_modified_date() %>
mode: #mode/praxis 
kind:: #code
status:: #status/seed
language:: [[Linux]]
platform::
***

The `pgrep` function allows you to search for a process by name and get its pid. 

```bash
pgrep AppSSOAgent
```

This will return just the pid (and nothing else) for the process named AppSSOAgent.

There are ways to [[Find the process name for a popup window on mac]] if you don't already have it. 