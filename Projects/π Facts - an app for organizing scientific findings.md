# π Facts - an app for organizing scientific findings
created:: 2022-08-31 05:16
modified:: <%+ tp.file.last_modified_date() %>
mode:: #mode/management
kind:: #project/startup  
status:: #status/raw
parent:: [[∂ Personal Project Dashboard]], [[∂ Startup Dashboard]]
[[document understanding]], [[claim extraction]]

***
## Project Summary

***
## Rollups
### Subprojects
```dataview
TABLE
FROM #project 
WHERE contains(parent, link(this.file.name))
```

### Task backlog
```dataviewjs

let curr = dv.current();
let curr_nm = curr.file.name;

let proj_pages = dv.pages('#project')
	.where(p => 
		dv.array(p.parent).includes(dv.current().file.link) ||
		p.file.name == curr_nm
	)
	.file.link

let all_tasks = dv.pages().file.tasks
	.where(t => t.project)
	.where(t => proj_pages.includes(t.project)
	)

let done_tasks = all_tasks.where(t => t.completed)
let still_tasks = all_tasks.where(t => !t.completed)
	
dv.header(4, 'Remaining tasks:')	
if (still_tasks.length > 0){
    for (let group of still_tasks
		    .groupBy(t => t.project)
		){
			dv.header(5, group.key)
			dv.taskList(group.rows, false)
		}
} else {
	dv.el("em", "No pending tasks")
}

dv.paragraph('<br><hr>')
dv.header(4, 'Completed tasks:')	
if (done_tasks.length > 0){
    for (let group of done_tasks
		    .groupBy(t => t.project)
		){
			dv.header(5, group.key)
			dv.taskList(group.rows, false)
		}
} else {
	dv.el("em","No completed tasks")
}
```
***
### Contextual Notes
```dataviewjs
let curr = dv.current()

let pages = dv.pages("#periodic/daily and -#project")
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

***
## Documentation





SPECTER: Document-level Representation Learning using Citation-informed Transformers
[https://allenai.org/data/scidocs](https://allenai.org/data/scidocs)
[2004.07180.pdf](2004.07180.pdf)
[https://github.com/allenai/scidocs](https://github.com/allenai/scidocs)

Citation mapping:
[https://www.connectedpapers.com/](https://www.connectedpapers.com/)

For the GUI
[https://arxiv.org/abs/1906.05996](https://arxiv.org/abs/1906.05996)
[https://medium.com/stellargraph/graph-machine-learning-and-ux-cdbf09edbc78](https://medium.com/stellargraph/graph-machine-learning-and-ux-cdbf09edbc78)

Ontology Learning:
[https://en.wikipedia.org/wiki/Ontology_learning](https://en.wikipedia.org/wiki/Ontology_learning)

TF-IDF with medical data:
[https://towardsdatascience.com/mining-and-classifying-medical-text-documents-1876462f73bc](https://towardsdatascience.com/mining-and-classifying-medical-text-documents-1876462f73bc)

Unsupervised Graph-based Learning
[https://medium.com/stellargraph/do-i-know-you-flexible-unsupervised-and-semi-supervised-graph-models-with-deep-graph-infomax-96fbfd63ec31](https://medium.com/stellargraph/do-i-know-you-flexible-unsupervised-and-semi-supervised-graph-models-with-deep-graph-infomax-96fbfd63ec31)
[https://medium.com/stellargraph](https://medium.com/stellargraph)

Start with scraping specialized journals (e.g., Journal of Neurophysiology).

Cluster papers into even more specialized topics based on weighted vectors of title, abstract, authors, and text-based parameters.

Use these clusters to find the most commonly cited papers (within the specialized topic of that cluster) in more generalized, higher-impact journals.

Find a way to extract facts/findings/results. This will rely on the extraction of semantics. You can probably bootstrap a lot of signal out of the citation patterns. Papers that are studying similar phenomena will be more likely to cite overlapping literature. You can train a neural network to start to recognize citation profiles and use them to form a prior of what the paper is studying. Then you can go in to the paper itself and try to learn more about the citation profile. There should be overlapping semantics as well.

Use unsupervised learning to cluster these findings into a map.

Create an interface that allows users to explore and/or search the map. For a particular family of facts, the user will get a cool interface that lists all of the findings, the paper and authors, and a link to the source. There needs to be an intuitive way to display and allow navigation through different levels of abstraction.

Abstraction is the key to this working. Can you represent the same information in a map through various levels of abstraction? Like zooming in and out of an actual map? The closer you zoom in, the more specific the topics/fact families become, and the smaller the number of hits for that family. The GUI that would be required for this sounds like a perfect opportunity to learn some JavaScript.

See:
[http://www.eigenfactor.org/projects/well-formed/map.html](http://www.eigenfactor.org/projects/well-formed/map.html)

Map Equation Team
- [https://github.com/mapequation/infomap](https://github.com/mapequation/infomap)
- [https://www.mapequation.org/code.html](https://www.mapequation.org/code.html)

CODE:
* Have the interface written in D3.js
- Currently, the basic unit of scientific discourse is the research paper. That's what we find when we search by topic (i.e., google scholar, pubmed, semantic scholar, etc). I argue that the basic unit of our scientific discourse should be the "finding": a statement about the world that is directly supported by a mathematical proof, a statistical analysis, an axiom, etc. How about "specimen" as a nod to [taxonomic rank](https://en.wikipedia.org/wiki/Taxonomic_rank) -- each finding or claim would be referred to as a specimen, and all of the findings that are essentially different measurements of the same phenomenon would be part of a species. And just as there is ambiguity and disagreement about classifications and boundaries in taxonomic ranking of living things, there would be a similar ambiguity built in to the way that people are allowed to structure their taxonomy.
- Each level of abstraction upward is a different "relationship". It answers increasingly more abstract levels of the question, "How is x related to y?"
- The app could send data back to a central server that tries to learn how people are structuring their taxonomies.
- Eventually, it could be a wiki-like structure where people can access, contribute to, and vote on a consensus-based taxonomy of scientific findings. Scientific authors would have an incentive to add their own findings and make sure they are represented.
- This is essentially a massive review paper and, eventually, potentially a massive meta-analysis of all scientific research. It would centralize, facilitate, streamline, and record the millions of debates, conversations, and replications that are currently occurring in ways that are not accessible to others, and in ways that are not saved in order to be built upon.
- The algorithm you develop should be iterative. It should mimic how humans build up their understanding of a topic through the hermeneutic circle. The current understanding becomes the background for the new understanding. There just has to be a strong external critic that keeps the learning process from running away into a local minimum.
- use NLP to digest large amounts of research. Talk to Titipat about this and his efforts to parse scientific papers. Use topic models to suggest groupings for scientific facts.

- for parsing scientific papers
	- **CODE**
		- [https://github.com/kermitt2/grobid](https://github.com/kermitt2/grobid)
		- [https://github.com/titipata/scipdf_parser](https://github.com/titipata/scipdf_parser)
		- [https://github.com/titipata/allennlp](https://github.com/titipata/allennlp)
		- [https://github.com/karpathy/researchpooler](https://github.com/karpathy/researchpooler)
		- [https://github.com/KordingLab/writing-style-in-science](https://github.com/KordingLab/writing-style-in-science)
- ScienceBeam - using computer vision to extract PDF data
	- [https://elifesciences.org/labs/5b56aff6/sciencebeam-using-computer-vision-to-extract-pdf-data](https://elifesciences.org/labs/5b56aff6/sciencebeam-using-computer-vision-to-extract-pdf-data)
- Claim extraction in biomedical publications using deep discourse model and transfer learning
		- [1907.00962.pdf](1907.00962.pdf)
		- [https://github.com/titipata/detecting-scientific-claim](https://github.com/titipata/detecting-scientific-claim)
- Parsing clinical text using the state-of-the-art deep learning based parsers: a systematic comparison
		- [s12911-019-0783-2.pdf](s12911-019-0783-2.pdf)
- Advances in deep parsing of scholarly paper content
	- [5224_paper12.pdf](5224_paper12.pdf)
- Extending biology models with deep NLP over scientific articles
	- [12615-57485-1-PB.pdf](12615-57485-1-PB.pdf)
- Extracting the science from scientific publications
	- [Extracting_the_science_from_scientific_p.pdf](Extracting_the_science_from_scientific_p.pdf)
- Using workflows to explore and optimise named entity recognition for chemistry
	- [journal.pone.0020181.pdf](journal.pone.0020181.pdf)
- Ontology population with deep learning-based NLP: a case study on the biomolecular network ontology
	- [1-s2.0-S1877050919313961-main.pdf](1-s2.0-S1877050919313961-main.pdf)
- Unsupervised word embeddings capture latent knowledge from materials science literature
	- [Tshitoyan_et_al-2019-Nature.pdf](Tshitoyan_et_al-2019-Nature.pdf)
- Extracting core claims from scientific articles
	- [1707.07678.pdf](1707.07678.pdf)
	- [https://github.com/TomJansen25/Extracting-Core-Claims/](https://github.com/TomJansen25/Extracting-Core-Claims/)
- Analyzing dynamics of Research by Extracting Key Aspects of Scientific Papers
	- [gupta-manning-ijcnlp11.pdf](gupta-manning-ijcnlp11.pdf)
- A method to automatically identify the results from journal articles
	- [2811c7f120290c32db4a82de6123ed04a7cc.pdf](2811c7f120290c32db4a82de6123ed04a7cc.pdf)
- Generating wikipedia by summarizing long sequences (Google Brain)
	- [1801.10198.pdf](1801.10198.pdf)