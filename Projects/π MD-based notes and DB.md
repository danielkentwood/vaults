# π MD-based notes and DB
title: π MD-based notes and DB
created:: 2022-09-20 17:18
modified:: <%+ tp.file.last_modified_date() %>
mode:: #management
kind:: #project/OSS 
status:: #status/raw
parent:: [[∂ Personal Project Dashboard]]]

***
## Project Summary
I want to create a note-taking software with the following features:
* Markdown (with embedded JS) front-end
* javascript back-end
* open-source plug-in community
* Metadata can be assigned to pages, lines, and words
* Tables
	* for generating arbitrary tables, lists, etc. 
	* All fields in tables are editable (similar to notion), and the edits will propagate to the original location of the data
	* filter/sort controls on the tables (similar to excel)
	* you can arbitrarily add rows, columns. 
		* as soon as the table pulls in data from more than one source, each row displays the source as a tag next to the row
		* you can add new data to a table that pulls from outside sources -- those rows will have a tag indicating that it is new data
	* at any point, you can choose to decouple the data from its source (essentially, create a copy of the data view, making the table a new, unique data source). 
	* you can also freeze the table so that it is not possible to edit it
	* column-wise operations (not cell-wise) can be implemented (e.g., aggregations, mutations, filtering, etc)
	* as new rows and columns are manually added to the table, the original query is modified. In essence, you can build a table manually, or you can build it with the query. These are interchangeable, and you can learn how to do the queries by doing the manual build and checking the query to see how it changed. The query approach is more flexible/powerful than the GUI based manual process, so there is still incentive to use the query approach.
* Tools for calendaring and task-tracking 
* 

## Task backlog
```dataviewjs

let curr = dv.current();
let curr_nm = curr.file.name;

let proj_pages = dv.pages('#project')
	.where(p => 
		dv.array(p.parent).includes(dv.current().file.link) ||
		p.file.name == curr_nm
	)
	.file.link

let all_tasks = dv.pages().file.tasks
	.where(t => t.project)
	.where(t => proj_pages.includes(t.project)
	)

let done_tasks = all_tasks.where(t => t.completed)
let still_tasks = all_tasks.where(t => !t.completed)
	
dv.header(4, 'Remaining tasks:')	
if (still_tasks.length > 0){
    for (let group of still_tasks
		    .groupBy(t => t.project)
		){
			dv.header(5, group.key)
			dv.taskList(group.rows, false)
		}
} else {
	dv.el("em", "No pending tasks")
}

dv.paragraph('<br><hr>')
dv.header(4, 'Completed tasks:')	
if (done_tasks.length > 0){
    for (let group of done_tasks
		    .groupBy(t => t.project)
		){
			dv.header(5, group.key)
			dv.taskList(group.rows, false)
		}
} else {
	dv.el("em","No completed tasks")
}
```


### Contextual Notes
```dataviewjs
let curr = dv.current()

let pages = dv.pages("#periodic/daily and -#project")
	.where(p => {
		if (p.sendto) {
			let sendto = dv.isArray(p.sendto) ? 
				p.sendto : 
				dv.array(p.sendto);
			if (sendto.some(str => str.includes(curr.file.name))) {
				return true
			}
		}		
	})
	.sort(p => p.file.cday, "asc")

function formatLinks(page) {
	let st_arr = dv.isArray(page.sendto) ?
		page.sendto.filter(str => str.includes(curr.file.name)) :
		dv.array(page.sendto).filter(str => str.includes(curr.file.name));

	let link_arr = st_arr.map(str => {
		return dv.sectionLink(
			page.file.name,
			("sendto:: " + str.replace(/\[\[/g, '').replace(/\]\]/g, '')),
			false,
			str.replace(/\[\[.*?\]\]/g, '')
		)
	});

	return link_arr
}

// set up table
dv.table(
	["File", "Note"], 
	pages
	.map(b => [
		b.file.link,
		formatLinks(b)
	])
)
```

## Documentation
