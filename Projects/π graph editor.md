# π graph editor
title: π graph editor
created:: 2022-09-05 16:45
modified:: <%+ tp.file.last_modified_date() %>
mode:: #mode/creation 
kind:: #project/OSS 
status:: #status/raw
parent:: [[∂ Personal Project Dashboard]]

***

## Project Summary
### Basic idea: Build a graph/network editor in D3.js
* Start with a single node.
* Each node has a name (visible), a description (optional, hidden), and any arbitrary set of attributes (hidden).
* Hovering over the node shows:
	* the hidden features
	* a "+" button, which, if clicked, will sprout a new node (with an edge connecting to it)
* You can click on edges to give them attributes (e.g., directed or undirected)
* There are several graph types
	* You can build in any graph type
	* You can convert from the current graph type to any other compatible graph type
* Each node is a link to a markdown document

### Why is this useful?
* Sometimes, especially when you are starting fresh (i.e., on learning a new topic, on writing a a new article, etc.), it is helpful to start with the visual map.
* We usually start with an outline, which is (I'm convinced) our attempt to implement a graph within the constraints of a word processor. 

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
