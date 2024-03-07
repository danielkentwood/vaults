# causal discovery

##### Metadata
created:: 2023-12-04 10:57
modified:: <%+ tp.file.last_modified_date() %>
mode: #mode/gnosis
kind:: #zettel 
status:: #status/seed
parent:: [[causal inference]]
***


### Notes from Aleksander Molak
Sources:
* [Causal discovery in Python - Aleksander Molak, Lingaro | GHOST Day: AMLC 2022](https://www.youtube.com/watch?v=qfRLlLnoA38)
* [00 - Causal discovery II Notes 1.ipynb](https://github.com/AlxndrMlk/causality/blob/main/00%20-%20Causal%20discovery%20II%20Notes%201.ipynb)
NOTE: Some of the content below is copy-pasted. Attribute when appropriate if you use it. 

#### 3 main families of causal discovery methods:
1. Constraint-based
	1. Leverage the graph independence structure
	2. important assumption: independence --> if there is independence in the data, it maps to the graph
	3. Typically, these methods return a Markov Equivalence Class (MEC), not necessarily a unique solution
	4. examples: 
		1. PC algorithm
			1. Starting with a fully connected graph, performs a series of steps to remove edges based on graph independence structure, and tries to orient as many edges as possible
		2. FCI (fast causal inference)
			1. Generalization of PC that tolerates and sometimes discovers unknown confounders
2. Score-based: 
	1. They try to generate many graphs and then evaluate them on their fit to the data
	2. finding optimal graph is NP-hard, so they use heuristics
	3. example: 
		1. GES (greedy equivalence search)
			1. starts with an empty graph, adds edges and then performs pruning. At each step graph-data fit is measured using a score (e.g. BIC or Z-score; Glymour et al., 2019).
3. Functional: 
	1. Leverage statistical properties of variable and noise distributions to find asymmetries and orient the edges in the graph
	2. Typically, these return a unique graph (not a MEC like constraint-based methods)
	3. functional causal model (FCM): $Y = f(X,\epsilon, \theta_1)$ 
		1. effect Y is a function $f$ of direct causes $X$ and some unmeasurable noise $\epsilon$ (and $\theta$ is a parameter set involved in $f$). 
		2. An important assumption is that the transformation $(X,\epsilon) \rightarrow (X, Y)$ is invertible.
		3. Using FCM we try to find the causal asymmetry when fitting two FCMs: $X \rightarrow Y$ and $Y \rightarrow X$, and then we check which direction results in the independence of the noise term $\epsilon$. NOTE: it has been shown that, without additional assumptions, the causal direction is non-identifiable [(Zhang et al., 2015)](https://ei.is.mpg.de/uploads_file/attachment/attachment/2/ACM_Zhang14.pdf)
	4. example: 
		1. LiNGAM (linear non-gaussian acyclic model)
		2. PNL (post-linear model)
		3. LinGAM estimation: Two-step algorithm and FASK

There are other methods:
- Hybrid
	- GFCI
		- a combination of GES and FCI, where GES generates a graph and FCI prunes it. Some simulation studies demonstrated that **GFCI** is more accurate in retrieving the true causal structure than pure FCI.
- Reinforcement-learning based methods
- End-to-end causal discovery and inference methods





## External Resources
### Blog articles
- [Causal Python — Level Up Your Causal Discovery Skills in Python](https://towardsdatascience.com/beyond-the-basics-level-up-your-causal-discovery-skills-in-python-now-2023-cabe0b938715)

### Research articles
- [Use of Prior Knowledge to Discover Causal Additive Models with Unobserved Variables and its Application to Time Series Data](https://arxiv.org/pdf/2401.07231.pdf)
- Review: [Review of Causal Discovery Methods Based on Graphical Models](https://www.frontiersin.org/articles/10.3389/fgene.2019.00524/full)
- [Causal discovery in high-dimensional, multicollinear datasets](https://www.frontiersin.org/articles/10.3389/fepid.2022.899655/full)
- 

### Youtube
- [Causal discovery in Python - Aleksander Molak, Lingaro | GHOST Day: AMLC 2022](https://www.youtube.com/watch?v=qfRLlLnoA38)
- [Causal inference, causal discovery, and machine learning with Jakob Runge](https://www.youtube.com/watch?v=R5JMeEy9koA)

### Github
- Aleksander Molak
	- Personal repo: https://github.com/AlxndrMlk/causality/tree/main
	- Packt repo for his book: https://github.com/PacktPublishing/Causal-Inference-and-Discovery-in-Python

### Tools
CausalLens
- [https://github.com/causalens](https://protect-usb.mimecast.com/s/iBJQCrgWNnT23MApNZJi7InV-?domain=github.com "https://protect-usb.mimecast.com/s/iBJQCrgWNnT23MApNZJi7InV-?domain=github.com")  

suite of causal discovery/inference tools: 
- [https://nips.cc/virtual/2022/63879](https://protect-usb.mimecast.com/s/VypUCvm67ruA01WGB8VFXiTQo?domain=nips.cc "https://protect-usb.mimecast.com/s/VypUCvm67ruA01WGB8VFXiTQo?domain=nips.cc")  
- [https://github.com/py-why](https://protect-usb.mimecast.com/s/GvDACwn68vsyZ6L7Oxrc925Ee?domain=github.com "https://protect-usb.mimecast.com/s/GvDACwn68vsyZ6L7Oxrc925Ee?domain=github.com")
- [https://github.com/microsoft/causica](https://protect-usb.mimecast.com/s/Jf47CxoWNwcxq8JyGvNHw5ym0?domain=github.com "https://protect-usb.mimecast.com/s/Jf47CxoWNwcxq8JyGvNHw5ym0?domain=github.com")  
- [https://github.com/microsoft/showwhy](https://protect-usb.mimecast.com/s/aVLnCypWOxhLmDNgjoVhNGYcR?domain=github.com "https://protect-usb.mimecast.com/s/aVLnCypWOxhLmDNgjoVhNGYcR?domain=github.com")  

### Other
Center for causal discovery: 
- [https://bd2kccd.github.io/docs/](https://protect-usb.mimecast.com/s/4ubsCzqgNyF4NDR3PqVuwJBFj?domain=bd2kccd.github.io/ "https://protect-usb.mimecast.com/s/4ubsCzqgNyF4NDR3PqVuwJBFj?domain=bd2kccd.github.io/")


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

