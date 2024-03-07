# ∂ Vault Maintenance
title: ∂ Vault Maintenance
created:: 2022-09-22 09:34
modified:: <%+ tp.file.last_modified_date() %>
mode:: #mode/metacognition 
kind:: #dashboard
status:: #status/processed 

***

## Tasks without a due date
```dataviewjs
dv.taskList(dv.pages('-"Templates"').where(p => {
	return !p.ignoreTasks
}).file.tasks
	.where(t => !t.completed)
	.where(t => !t.due))
```
