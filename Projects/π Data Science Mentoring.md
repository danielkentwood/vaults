# π Data Science Mentoring
title: π Data Science Mentoring
created:: 2022-08-25 16:34
modified:: <%+ tp.file.last_modified_date() %>
mode:: #mode/management
kind:: #project 
status:: #status/raw
parent::

***
## Project Summary


## Rollups
### Subprojects
```dataview
Table
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

## Notes
### On bootcamps vs internships

There is something fundamentally different about the candidates that have prior experience with a mature DS team. It attunes you in ways that are just incredibly difficult to replicate outside of that environment. It forces you to build, in essence, muscle memory of the foundational tasks that are not so common outside of a DS role. 

**If you are struggling to break into DS, here is my advice:**
* Get an internship. You'll get paid to learn. But these are rapidly becoming the new bottleneck due to competition.
* If an internship is not an option, do a *mock internship*! This is a mix between a bootcamp and a mentorship, where you work on a team with other trainees, asynchronously. 
* If internship or mock internship are not options, do a mentorship.

**Why no bootcamps?** 
* IMHO, if you're good enough to get into one of the quality bootcamps, you are probably already good enough to do DS. 
* What you're paying for in those bootcamps is a little bit of intense practice (which you could've done on your own), but mostly you're paying for the industry partnerships that these bootcamps have. 
* The bootcamps are typically one-size-fits-all. Due to their scale, they lack the flexibility to help you identify your specific gaps and focus on filling them. You'll waste time and money covering material that you already know.  
* They are exclusionary in most cases. You have to be physically present at a location for an extended period, something that is out of reach for many older applicants who have families.



### Your information pipeline
Everyone has a pipeline. Most people don't have insight into what their pipeline is, and therefore they don't know if it is doing what they want it to do. The pipeline has 4 basic steps:

1. Capture
2. Filter
3. Process
4. Package

1. How/when do you capture information?
	1. During conversations
	2. During lectures/lessons
	3. During reading
	4. During browsing
	5. During problem-solving (e.g., coding)
2. How do you filter the information you capture? 
	1. Triage: Decide what you should do with the information (this actually jumps ahead to step 4 to anticipate how you might package the information for consumption -- who is the audience? How will they use the info?)
3. How do you process the filtered information?
	1. Rephrase: put it into your own words
	2. Connect: find connections with other information
	3. Extract: identify the most important claims/arguments/etc.
	4. Critique: identify where you disagree with the claims, and why
	5. Extend: generate novel ideas that go beyond the claims from your sources
4. How do you package the information for consumption? (this step determines a lot of the preceding steps)


## Future sections
* How to discover gaps in skills
* How to fill gaps in skills
* How to know which skills to focus on 
* The unwritten rules of data science interviews
* How to select a good project
* How to prepare for interviews
* How to "woo" a company



