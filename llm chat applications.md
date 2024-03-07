# llm chat applications

##### Metadata
created:: 2023-12-19 15:09
modified:: <%+ tp.file.last_modified_date() %>
mode: #mode/gnosis
kind:: #zettel 
status:: #status/seed
parent:: [[LLM]]
***






## External Resources

* Ollama
	* youtube tutorial: [https://youtu.be/y7wMTwJN7rA?si=UIf60cjeAxiMXItP](https://protect-usb.mimecast.com/s/8mAGCA8E7ghEJ09gmOqh2bn6M?domain=youtu.be "https://protect-usb.mimecast.com/s/8mAGCA8E7ghEJ09gmOqh2bn6M?domain=youtu.be")
- Taskweaver: [https://github.com/microsoft/TaskWeaver](https://protect-usb.mimecast.com/s/bVwMCB1G7jH8JqV1ZK2SrYe95?domain=github.com "https://protect-usb.mimecast.com/s/bVwMCB1G7jH8JqV1ZK2SrYe95?domain=github.com")
- Memory management: 
	- memgpt: [https://memgpt.ai/](https://protect-usb.mimecast.com/s/mnSNCDwK7lh3rpB16AGI8p9y-?domain=memgpt.ai/ "https://protect-usb.mimecast.com/s/mnSNCDwK7lh3rpB16AGI8p9y-?domain=memgpt.ai/")
	- kernel memory: [https://github.com/microsoft/kernel-memory](https://protect-usb.mimecast.com/s/aWz0CEKL7mupoyWmAxXH4Ulp2?domain=github.com "https://protect-usb.mimecast.com/s/aWz0CEKL7mupoyWmAxXH4Ulp2?domain=github.com")
- [how to use mistral 8x7b on google cloud](https://www.linkedin.com/pulse/how-use-mistral-8x7b-google-cloud-frederic-molina-nsfhe/)
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