# SkillGraph graph ontologies
created:: 2023-01-17 14:10
modified:: <%+ tp.file.last_modified_date() %>
mode: #mode/gnosis
kind:: #zettel 
status:: #status/seed
parent:: [[π SkillGraph]]
***

# Ontology
##### 1. Nodes
The node entities should reflect whether knowledge of that node is _practical_ (i.e., a series of actions) or _conceptual_ (i.e., linking of concepts). Focus on the compositionality of skill. 

###### Node types:
* discipline: e.g., mathematics, topology
* formula: a standardized version of an important formula
* theorem: 
* algorithm: 
* technique: 
* platform: 
* coding_language: 
* package: 
* framework: 
* resource: 
* technology: 
* activity: 
* competency:

###### Edge types:
* sub-discipline
* used for:
* version of: 
* 

###### Validation layer
* certification
* degree
* endorsement
* artifact: link to an artifact that proves the person has the linked skill (e.g., repository, portfolio item, publication, etc.)

The connections from a given node should be weighted by how often the two nodes co-occur in source texts. The weightings can be normalized in several ways: 
* over the entire graph
* over all immediate neighbor nodes
* over all immediate neighbor nodes of a particular class

For each node, we should have resources to learn more about that link. The resources are scraped from several sources (moocs, wikipedia, blogs, youtube, other free learning platforms, etc). The resources are ranked by an algorithm that checks which nodes are most important to the anchor node (in the graph), extracting a weighted graph from the entities in each source, and then comparing these to the anchor graph. This provides a "topic coverage" score. We could come up with other metrics as well. 

##### 2. Edges
* is_subclass_of
* uses_theorem
* uses_algorithm
* uses_technique
* uses_platform
* uses_language
* uses_package

#### Python and/or JS classes
* User
* SkillNode
* SkillBlock
* SkillFlow
* SkillTree


# Notes

* Skills should always be contextualized. What was the need? What was the outcome? 
	* There should be a graph of needs
		* For example, signal separation <-- multicellular electrophysiology <-- cortical electrophysiology <-- neurobiology
	* There should be a graph of outcomes. 
	* These outcomes should be abstract enough to avoid numeric specificity. At most, we want to know which metric or data type (e.g., voltage), but not the amount of voltage (e.g., 20 mV)


# External
## Other ontology/KG examples
* [Computer Science Ontology (CSO)](https://cso.kmi.open.ac.uk/topics/computer_science)
* [Data Science Ontology](https://github.com/IBM/datascienceontology)