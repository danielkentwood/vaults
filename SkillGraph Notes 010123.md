# SkillGraph Notes 010123
created:: 2023-01-03 12:23
modified:: <%+ tp.file.last_modified_date() %>
mode: #mode/gnosis
kind:: #zettel 
status:: #status/seed
parent:: [[π SkillGraph]]
***

## External Resources

### SkillGraph notes
Create a skeleton website
- Use webflow to get started
https://webflow.com/design/higher-1bf40a

### Skill ontology resources
##### MIT
- [MIT SkillScape](https://sites.pitt.edu/~mrfrank/skillscape/#/landing)
##### World Economic Forum 
- [The Reskilling Revolution](https://initiatives.weforum.org/reskilling-revolution/home)
- [Strategic intelligence interactive visualization](https://intelligence.weforum.org/topics/a1Gb0000000LPFfEAO?utm_source=ed75b345-f6ec-4412-8191-31e01ec50155&utm_medium=InSIW&utm_campaign=https://initiatives.weforum.org/&utm_content=iframe_implementation)
- [Global skills taxonomy](https://www1.reskillingrevolution2030.org/skills-taxonomy/index.html)
- [Defining Education 4.0: A Taxonomy for the Future of Learning](https://www.weforum.org/whitepapers/defining-education-4-0-a-taxonomy-for-the-future-of-learning)
- 

OLD LINKS (currently broken)
- [Strategies for the New Economy: Skills as the Currency of the Labour Market](https://www.reskillingrevolution2030.org/reskillingrevolution/wp-content/uploads/2020/05/WEF_2019_Strategies_for_the_New_Economy_Skills.pdf)
- [Upskilling for Shared Prosperity](https://www.reskillingrevolution2030.org/reskillingrevolution/wp-content/uploads/2021/01/127701_PwC_Upskilling_for_Shared_Prosperity_Final.pdf)
- [Building a Common Language for Skills at Work A Global Taxonomy](https://www.reskillingrevolution2030.org/reskillingrevolution/wp-content/uploads/2021/01/Skills-Taxonomy_Final-1.pdf)
	- [Interactive skills taxonomy](https://www1.reskillingrevolution2030.org/skills-taxonomy/index.html)
- [Towards a Reskilling Revolution: Industry-Led Action for the Future of Work](https://www.reskillingrevolution2030.org/reskillingrevolution/wp-content/uploads/2020/05/WEF_Towards_a_Reskilling_Revolution.pdf)
##### Government
- https://www.bls.gov/ooh/occupation-finder.htm
- https://esco.ec.europa.eu/en/classification/skill_main
	- https://esco.ec.europa.eu/en/about-esco/data-science-and-esco
- https://www.onetcenter.org/database.html
	- https://esco.ec.europa.eu/en/about-esco/data-science-and-esco/crosswalk-between-esco-and-onet
##### Companies
- https://lightcast.io/open-skills
- https://www.thezeit.co/
- https://linkedin.github.io/career-explorer/

### Visualization resources
##### SciencesPo MediaLab
* https://medialab.sciencespo.fr/en/tools/
* https://www.sigmajs.org/
	* https://github.com/jacomyal/sigma.js
	* https://github.com/medialab/ipysigma
	* examples:
		* massive graph with clusters: https://codesandbox.io/s/github/jacomyal/sigma.js/tree/main/examples/large-graphs?file=/index.ts
		* node and edge reducers for interactivity: https://codesandbox.io/s/github/jacomyal/sigma.js/tree/main/examples/use-reducers
		* Cluster labels: https://codesandbox.io/s/github/jacomyal/sigma.js/tree/main/examples/clusters-labels
		* hover and click events: https://codesandbox.io/s/github/jacomyal/sigma.js/tree/main/examples/events
		* embed graph in html website, and graph allows node manipulation and adding new nodes: https://codesandbox.io/s/github/jacomyal/sigma.js/tree/main/examples/mouse-manipulations
* https://medialab.sciencespo.fr/en/tools/seealsology/
* https://medialab.sciencespo.fr/en/tools/graphology/
##### Cytoscape
- https://js.cytoscape.org/
- https://github.com/cytoscape/cytoscape.js
- https://medium.com/analytics-vidhya/javascript-graph-visualization-using-cytoscape-js-e741556afb96
* https://stackoverflow.com/questions/41506664/hide-and-show-child-nodes-on-node-tap-cytoscape
	- https://jsfiddle.net/sLko7pcu/
##### Vis.js
- Another powerful library, based on Canvas, for visualizing network data
- https://visjs.org/
##### d3fc.io
- provides components for drawing d3 elements with WebGL
- https://d3fc.io/
- https://blog.scottlogic.com/2020/05/01/rendering-one-million-points-with-d3.html
##### PIXI.js
- a powerful 2d drawing library that allows you to render d3 (and other JS drawing instructions) in WebGL or Canvas
- https://graphaware.com/visualization/2019/09/05/scale-up-your-d3-graph-visualisation-webgl-canvas-with-pixi-js.html
##### 3d-force-graph
- a library for visualizing force-directed graphs in 3D with three.js and WebGL
- https://github.com/vasturiano/3d-force-graph


### Internal resources
[[ç Visualize graphs with sigma.js]]
[[ç Visualize large graphs with Plotly]]


### Gamification ideas
##### Farming/Cultivation
- Farming analogy. Have a visualization of a tree/plant, and it gets bigger as the user connects more skills. Size is dependent on number of nodes.
- Health of the plant is dependent on amount/recency of validation. Are you continuing to use this knowledge/skill? Or is it something that is "withering on the vine"?
- You have a size score and a health score, both for each branch and in aggregate.
##### Cards/Rare items
* Skill Flows will be scored by how rare they are and how lucrative they are. 
* Archetypal Skill Flows will be encapsulated in cards -- we can use diffusion models to programatically generate card images at scale. 

### Validation
- Each form of validation pushes you to show/create some kind of artifact in the real world that demonstrates your skill.