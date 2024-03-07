# ∂ Master Dashboard

##### Metadata
created:: 2023-02-27 17:26
modified:: <%+ tp.file.last_modified_date() %>
mode:: #mode/management
kind:: #dashboard 
status:: #status/raw
parent::
***

# 1. Work

## Most pressing tasks

> [!NOTE] 
> This current approach just shows the top 5 most recent tasks for each project.
> 
> Create a dataview table here that shows, for each dashboard, and for each Aetna project within that dashboard. 
> 1. the highest priority TODO task
> 2. the next due task
> 3. the oldest overdue task
> 
> - NOTE: This requires you to go through all of your tasks, find the ones that truly don't need a due date (i.e., you have no intention of honoring the due date), convert them to TODO.

```dataviewjs

let curr = dv.current();
let curr_nm = curr.file.name;

let work_dashboards = dv.pages('#dashboard and #aetna')
	.where(p => 
		dv.array(p.parent).includes(dv.current().file.link)
	)
	.file.link
	.sort(k => k, 'desc')

for (let i = 0; i < work_dashboards.length; i++) {
	let wd = work_dashboards[i]
	dv.header(3, wd)
	let proj_pages = dv.pages('#project')
		.where(p => 
			dv.array(p.parent).includes(dv.page(wd).file.link) 
		)
		.file.link

	let rem_tasks = dv.pages().file.tasks
		.where(t => t.project)
		.where(t => proj_pages.includes(t.project))
		.where(t => !t.completed)
	
	if (rem_tasks.length > 0){
	    for (let group of rem_tasks
			    .groupBy(t => t.project)
			){
				dv.header(4, group.key)
				dv.taskList(
					group.rows
						.sort(k => k.due, 'desc')
						.slice(0,5), 
					false
				)
			}
	} else {
		dv.el("em", "No pending tasks")
	}	
}
```

***

# 2. Personal
## 2.1 Personal Priorities
* Health. Health. Health! [[General Health Notes]]

## 2.2 Most pressing tasks
```dataviewjs

let curr = dv.current();
let curr_nm = curr.file.name;

let work_dashboards = dv.pages('#dashboard and -#aetna')
	.where(p => 
		dv.array(p.parent).includes(dv.current().file.link)
	)
	.file.link

for (let i = 0; i < work_dashboards.length; i++) {
	let wd = work_dashboards[i]
	dv.header(3, wd)
	let proj_pages = dv.pages('#project')
		.where(p => 
			dv.array(p.parent).includes(dv.page(wd).file.link) 
		)
		.file.link

	let rem_tasks = dv.pages().file.tasks
		.where(t => t.project)
		.where(t => proj_pages.includes(t.project))
		.where(t => !t.completed)
	
	if (rem_tasks.length > 0){
	    for (let group of rem_tasks
			    .groupBy(t => t.project)
			){
				dv.header(4, group.key)
				dv.taskList(
					group.rows
						.sort(k => k.due, 'desc')
						.slice(0,5), 
					false
				)
			}
	} else {
		dv.el("em", "No pending tasks")
	}	
}
```

