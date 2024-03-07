# set up proxy on local machine

##### Metadata
created:: 2024-02-07 11:33
modified:: <%+ tp.file.last_modified_date() %>
mode: #mode/gnosis #aetna 
kind:: #zettel 
status:: #status/seed
parent:: 
***

* add a self-signed certificate to `/etc/ssl/certs/` dir (you have to use sudo and provide your login password)
```bash
sudo cp AetnaInternalRoot.pem /etc/ssl/certs
```
* get proxy URL (including URL-encrypted username and password) -- you can use boa for this
* add the HTTPS and HTTP proxies definitions as env variables (oddly, both of them need to start with http://)
```bash
export HTTPS_PROXY=http://A522860:mypassword@proxy.aetna.com:9119
export HTTP_PROXY=http://A522860:mypassword@proxy.aetna.com:9119
export REQUESTS_CA_BUNDLE="/etc/ssl/certs/AetnaInternalRoot.pem"
```




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

