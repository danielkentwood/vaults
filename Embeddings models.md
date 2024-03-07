# Embeddings models

##### Metadata
created:: 2023-11-09 16:31
modified:: <%+ tp.file.last_modified_date() %>
mode: #mode/gnosis
kind:: #zettel 
status:: #status/seed
parent:: [[NLP]], [[LLM]]
***






## External Resources
- https://txt.cohere.com/introducing-embed-v3/
	- "A model that just measure topic match like OpenAI text-embedding-ada-002 retrieves mostly irrelevant results. The retrieved hits are on-topic, but provide little information on the topic.  Our new Embed v3 models not only measures topic match, but also content quality. A text that provides e.g. detailed information on COVID-19 symptoms will rank higher than a document just stating 'COVID-19 has many symptoms'."
	- "You can either use our API (free until you go into production, then $0.0001 / 1K tokens) or deploy in your own VPC."

## Contextual Notes
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