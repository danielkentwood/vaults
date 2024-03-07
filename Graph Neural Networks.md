# Graph Neural Networks
[[Networks]]


# Resources
## Articles
* How powerful are graph neural networks?
	* paper: https://arxiv.org/pdf/1810.00826.pdf
	* This paper shows that most GNN variants cannot learn to distinguish certain simple graph structures (e.g., a triangle). They propose an architecture that is, at the time, provably the most expressive GNN. 
	* For supplemental thoughts on the limitations of GNNs (particularly the popular Weisfeiler-Lehman approaches) and how to potentially overcome those limitations, here's Michael Bronstein: https://towardsdatascience.com/graph-neural-networks-beyond-weisfeiler-lehman-and-vanilla-message-passing-bc8605fa59a
* DISTILL.PUB!!!
	* https://distill.pub/2021/gnn-intro/
	* https://distill.pub/2021/understanding-gnns/ 
	* distill.pub template: https://github.com/distillpub/template
* Graph Neural Networks: A review of methods and applications: 
	* paper: https://arxiv.org/pdf/1812.08434.pdf
* Edge Proposal Sets for Link Prediction
	* paper: https://arxiv.org/pdf/2106.15810.pdf
	* This paper shows link prediction accuracy can be significantly boosted by adding a preprocessing step where you add a set of edges (a "proposal set") that generally align with the structure of the graph.

## Videos
* #### Why would you use graphs for machine learning data? 
	* https://www.youtube.com/watch?v=mu1Inz3ltlo
	* ##### (1) Because graphs capture information that is otherwise hard to model
		* Modern deep learning techniques are designed to deal with sequences and grids. But many real-world systems can be modelled as graphs. 
		* Graphs model entities and the connections between them, and therefore they contain topological information about the network. 
		* Take the example of a map of airports: How else can we model the connections between airports? Modeling the data as a graph is likely the most compressed way to represent the connections (i.e., edges).
		* What kind of information is difficult to represent outside of a graph? 
			* Edge type: weighted vs binary
			* Edge directionality: directed vs undirected
			* Features: node-based, edge-based
			* Network analytics: e.g., centrality (degree centrality, eigenvector centrality, betweenness centrality, closeness centrality), community detection (clustering, modularity, size distribution, growth, stability), spreading phenomena, robustness, etc.
			* Others: multi-graphs, hypergraphs, complex networks
			* Temporal aspects of all of the above
		* 
	* ##### (2) Because if data are best represented as a graph, the model architecture should be optimized for it
		* Data efficiency: Why not just use MLP or attention and learn "everything" end-to-end? MLPs are "universal function approximators" -- in theory, they can learn any function shape if you give them enough data, layers, etc.
			* But we can train more efficiently (i.e., require less training data) if we change the structure of the model. The point behind deep learning model architectures is that you can modify your architecture in order to "fit" the structure of the data you are looking at. This is known as a "relational inductive bias".
				* For example, convolutional neural networks take advantage of the structure of image data (which are basically special cases of graphs). Recurrent neural networks take advantage of temporal information in certain ways (e.g., build up "memory"). 
				* GNNs are neural network architectures that are optimizing for the unique structure of the data in graphs. 
* Geometric DL course (Bronstein): https://www.youtube.com/watch?v=PtA0lg_e5nA&list=PLn2-dEmQeTfQ8YVuHBOvAhUlnIPYxkeu3
* Intro to GNNs - Models and applications (Microsoft Research): https://www.youtube.com/watch?v=zCEYiCxrL_0
* Zak Jost interview: https://www.youtube.com/watch?v=jAGIuobLp60&t=1423s

## Blog posts
* https://neptune.ai/blog/graph-neural-network-and-some-of-gnn-applications
* https://towardsdatascience.com/a-gentle-introduction-to-graph-neural-network-basics-deepwalk-and-graphsage-db5d540d50b3
* https://towardsdatascience.com/why-graph-modeling-frameworks-are-the-future-of-unsupervised-learning-2092b089caff
* All google AI posts on graphs: https://www.google.com/search?q=site%3Aai.googleblog.com%20graphs

## Platforms and Repos
* https://ogb.stanford.edu/
* https://github.com/divelab/DIG

## Tutorials
* https://docs.dgl.ai/tutorials/blitz/index.html
* https://www.kaggle.com/elmahy/code
* https://github.com/turi-code/tutorials/blob/master/notebooks/link_prediction.ipynb
* https://cnvrg.io/graph-neural-networks/
* https://neo4j.com/docs/graph-data-science/current/
* Link prediction in large-scale networks (not deep learning): https://github.com/Cdiscount/IT-Blog/tree/master/samples/DataScience/link-prediction-in-large-scale-networks

## Books
* Graph Representation Learning (Hamilton, 2020)
	* pdf: https://www.cs.mcgill.ca/~wlh/grl_book/files/GRL_Book.pdf
	* This is a math-heavy intro to GNNs.

## Courses:
* Stanford CS224W (Machine Learning with Graphs): http://web.stanford.edu/class/cs224w/

## Libraries
* Deep Graph Library: https://www.dgl.ai/
* PyTorch Geometric Temporal: https://pytorch-geometric-temporal.readthedocs.io/en/latest/index.html
	* paper: https://arxiv.org/pdf/2104.07788.pdf
	* video: https://www.youtube.com/watch?v=Rws9mf1aWUs
* Spektral (based on Keras/Tensorflow 2 API): https://graphneural.network/


## People
* Michael Bronstein
	* https://michael-bronstein.medium.com/
	* https://scholar.google.com/citations?user=UU3N6-UAAAAJ&hl=en
	* Geometric DL; Oxford; GraphML Research @ Twitter