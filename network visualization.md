# network visualization

##### Metadata
created:: 2023-08-10 12:59
modified:: <%+ tp.file.last_modified_date() %>
mode: #mode/gnosis
kind:: #zettel 
status:: #status/seed
parent:: 
***



## External Resources
* [Interactive subreddit network](http://www.jacobsilterra.com/subreddit_map/network/index.html#): Shows an interactive graph of top subreddits, with edges determined by commenter overlap. 


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




