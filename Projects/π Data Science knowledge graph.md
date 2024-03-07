# Data Science knowledge graph
created:: 2022-08-31 05:16
modified:: <%+ tp.file.last_modified_date() %>
mode:: #mode/management
kind:: #project 
status:: #status/raw
parent:: [[π SkillGraph]]

***
## Project Summary

***
## Rollups
### Subprojects
```dataview
TABLE
FROM #project 
WHERE contains(parent, link(this.file.name))
```

### Task backlog
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
***
### Meetings
```dataview
table created
from #meeting and #mode/management and #aetna
where contains(parent, link(this.file.name))
sort created asc
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
***
## Documentation





## Why this Project?

Can I create a knowledge graph that hierarchically organizes the various branches of data science in an unsupervised manner?

## Notes/Thoughts:

- Pull data from Toward Data Science and other DS publications on Medium
- Scrape other data science websites?

---

# Project Workspace:

## Build a hierarchical knowledge graph of math/stats/ds/ml/engineering concepts:

- Identify data sources
    - High confidence: textbooks, tech company blogs, tech journals
    - Low confidence: medium (e.g., TDS), kaggle, KDnuggets
- Perform an initial pass to pull/scrape articles from these sources and put them into a database.
    - Schedule periodic pulls/scrapes from the designated data sources to update the database
- Python scripts pull from database and create a knowledge graph
    - Knowledge Graphs
    - Extract entities
    - Coreference resolution
    - Extract edges:
        - "is a branch of"
        - "is an implementation of"
        - "is necessary for"
        - "is a technique for"
        - “is a kind of”
    

