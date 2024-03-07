# π AI-native behavioral health clinic

##### Metadata
created:: 2023-11-30 13:59
modified:: <%+ tp.file.last_modified_date() %>
mode:: #mode/management
kind:: #project/startup  
status:: #status/raw
parent:: [[∂ Startup Dashboard]]

***
## Project Summary

#### Team
* Approach Jason about incubating this within CVS 
* Maybe also approach Eli to see if he's interested? 
* This dovetails with Nicolette's interests! 
#### value prop
##### For clinicians
* AI-driven training of clinicians on best practices
	- contextualized: immediate feedback after sessions
	- personalized: takes into account history/situation of patient
	- actionable: provides data-driven, explainable recommendations for next steps
- tools for summarizing, analyzing, and finding insights from session transcriptions
##### For patients
* privacy and full ownership over their data
	* Transcripts go immediately to them (and them only). They grant access back to the company via opt-in
		* possible to use blockchain for the database? the distributed nature of the blockchain
	* Granting data access is compensated (discounts, etc.)
	* all data are de-identified prior to consumption/analytics
	* provider-agnostic: platform offers tools so they can sell their data to anyone, not just us
* they get access to our behavior change app
	* recommendations driven by behavioral economics + causal inference + peer-reviewed standards + AI


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

Mental/behavioral health counseling and care companies that are leveraging AI: https://www.perplexity.ai/search/Please-lay-out-Gx85cydATZy0FgnIX5iFDA?s=c
* Ginger
* Lyra Health
	* https://www.datasciencecentral.com/ai-ushers-in-a-new-era-of-mental-health-monitoring/
* Centerstone and Lyssn
	* https://www.fiercehealthcare.com/ai-and-machine-learning/centerstone-taps-tech-company-lyssn-build-out-ai-based-training-behavioral
* Aiberry



