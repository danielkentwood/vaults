# π Corpus

##### Metadata
created:: 2023-09-28 16:43
modified:: <%+ tp.file.last_modified_date() %>
mode:: #mode/management
kind:: #project/startup  
status:: #status/raw
parent:: [[∂ Personal Project Dashboard]], [[∂ Startup Dashboard]]

***
## Project Summary

### Summary
Corpus is a platform where users can easily add, analyze, visualize, and license their own medical data. 
- it is a medical data marketplace powered by a distributed graph (i.e., blockchain) 
- it is also a platform where users find incentives to take ownership over their own medical journey

### Interfaces available
- flexible, interactive graph representations of existing medical journey
- inference + visualization:
	- What are my risks? Models trained to predict risk of disease
	- How long will I live? Models trained to predict the most likely death scenarios for the user
		- [[π Countdown]] style visualizations that frame your life in terms of experiences remaining
- Marketplace:
	- user earns money:
		- behavior change campaigns from insurance providers (we can handle fulfillment for a fee)
		- experiment/study recruiting
		- data licensing
	- user pays money:
		- targeted product offers
- sometimes we have a specific question and don't want to sift through timelines or graphs, so Corpus also provides a natural language interface to their health data (open-source/fine-tuned LLM with retrieval augmented generation)

### data tools
- tool for user to request their personal health data from various sources
	- request claims data from health insurance provider
	- request EMR, biosignal data from providers
	- request health metrics from tech companies (e.g., Apple, Noom, Oura, etc)
	- we load user data onto a blockchain, allowing the user to control it and license it for data consumers (we take a small cut of the transaction)
- tool for user to license their data to data consumers
	- user gets to decide terms of licensing
		- levels of permission: de-identifying; arbitrary filters for time period, data type, procedure type, etc.
		- how long? licensing can be renewed yearly, etc.
- tool making it easy to share your clinical history (e.g., with a new provider) with the push of a button
- tools that help you invite your family members to connect their data to yours (in ways that preserve privacy)
- tools that allow providers to easily add new data to a user's chain (at their request) via integrations with existing software

### revenue model
- user can pay small fee for upgraded analytics and visualizations (NOTE: they need to opt in to sharing their data with us in order to get access to the analytics and visualizations)
- we take small percentage of transactions on the blockchain (e.g., users selling their data to companies)
- companies can pay us to perform analytics on data they have permission to use
- companies can advertise for their offers
- companies can pay us to run experiments
- training and selling access to a medical LLM (if/when we have large-scale medical data)
- training and selling access to federated learning models and synthetic data
- tokenization: if users choose to complete transactions with our token instead of USD, the conversion fee is waived (or some other incentive to use our token)

##### Partnership with Aetna

**Benefit to Corpus**
To solve the cold-start problem. This could be an Aetna-backed venture, and would benefit from Aetna's already powerful reach. Aetna could have a massive digital campaign that nudges members to opt-in to the Corpus platform, giving the member access to rich visualizations of their own personal data, predictive analytics, and tools to integrate all of their health data into one place where they own it and can make money off of it (instead of other companies making money off of their data)

**Benefit to Aetna**
The whole problem with outreach from Aetna (and other payors) is that very few people trust us (and with good reason). The effectiveness of our campaigns is limited primarily by poor engagement. We need people to have a compelling reason to come to us and ask for help, rather than us coming to them and asking them to do something. Corpus provides an interface and platform for payors like Aetna to:
- engage members in personalized campaigns
- encourage members to take more ownership over their health generally, leading to better outcomes and more efficient interaction with the healthcare system
- gain access to richer data from the member (by licensing from the member)

**Risks to Corpus**
People may not trust Corpus when they discover that it spun off from Aetna, and that Aetna is a major investor. To address this, we can be clear that Corpus cannot provide data permissions to anybody (including Aetna) -- rather, the user controls all permissions for their data, with Corpus providing tools and a platform that facilitate the transactions. Outside of a return on their investment, Aetna cannot benefit preferentially from their investment in Corpus.

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





