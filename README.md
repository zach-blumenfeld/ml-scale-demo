# GDS Webinar Demo: Graph Data Science for Really Big Data

This repo contains demo code from the 2022 GDS February Webinar  - "Graph Data Science for Really Big Data". The exact pattern here may vary slightly from what you have seen in the webinar, most of the commands have been placed in notebooks for example, but the overall steps should be the same. 

The purpose of this demo is to explore engineering graph features using Neo4j and the [Graph Data Science (GDS) Library](https://neo4j.com/docs/graph-data-science/current/) on a larger dataset to see if we can improve accuracy for a classification problem. 

The graph used here is the [MAG240M OGB Large-Scale-Challenge Graph](https://ogb.stanford.edu/docs/lsc/mag240m/).  It is a heterogeneous academic paper graph that contains around 240 Million Nodes and 1.7 Billion Relationships.  

## Demo Outline and Notebooks Parts

This demo walks through multiple steps including running a reference model before using graph, formatting and importing data into Neo4j, analyzing the graph and engineering graph features with GDS, and exporting data to re-run a model with those graph features. 

The demo here is ultimately split up into 8 parts, 7 of which are ipython notebooks. Hopefully the file names are descriptive as to what they cover

- Parts 1 and 2 focus on understanding the data and running a classification model with available features before leveraging Neo4j/GDS/graph
  - `part1-get-data-and-non-graph-modeling-prep.ipynb`
  - `part2-simple-non-graph-model-and-pca.ipynb`

- Parts 3-5 are focused on pre-formatting the data and importing into graph
  - `part3-prepare-papers-for-import.ipynb`
  - `part4-prepare-authors-and-inst-for-import.ipynb`
  - `part5-admin-import.md`

- Part 6 and 7 focus on work in Neo4j and GDS. Part 6 is mostly inspecting the graph and demoing native projections and the WCC algorithm. Part 7 is focused on actually generating and exporting graph features (FastRP Node Embeddings)
    - `part6-analysis-in-neo4j-gds.ipynb`
    - `part7-graph-feature-engineering-in-gds.ipynb`

- Finally Part 8 re-runs the classification model with the graph features (FastRP Node Embeddings). In this very rough exploratory first pass we get an ~9% point increase in classification accuracy.
  - `part8-graph-feature-model.ipynb`



## Prerequisites & Environment for Running the Demo 

### Software Versions
- Neo4j = Enterprise Edition 4.4.3
- GDS = Enterprise Edition 1.8.3
- APOC = 4.4.0.3
- Python = 3.9.7

Important Note: Enterprise (as opposed to Community) Editions were used for both the Neo4j Database and GDS library in this demo. The use of GDS Enterprise, in particular, provides high-concurrency and optimized in-memory compression which are not available in Community Edition and key to performance at these scales.

### Instance
This demo was run on a single AWS ec2 x1.16xlarge instance (64 vCPUs, 976 GB Memory).

### Neo4j Configuration
I tweaked a few things but the below are the most critical which you can update in the neo4j settings/configuration (a.k.a `neo4j.conf`)

- `dbms.memory.heap.max_size=760G` 
- `gds.export.location=/data/neo-export` # or set to whatever directory you would like data exports from Neo4j to go

Depending on your environment and specific needs you may need to tune this and other configuration like min heap size, pagecache, etc. For more details on optimizing Neo4j configuration for data science and analytics at scale I recommend looking into the [Graph Data Science Configuration Guide](https://neo4j.com/whitepapers/graph-data-science-configuration-guide/). 


## Future Experimentation & Improvements

This demo was just a rough first pass to explore what is possible. There are many ways to improve upon this analysis! Here are just a few areas to experiment:

1. Improved tuning of FastRP node Embeddings
2. Inclusion of more graph features
3. Streamlined data formatting and ETL
4. Better-tuned and/or more sophisticated classification models and frameworks
5. Exploration of Semi-supervised transductive approaches to label the rest of the papers, such as Label Propagation Algorithm (LPA) or K-Nearest Neighbor (KNN)