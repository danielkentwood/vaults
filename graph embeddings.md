# graph embeddings

##### Metadata
created:: 2023-12-04 10:57
modified:: <%+ tp.file.last_modified_date() %>
mode: #mode/gnosis
kind:: #zettel 
status:: #status/seed
parent:: 
***
In static [[Graph Neural Networks]], [[message passing]] is an iterative construction of embeddings, and the number of iterations corresponds to the number of layers in the GNN. With each layer there is another pass of message passing, and each node embedding incorporates information about its immediate neighbors. So on the first pass, each node embedding contains information only about the node's neighborhood. On the second pass, it will incorporate information about the neighbors of its neighbors. Do this enough times and you get _oversmoothing_--i.e., every node contains essentially the same information about every other node in the graph. So there is a tension between the depth of the network and the smoothness of the embeddings. There are approaches that solve this problem -- e.g., [PairNorm](https://openreview.net/forum?id=rkecl1rtwB).





## External Resources
* Graph node embedding algorithms (stanford fall 2019): https://www.youtube.com/watch?v=7JELX6DiUxQ
* Brief explainer of graph embeddings: https://neo4j.com/blog/graph-embeddings-ai-learns-solve-problems/



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




# Resources

