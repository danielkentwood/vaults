# Creating a DDL

For reference: https://docs.tigergraph.com/gsql-ref/current/ddl-and-loading/modifying-a-graph-schema

We will be using GSQL to create a schema for our graph. This is a three-step process:
1. Define the classes of nodes (TigerGraph calles them "vertices") our graph can have
2. Define the edges that can exist between nodes
3. Create the graph schema

## Define vertices
Here is an example where we define two vertex classes:
```
CREATE VERTEX _Member(PRIMARY_ID individual_id STRING, birthday DATETIME, maritalStatus STRING) WITH primary_id_as_attribute="true"

CREATE VERTEX _Conditions(PRIMARY_ID icd_cd STRING, description STRING) WITH primary_id_as_attribute="true"
```

**Notes:**
* Each vertex class requires a PRIMARY_ID attribute, denoting a unique vertex in this class. If we set `primary_id_as_attribute` to "true", the PRIMARY_ID will be included in the database and we can use it in a query. Otherwise, it will only be stored as a mapping in the graph storage engine (see [system overview](https://docs.tigergraph.com/tigergraph-server/current/intro/internal-architecture#_system_overview)).
* You can add an arbitrary number of other attributes for each vertex class. 
* Eligible [attribute types](https://docs.tigergraph.com/gsql-ref/current/querying/data-types#_vertex_and_edge_attribute_types) for vertices (and edges) are: 
	* INT
	* UINT
	* FLOAT
	* DOUBLE
	* STRING
	* STRING COMPRESS
	* BOOL
	* SET< type >
	* LIST< type >
	* MAP<key_type, value_type> 
	* DATETIME


## Define edges
Here is an example where we define an edge between two nodes:
```
CREATE UNDIRECTED EDGE _MEMBER_HAS_CONDITION(FROM _Conditions, TO _Member, startDate DATETIME)
```

**Notes:** 
* In this example, we are creating an undirected edge, so the FROM and TO assignments are interchangeable. If we were creating a directed edge, we would need specify the direction with the FROM and TO assignments. 
* Edges can also have an arbitrary number of attributes assigned to them. In this case, we want to know when the condition was diagnosed. 

## Create the graph




