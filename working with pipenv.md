# working with pipenv

##### Metadata
created:: 2024-03-05 15:13
modified:: <%+ tp.file.last_modified_date() %>
mode: #mode/gnosis
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

### working with pipenv
After installing pipenv, you need to open the pipenv shell in the directory where you want the pipfile to be located. 
```bash
pipenv shell
```

From there you can install packages:
```bash
pipenv install pandas
```

You can install some of them only for dev:
```bash
pipenv install pytest --dev
```

When you're done installing your packages, you can lock the pipfile so it stays the same for production:
```bash
pipenv lock
```

Finally, once you're ready to go, you should tell pipenv to ignore the pipfile and always use the pipfile.lock for installations. 
```bash
pipenv install --ignore-pipfile
```

To leave the pipenv shell, just type `exit`.

To delete the shell, type `pipenv -rm`

