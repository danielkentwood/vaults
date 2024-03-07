# ∂ Article Dashboard

##### Metadata
created:: 2023-02-27 21:43
modified:: <%+ tp.file.last_modified_date() %>
mode:: #mode/management
kind:: #dashboard 
status:: #status/raw
parent:: [[∂ Master Dashboard]]
***
## Projects

```dataview
TABLE
FROM #kind/article AND "Content" 
WHERE contains(parent, link(this.file.name))
```

