# π personal notetaking system
created:: 2022-09-06 13:48
modified:: <%+ tp.file.last_modified_date() %>
mode:: #mode/metacognition
kind:: #project
status:: #status/sapling 
parent::  [[∂ Personal Project Dashboard]]
description:: 
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
## Organization
### Folders
* Media
* Periodic
* Projects
* Resources
* Templates

### Dataview metadata fields
#### Page metadata
- title 
- created
- modified
- mode
- kind
- status
- links
- description
- parent
- todo

#### Task metadata
* project
* due
* done (you only need to add this by hand if you mark the task as complete in the same page where you created it -- i.e., outside of a dataview taskList)
* deliverable: code, email, presentation, meeting, report


## Links
Links serve two functions:
1. document-level links act as concept tags
2. in-line links connect an idea to another document

## Tags
Generally tags are for items/blocks instead of notes. Tags delineate either (1) the stage or maturity of the tagged item, or (2) the function of the tagged item.
* #mode
	* #mode/management
	* #mode/metacognition
	* #mode/praxis
	* #mode/creation
	* #mode/gnosis
	* #mode/organization
	* #aetna
* kind (i.e., note type)
	* #periodic
		#periodic/daily: For planning the day, managing the day's tasks, and capturing all new information.
		#periodic/weekly: For weekly reviews
		#periodic/monthly: For monthly reviews
	* #code
	* #dashboard
	* #project: A dashboard for managing tasks, timelines, and ideas for a project. Some tasks grow so much in scope that they need to become their own project note in order to keep track of subtasks, condensing meeting minutes about that task, etc.
	* #meeting
		* #meeting/recurring
		* #meeting/isolated
	* #flashcard
	* #annotation: Actual annotations on a pdf
	* #literature:  Notes/commentary on a resource. That resource can be an imported media file (e.g., pdf), or it can be an external resource (e.g., a physical book, a youtube video, a blog entry, etc.)
	* #goal
	* #resource
		* #resource/data
		* #resource/course
		* #resource/article 
		* #resource/video
		* #resource/website
	* #zettel
		* #zettel/moc
* #status
	* for periodic, meeting, annotation
		* #status/raw
		* #status/processed
	* for zettel, moc, flashcard, literature
		* #status/seed
		* #status/sapling
		* #status/evergreen


### Map of content (MOC)
This approach uses linked documents to conceptually structure the network. It treats a linked document as a tag. MOC documents are usually concepts that link zettel documents. 

### Zettel 
Zettelkasten documents should be atomic ideas that can be clearly expressed in the note title.  There will be an urge to organize them hierarchically, but resist this temptation and focus on horizontal connections to as many other zettels and MOCs as possible. Do this even if the note is part of a book you are writing (the book can be a Content note that you link to in every related note). Let the structure emerge organically. 





***
### maturity
How should I handle the issue of information maturity? For example, let's say I have document for the concept of gradient-boosted random forest models. Should I ever, at any stage of that document, allow it to become bloated with incomplete thoughts or lists of resources to follow up on? No! This is what backlinks are for. Imagine the following process after creating your document:

* You come across an article that seems relevant and you want to read it, but you don't have time at the moment. 
* Instead of linking to it in your concept document, you should 
	* make a note of it in your daily notes
	* create a link from that line to the concept document
	* tag it as *inbox*
	* at some set time (daily and/or weekly), review your daily notes and organize the inbox items. In this case, you would take that article and create a _literature_ note for it. This note holds the URL for the article, and acts as a place to collect notes, comments, and ideas while you read the article. 



## Two dimensions
The system should be organized across two dimensions:
1. Information maturity
	1. Capture
	2. Organize
	3. Distill
	4. Express
2. Type of information
	1. Projects
	2. Areas
	3. Resources
	4. Archive