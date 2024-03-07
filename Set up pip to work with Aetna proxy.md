# Set up pip to work with Aetna proxy

##### Metadata
created:: 2024-03-05 15:12
modified:: <%+ tp.file.last_modified_date() %>
mode: #mode/gnosis #aetna 
kind:: #zettel 
status:: #status/seed
parent:: 
***


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

### Set up pip to work with Aetna proxy

1. Make sure you have the AetnaInternalRoot.pem certificate file in your home dir
2. Build a pip config file and add the path to the certificate
```bash
pip config set global.cert ~/AetnaInternalRoot.pem
```
3. Edit your pip config file (on a mac, it is usually found in ~/.config/pip/pip.conf) so it looks like this: 
```toml
[global]
cert = /Users/a522860/AetnaInternalRoot.pem
trusted-host =  pypi.python.org
				pypi.org
				files.pythonhosted.org
proxy = http://{your AID}:{your URL encoded password}@proxy.aetna.com:9119
```


