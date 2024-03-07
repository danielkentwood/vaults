# ∂ Startup Dashboard
created:: 2022-10-24 08:19
modified:: <%+ tp.file.last_modified_date() %>
mode:: #mode/management
kind:: #dashboard 
status:: #status/raw
parent:: [[∂ Master Dashboard]]
***
## Projects
```dataview
TABLE
FROM #project/startup
WHERE contains(parent, link(this.file.name))
```
