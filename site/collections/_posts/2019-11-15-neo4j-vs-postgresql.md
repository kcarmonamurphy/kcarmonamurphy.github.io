---
date: 2019-11-15 05:20:35 +0300
title: Neo4j vs PostgreSQL
description: Neo4j can be substantially faster for certain types of queries because of the benefits gained from index-free adjacency
tags: [neo4j, PostgreSQL]
image: '/images/airplane.jpg'
---

**Created:** November 2019

### Description

*Neo4j can be substantially faster for certain types of queries because of the benefits gained from index-free adjacency.*

**Example: Get the names of destination airports from all flights originating in Wyoming**

#### Cypher (Neo4j query language):

```
MATCH (hi:Airport {state: 'WY'})-[:HAS_DEPARTURE]->(fl:Flight)-[:FLIES_TO]->(ap:Airport)
```
<div style="margin-bottom: 40px"></div>

#### Postgres SQL:

```
RETURN DISTINCT ap.name
SELECT name from airports
JOIN flights ON (airports.iata = flights.destination_airport)
WHERE flights.origin_airport IN
(SELECT iata from airports WHERE airports.state = 'WY')
```

<div style="margin-bottom: 40px"></div>

| Attempt | 1 | 2 | 3 | Average | Logo |
| ----------- | ----------- | ----------- | ----------- | ----------- | ---|
| **Neo4j** | 0.29222047s | 0.34756797s | 0.30003158s |  **0.32918392s** |  ![neo4j](/images/neo4j.png) |
| **PostgreSQL** | 2.32982001s | 2.14832110s | 2.39080437s | **2.29873976s** | ![PostgreSQL](/images/postgresql.jpg) |

### Context

This performance comparison was completed for the final project of my SCS 3252:017 Big Data Management Systems & Tools course (University of Toronto). 

There is a PDF and Jupyter notebook investigating how Neo4j can outperform PostgreSQL for large interconnected datasets. See below:

### Technology Stack
- neo4j
- PostgreSQL
- jupyter notebooks
- Google Colab

### Links
- **Project PDF Document:** [Comparing Neo4j with PostgreSQL ⎘](https://github.com/kcarmonamurphy/flightly/blob/master/Big%20Data%20Course_%20Comparing%20Neo4j%20with%20PostgreSQL.pdf){:target="_blank"}
- **Jupyter Notebook:** [Flightly Comparing Neo4j and PostgreSQL.ipynb
 ⎘](https://github.com/kcarmonamurphy/flightly/blob/master/Flightly%20Comparing%20Neo4j%20and%20PostgreSQL.ipynb){:target="_blank"}
- **Github:** [Github ⎘](https://github.com/kcarmonamurphy/flightly){:target="_blank"}


