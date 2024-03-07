# SkillGraph brand identity
created:: 2022-08-29 09:20
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

***
# Marketing/Branding


* "Ditch your resume."
* "Kn/Gr/Flow your skills." (animation)




## What does my idea offer?
* **A user-focused SaaS platform.** It optimizes for the experience of the individual rather than the organization. It will have an engaging, immersive UI.
* **A replacement of the resume**. If successful, it will make resumes obsolete. 
* **Gamification of skill tracking and validation.**
* **Recommendations for skill development.** Constantly updated repository of online learning content as sources of skill validation.
* **Tools, not just resources, for skill development.


## Brand
It is a platform for quantifying skill. Once it is quantified, several doors open:
* **Hiring**
	* More equitable comparisons between candidates during hiring
	* More reliable information about what the candidate can and cannot do
* 

