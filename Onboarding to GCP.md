# Onboarding to GCP

##### Metadata
created:: 2024-01-26 12:19
modified:: <%+ tp.file.last_modified_date() %>
mode: #mode/gnosis
kind:: #zettel 
status:: #status/seed
parent:: [[π NeuroNudge]]
***

- CEBC sharepoint 
	- for migration: [GCP Migration](https://aetnao365.sharepoint.com/:f:/r/sites/CEBC961/Shared%20Documents/General/GCP%20Migration?csf=1&web=1&e=qUcjAR)
	- for Onboarding and Training: [Onboarding and Training](https://aetnao365.sharepoint.com/:f:/r/sites/CEBC961/Shared%20Documents/General/Onboarding%20and%20Training?csf=1&web=1&e=fPbM9c)
- ABC GCP Onboarding repo
	- For the team lead: https://github.aetna.com/abc-cloud/abc-gcp-onboarding/blob/master/onboarding.md
	- For the new hire: https://github.aetna.com/abc-cloud/abc-gcp-onboarding/blob/master/getting-started-with-gcp.md
- CEBC GCP wiki
	- https://github.aetna.com/ca-nba-pods/cebc-gcp-documentation/wiki
	- https://github.aetna.com/ca-nba-pods/cebc-gcp-documentation/wiki/K.-New-Team-Member-Onboarding
- ABC tech repo
	- a few GCP relevant items on the 'new employee' page: https://github.aetna.com/analytics-org/abc-tech-repo/blob/c114e1518ee6b84797366d28c4b64e42d16d4777/new_employee/new_employee.md

- What can I do for the new hires before they arrive?



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


