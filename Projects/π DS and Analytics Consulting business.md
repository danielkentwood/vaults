# π DS and Analytics Consulting business

##### Metadata
created:: 2023-11-30 12:11
modified:: <%+ tp.file.last_modified_date() %>
mode:: #mode/management
kind:: #project/startup  
status:: #status/raw
parent:: [[∂ Startup Dashboard]]

***
## Project Summary

#### My Brand
- Rapid sizing and roadmapping of project
- Professional comms
- Skills
	- Mentoring/teaching
	- Generative AI (this has to be a focus as the other skills get cannibalized by AI products)
		- Building custom RAG pipelines
		- The cutting edge of customized LLM product engineering
	- Automation pipelines
	- A/B testing and causal inference
	- Predictive modeling
		- classifier models with rich explainability
			- catboost
			- lightgbm
			- shap
		- time series models
	- Graphs
		- skills:
			- knowledge graphs
			- GNNs
		- platforms:
			- tigergraph
			- neo4j
			- python
				- networkx
				- pytorch geometric
	- Cloud platforms
		- GCP
	- Build and serve API
	- Documentation
	- Dashboarding and interactive data
		- D3.js
		- plotly Dash
		- streamlit



#### Cold start problem
- pay experts for their knowledge
	- they get 50/50 split for mentoring me (project basis)
- portfolio
	- needs drastic updating
	- be strategic about the types of projects in there

#### Scaling
* once your network is big enough, start offering colleagues opportunities to take on jobs (you take a small percentage of the fee)
	* they get free business and consulting experience
	* they get access to my codebase and business IP (under contract to not steal for themselves)
* if the hiring market ever warms up again, do mentoring and use your network/resources to attract mentees (similar to what Joe Papa was doing)


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
from #meeting and #mode/management
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



