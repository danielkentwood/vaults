# behavioral taxonomy

##### Metadata
created:: 2023-08-10 12:59
modified:: <%+ tp.file.last_modified_date() %>
mode: #mode/gnosis
kind:: #zettel 
status:: #status/seed
parent:: [[behavioral economics]]
***

Many of the categories in this taxonomy are not discreet categories, but rather constitute continuous dimensions with the opposing categories inhabiting extremes of the dimension. 

* ## Cyclicity
	* **Acyclical (i.e., contextual)**
		* skills: learned behaviors that are contextually deployed
		* instincts: innate behaviors that are contextually deployed
	* **Cyclical (i.e., acontextual)**
		* NOTE: the degree to which someone is able to sustain different types of cyclical behaviors is a type of biomarker. Some people (e.g., with [[ADHD]]) may not be able to retain habits for very long. This should shift the strategy toward external enforcement of [[cyclical behavior]]

* ## Intentionality (a feature of learned behaviors)
	* **intentional:** 
		* Learning: the skill was learned as a result of behaviors that the agent performed with the intention of learning the skill
	* **unintentional**: 
		* Learning: the skill was learned (i.e., picked up) without the intention (and often without the awareness) of the agent

* ## Innateness
	* **Innate**
	* **Learned**

* ## Memory locus
	* **Internalized**: behaviors that do not rely on the [[externalization]] of memory
	* **Externalized**: behaviors that rely on externalized memory artifacts





## External Resources



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



