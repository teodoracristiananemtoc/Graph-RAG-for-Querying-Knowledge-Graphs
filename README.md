# Graph-RAG-for-Querying-Knowledge-Graphs
This repository contains the source code and experimental details for Graph RAG for Querying Knowledge Graphs.
Unlike the standard RAG approach, which relies on textual input, Graph RAG replaces it with a Knowledge Graph. For the current experiment, the step of constructing the KG within the Graph RAG process is substituted with an existing reference KG dataset provided by Pykeen https://pykeen.readthedocs.io/en/stable/api/pykeen.datasets.UMLS.html

A series of standard query typologies for KGs have been tested in this setup, examining how Large Language Models (LLMs) can respond to these queries in natural language. The results returned by the LLMs are compared to the SPARQL standard, measuring performance metrics.

LLMs utilized: : Mixtral-8x7B-Instruct-v0.1, GPT-3.5-Turbo, and GPT-4o 

Graph RAG: Microsoft  https://github.com/microsoft/graphrag

Query Taxonomy:

1)Reading the object for a known relationship with a known subject
SELECT ?object WHERE {@node @predicate ?object.}

2)Reading the subject for a known relationship with a known object
SELECT ?subject WHERE {?subject @predicate @node.}

3)Reading the entity(ies) related to a known node through a known relationship
SELECT ?ent WHERE {{@node @relationship ?ent.} UNION {?ent @relationship @node.}}

4)Reading the relationship(s) that directly connect two known entities
SELECT ?predicate WHERE {{@node1 ?predicate @node2.} UNION {@node2 ?predicate @node1.}}

5)Discovering all relationships of an entity and their targets
SELECT ?predicate ?target WHERE {@node ?predicate ?target.}

6)Return pairs of nodes connected by a relationship
SELECT ?source ?target WHERE {?source @predicate ?target.} UNION {?target @predicate ?source.}

7)Discovering all triples that involve an entity
DESCRIBE @x

To reproduce the experiments, OpenAI and Hugging Face prerequisites are mandatory, as well as storing the dataset in a dedicated Graph DB environment.

