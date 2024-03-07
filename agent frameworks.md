# agent frameworks

##### Metadata
created:: 2023-12-04 14:03
modified:: <%+ tp.file.last_modified_date() %>
mode: #mode/gnosis
kind:: #zettel 
status:: #status/seed
parent:: [[llm chat applications]]
***






## External Resources
* Curated list of agents: https://github.com/e2b-dev/awesome-ai-agents
* AutoAgents:
	* https://github.com/Link-AGI/AutoAgents
* smol developer
	* https://github.com/smol-ai/developer/
* MetaGPT
	* https://github.com/geekan/MetaGPT
	* paper: https://arxiv.org/abs/2308.00352
* AutoGen
	* https://github.com/microsoft/autogen
	* articles:
		* https://e2b.dev/blog/microsoft-s-autogen
		* https://medium.com/@krtarunsingh/autogen-advanced-beyond-the-basics-and-into-real-world-applications-d648a59ed6cb
		* https://medium.com/microsoftazure/introducing-autogen-df7fa6cb81ee
	* an attempt at an "enhanced" version of agents in AutoGen (starts with PoC of a Memory-Enabled Agent): https://github.com/Andyinater/AutoGen_EnhancedAgents
- Taskweaver: [https://github.com/microsoft/TaskWeaver](https://protect-usb.mimecast.com/s/bVwMCB1G7jH8JqV1ZK2SrYe95?domain=github.com "https://protect-usb.mimecast.com/s/bVwMCB1G7jH8JqV1ZK2SrYe95?domain=github.com")

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