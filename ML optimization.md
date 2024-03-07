# ML optimization

##### Metadata
created:: 2023-12-04 10:57
modified:: <%+ tp.file.last_modified_date() %>
mode: #mode/gnosis
kind:: #zettel 
status:: #status/sapling 
parent:: 
***

## Techniques for squeezing out more performance from your models
### Adversarial validation
[[Adversarial validation]]

### Interesting metrics
* [[Area under the precision-recall curve]]

### Constructing your training set
#### Accounting for label accuracy
Always think about your labels as the result of a previous model (whether ML, heuristic, cognitive, etc.)! 

In many (most?) real-world cases, the labels that you have for your variables (including your target variable) are not 100% dependable. 

For example, pre-eclampsia diagnoses: It is likely that most people who get a preeclampsia diagnosis actually do have preeclampsia (high [[model precision]]), but it is also likely that many people who have preeclampsia are not getting diagnosed properly (non-trivial reduction in [[model recall]]). If you keep all of these people in the training set, you are essentially telling your model that they are negative examples when, in fact, they are not. This will hurt performance, even if the mislabeling issue will continue to infect the out-of-sample data that you'll test your model on. If we were able to remove such examples from the training set, we would be able to train a model that more effectively learns differences between negative and positive examples. 

Sometimes there will be no principled way to curate the data. If there is, train two models:
1. Full distribution (including mislabeled samples)
2. Curated distribution (removing/correcting mislabeled samples)

When we introduce a full distribution to the model in the form of the validation or test set, we hope to have two outcomes: (1) a drop in performance relative to the model trained on the curated data, but hopefully an increase in performance relative to the model trained on the full dataset, and (2) an increased confidence that the false positives are actually mislabeled true positives. The tricky part, of course, is finding a way to confidently identify and remove the false negatives from your training set. 

### Study model performance in subpopulations
1. Find subpopulations in your data (whether via heuristics or unsupervised methods). 
2. Identify the subpopulations for which the model has poor performance
3. Diagnose why the model struggles with that subpopulation
	1. maybe the subpopulation lacks data in a certain features
	2. maybe there aren't enough samples for that subpopulation
	3. maybe there are differences between the training and test set for this subpopulation (see [[Adversarial validation]] for one way to diagnose this)
4. Fix the issue 
	1. it's usually a data issue instead of a model issue
	2. use synthetic data






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


