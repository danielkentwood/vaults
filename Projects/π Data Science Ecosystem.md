# Data Science Ecosystem
created:: 2022-08-31 05:16
modified:: <%+ tp.file.last_modified_date() %>
mode:: #mode/management
kind:: #project 
status:: #status/raw
parent:: [[π Job Market Dashboard]]

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





**Pitch:**

- Many people want to break into data science, but are geographically constrained. They need a way to explore the existing opportunities in their city.
- Currently, the way that most data scientist job candidates match themselves with a company is through a skill set or tech stack. Do I meet the experience/skill requirements in the job ad? This seems like a suboptimal way of matching candidates with jobs. Getting a sense for what candidates like to do or want to do, then matching that with what companies are doing, is probably going to lead to much better outcomes. Or at least providing an interface where candidates have a sense for what their tasks will be like at a given company, rather than what they have to know, will lead to less turnover, more informed and better prepared candidates.
- 

**What is it?**

- An app that lets you explore the data science ecosystem in your city.

DESIGN:

DB Tables:

1. User
    1. ID
    2. Link
    3. Name
    4. Current Role
    5. Past Roles
    6. Skills listed
    7. Current company ID
2. Company
    1. ID
    2. Link
    3. Name
    4. Number of local employees in DS
    5. 
3. Job Listing

**How?**

- There are lots of job boards out there: [https://www.dataquest.io/blog/career-guide-find-data-science-jobs/](https://www.dataquest.io/blog/career-guide-find-data-science-jobs/)
- We can use the info from these job boards to get info about the companies.
- However, LinkedIn also gives us very valuable information about the individual user profiles, where they work, what they do, for how long, what their skill sets are, etc.
- Use the LinkedIn API (start here, and maybe go to other job boards after) to pull the following info:
    - For a given company within the specified geographical area:
        - How many people on LinkedIn list that company as their employer and have a job description that matches a specified job? (i.e., how large is the data science team?)
        - What is the size of the company?
        - How long have people been working in that company in a data science role? (i.e., how old is the data science team?)
        - What is the data science stack at this company? Use job ads to build this up.
        - Information about the team hierarchy, like who the hiring manager is at the company, etc.
        - What field is the company in?
        - What kinds of tasks are the data scientists typically doing there (e.g., NLP, computer vision, etc.)?
        - Build a recommender system that takes as input the preferences and skills of the applicant, and returns companies that would be a good fit.
        - What skill-sets do people typically list who work at this company?
        - How much data science experience do people in this company have?
- Build a pipeline that scrapes the data on a regular basis, updates the database, and deploys the updates automatically.

**Front end:**

- User can search for a city and get a list of the companies in that city that have data science teams.
- User can enter in a job description and/or list of skills, and the app will recommend good fits for them.