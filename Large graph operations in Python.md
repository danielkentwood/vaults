# Large graph operations in Python
created:: 2022-11-06 13:20
modified:: <%+ tp.file.last_modified_date() %>
mode: #mode/gnosis
kind:: #zettel 
status:: #status/seed
***
## Storage
##### Memgraph
* Memgraph is a persistent in-memory graph database that [integrates with networkx](https://memgraph.com/memgraph-for-networkx). There is a free tier that is fully functional. It is written in C++, so it is fast and can handle massive graphs. 
* https://networkx.guide/faq/
* https://memgraph.com/benchmark -- it outperforms Neo4j in some important tasks. 
* https://github.com/memgraph/memgraph -- it is open source.
* Free playground: https://playground.memgraph.com/
* Memgraph is supported by LangChain! https://dev.to/memgraph/exciting-news-langchain-now-supports-memgraph-4mc8


***
## Analytics/Operations

What are the options for working with massive [[Networks]] in [[ç Python]]?

##### PyTorch Geometric
* [This medium article](https://towardsdatascience.com/sampling-large-graphs-in-pytorch-geometric-97a6119c41f9) mentions two algorithms for graph sampling to handle [[graph embeddings]] learning over large graphs in PyTorch Geometric. 
	* NeighborSampler: implements [[GraphSAGE]] over node neighborhoods instead of the full graph.
	* GraphSaintSampler: samples subgraphs of the original graph before learning embeddings.  

##### Apache Spark
* Spark is an attractive option because of the way that it interacts with distributed representations in parallel. 
* There are two [[PySpark]] options provided by [[Apache Spark]]:
	* [GraphFrames](http://graphframes.github.io/graphframes/docs/_site/quick-start.html) 
		* uses the Spark DataFrames framework
		* [Medium article on using GraphFrames in Jupyter](https://towardsdatascience.com/graphframes-in-jupyter-a-practical-guide-9b3b346cebc5#:~:text=The%20functionality%20of%20GraphFrames%20and,browsing%20through%20the%20API%20documentation.)
		* [Running GraphFrames with PySpark on Google Dataproc](https://stackoverflow.com/questions/58222729/pyspark-exception-with-graphframes)
			* Google Dataproc is a GCP service for running Spark and many other open-source tools. 
	* [GraphX](https://spark.apache.org/docs/latest/graphx-programming-guide.html) 
		* uses Spark RDDs (resilient distributed dataset)





***
## Visualization
##### In Python
[[ç Visualize large graphs with Plotly]]

DataMapPlot
* [linkedin post](https://www.linkedin.com/posts/leland-mcinnes-406233103_a-major-update-for-datamapplot-adds-interactive-activity-7167915698223038464-q9Mu?utm_source=share&utm_medium=member_desktop)
* examples:
	* [https://lnkd.in/g94MGBZV](https://lnkd.in/g94MGBZV)  
	- [https://lnkd.in/gS948CVn](https://lnkd.in/gS948CVn)  
	- [https://lnkd.in/gwmM8u_a](https://lnkd.in/gwmM8u_a)  
	- [https://lnkd.in/gBCrzvCJ](https://lnkd.in/gBCrzvCJ)
- Docs: [https://lnkd.in/gyCY4U4f](https://lnkd.in/gyCY4U4f)  
- Code: [https://lnkd.in/gxvQhsbc](https://lnkd.in/gxvQhsbc)  
- PyPI: pip install datamapplot  
- conda: conda install -c conda-forge datamapplot
