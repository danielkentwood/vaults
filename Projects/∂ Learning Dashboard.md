# ∂ Learning Dashboard

##### Metadata
created:: 2022-10-19 09:13
modified:: <%+ tp.file.last_modified_date() %>
mode:: #mode/management 
kind:: #dashboard 
status:: #status/raw
parent:: [[∂ Master Dashboard]]
***
## Projects
```dataview
TABLE
FROM #project
WHERE contains(parent, link(this.file.name))
```
