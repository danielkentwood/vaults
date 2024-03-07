# How to develop new NBA ideas

##### Metadata
created:: 2024-01-23 10:26
modified:: <%+ tp.file.last_modified_date() %>
mode: #mode/gnosis
kind:: #zettel 
status:: #status/seed
parent:: [[π Innovation at Aetna]]
***

- What are the typical NBA categories? 
- What are the available value levers? 
- What are the strategic priorities of your leadership chain? 

#### 0. Preliminary steps
##### 0.1 Get to know Pods (our marketing/design partner)
- You'll be working with the following people in Pods:
	- Design:
		- **Creative Lead**: Responsible for the design (layout, images, copy, enterprise branding standards, etc.) of the creatives
		- **Graphic Designer**: Implements the design
	- Engineering: 
		- **SFMC Architect:** Responsible for coding/engineering the marketing journeys in SFMC (i.e., who gets what, through which channel, when, and how often)
		- **Email Developer**: codes the email templates that will be populated by our data
	- Management
		- **Ops Lead**: Drives formal review process (i.e., feedback and working with creative team to apply changes during reviews)
		- **Test Lead**: POC for E2E execution of the campaign within Pods (e.g., timeline/strategy/logic flow, etc)
		- **Pod Lead**: Owns/manages the Pod.
- Get to know these people (especially test and ops leads). Invest in those relationships. Treat them like members of your team.
- Get _really_ familiar with the [Pods playbook](https://aetnao365.sharepoint.com/sites/BehavioralChangeLab/SitePages/Pods-101-Playbook.aspx) 
- Know the current [Pods learning agenda](https://aetnao365.sharepoint.com/:f:/r/sites/BehavioralChangeLab/Other%20job%20aid%20tools/Learning%20Center?csf=1&web=1&e=U3QB4M). 
##### 0.2 Understand the NBA landscape
- **Get a rough sense for which NBAs are currently running.** This doesn't have to be too exhaustive, but at least quickly browse the current stable of campaigns. This is currently a bit labor-intensive. There is no single, exhaustive source of truth that lists all campaigns in an easy-to-digest format. But you can find documentation for all campaigns on the [Pods sharepoint site](https://aetnao365.sharepoint.com/sites/BehavioralChangeLab/SitePages/Home.aspx).  Look to the sidebar under Pod X Artifacts (and note that some of the campaigns listed there are no longer running or are in development)
- **Have a mental map of the types of NBAs that we typically do.** Here are some general categories:
	* Targeting Members
		* Targeting a specific clinical population
			* Address an existing care gap (or multiple)
				* start/stop doing behavior X
			* Preventing common care gaps (e.g., healthy lifestyle incentives/recommendations, reminder to get vaccinated)
			* Early identification via predictive model (facilitating timely treatment)
			* Disease management
		* Identifying an inefficiency in the medical system
			* site of care recommendation
			* switch from provider A to provider B
			* improve poor transitions in care
	* Targeting Providers
		* Refer your patients to A instead of B
		* Stop doing behavior A (e.g., testing, screening)
		* Start doing behavior A (e.g., diagnosis, prescribing, get member in for visit)
		* Switch your patient's prescriptions/regimen (more, less, different)
	* Testing a marketing concept (these are typically layered over an established campaign)
		* Test a behavioral psychology/economics principle
		* Test a journey design
		* Test a creative
#### 1. Identify the NBA concept
* What are the strategic priorities of your leaders? 
* What kind of NBA is it? 
* What are the value levers?
* Which clinical population are you targeting, and how will you operationally define it? 
#### 2. Early sizing
* The goal here is to find the projected medical cost savings for the concept, as quickly as possible.
	1. Find the volume of members in your experiment (i.e., average unique members that match the operational definition within a year)
	2. Find how much money (in paid amount) we're spending on their claims in a given year
	3. Split the total volume in half (to represent assignment to test and holdout groups)
	4. Assume that members who respond to your intervention would see a 10-40% reduction of the above amount (depending on confidence regarding the intervention and how it might impact the overall health of the member)
	5. Assume that .5% of the test group will change their behavior due to the intervention
	6. So the estimated MCS from this concept equals:
		   test volume * average yearly paid amt * assumed cost reduction * .005 (BC assumption)
   - If it's below 500K, file it away.
   - If it's above 500K, it deserves a deeper dive. 
#### 3. Deep-Dive Sizing
##### 3.1 Sharpen assumptions and campaign concept
- Meet with clinical partners to sharpen your clinical understanding of the concept, to validate the concept, and to explore ideas for interventions

##### 3.2 Stock and flow power analysis









## Contextual Notes
```dataviewjs
let curr = dv.current()

let pages = dv.pages("(#periodic/daily or #zettel) and -#project")
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