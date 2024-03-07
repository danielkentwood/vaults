# PERT + CPM Project Scheduling

##### Metadata
created:: 2023-12-01 15:36
modified:: <%+ tp.file.last_modified_date() %>
mode: #mode/gnosis
kind:: #zettel 
status:: #status/sapling 
parent:: [[project management]]
***

The Critical Path Method (CPM) is a quantitative approach to project management. 

Program Evaluation and Review Technique ([[PERT estimation]]) is a tool for estimating completion time for an activity. It is calculated as:
$$
PERT = \frac{O + 4M + P}{6}
$$
where O is the optimistic estimate, M is the most likely estimate, and P is the pessimistic estimate. 
### Steps in CPM
1. Identify all tasks and encode them as nodes
2. Build a DAG by identifying dependencies (i.e. prerequisite relationships) between tasks and connecting the nodes accordingly. All nodes without a predecessor are connected (as children) to a "start" node. All nodes without a successor are connected (as parents) to an "end" node. This DAG will often have multiple paths from "start" to "end". 
3. Use PERT to identify weight/duration of each task
4. Complete forward pass to identify the earliest start and finish times for each task/node. 
5. Complete backward pass to identify the latest start and finish times for each task/node.
6. Calculate the "slack" (i.e., the delta between earliest and latest start/finish times) for each node. 
7. The activities with 0 slack are called "critical activities"; they cannot be adjusted without delaying the project as a whole.  The path that traverses the critical activities is the critical path through the project. The goal is to prioritize these activities while allowing flexibility around the activities that have some slack.


## External Resources

* great explanation of quantitative project mapping (forward and backward pass through a DAG): https://www.youtube.com/watch?v=-TDh-5n90vk
* prose article explaining CPM: https://hbr.org/1963/09/the-abcs-of-the-critical-path-method
* repos:
	* https://github.com/juwonzylee/critical-path-method
	* https://github.com/akeita11/Designing-And-Evaluating-Critical-Path-Methods-Genetic-Algorithms-to-Assess-Critical-Activities/tree/master
* article comparing software for critical path planning: https://clickup.com/blog/critical-path-software/v
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