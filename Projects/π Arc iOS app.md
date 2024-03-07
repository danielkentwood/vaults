# π Arc iOS app

##### Metadata
created:: 2023-10-16 12:36
modified:: <%+ tp.file.last_modified_date() %>
mode:: #mode/management
kind:: #project/startup 
status:: #status/raw
parent:: [[∂ Startup Dashboard]], [[π arc]]

***
## Project Summary

#### iOS app

1. Gen AI assistant
	1. Fine-tuned on health (especially behavioral health) literature (try to find an existing open corpus)
	2. Augmented with specific info about the user
	3. Augmented with aggregated info from all users
2. Start with a target behavior. It can be anything, but must be done daily. Enter it into the app.
	1. It can be at the same time every day, or it can be event-triggered (but the event must happen every day)
	2. (OPTIONAL): Identify at least one motivation/need for the goal. You can propose as many as you want (although experiments are easier when there are fewer).
	3. (OPTIONAL): Identify at least one opposing force that will inhibit the behavior (e.g., habit, uncertainty in schedule due to demands of other people, etc)
	4. (OPTIONAL): Identify what will change in your life if you successfully implement this behavior
	5. (OPTIONAL): Identify what will happen in your life if you don't implement this behavior
	6. NOTE: for any of these steps, if the user is having a hard time coming up with ideas, they can have the GenAI assistant suggest some options.
3. App pushes notification with yes/no button to indicate whether the goal has been completed yet.
	1. If no, app lets you "snooze" the reminder once (you can set the duration)
	2. If no after snooze, app triggers the discovery module
4. Discovery module
	1. congratulates/motivates user re: starting an experiment
	2. "why do you think you didn't do the behavior?"
		1. external (I was too busy, bad weather, etc.)
		2. health (underslept, feeling ill, etc.)
		3. cognitive (I forgot, I remembered but got distracted, remembered but lacked motivation, etc.)
		4. emotional (I was angry, sad, etc.)
		5. mental health (depression, ADHD)
		6. social (embarrassment, pressure from someone, etc.)
	3. after you identify the reason(s) why you didn't do it, identify the needs that were satisfied by those reasons.
		1. for example, if you are underslept, were there any choices you made that contributed to you being underslept? If so, what needs were satisfied by those choices? 

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



