# Docker Instructions for local macbook usage

##### Metadata
created:: 2024-02-07 11:35
modified:: <%+ tp.file.last_modified_date() %>
mode: #mode/gnosis #aetna 
kind:: #zettel 
status:: #status/seed
parent:: 
***

### Docker Instructions for local macbook usage
0. set up the proxy (see [[set up proxy on local machine]])
1. start the daemon with the "Docker Desktop" app
2. run docker-compose commands




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

