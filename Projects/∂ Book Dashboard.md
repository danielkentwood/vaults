# ∂ Book Dashboard

##### Metadata
created:: 2023-02-27 21:46
modified:: <%+ tp.file.last_modified_date() %>
mode:: #mode/management
kind:: #dashboard 
status:: #status/raw
parent:: [[∂ Master Dashboard]]
***
## Projects

```dataview
TABLE
FROM #kind/book 
WHERE contains(parent, link(this.file.name))
```
