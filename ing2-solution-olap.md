---
title: ing2-solution-olap
tags: [olap, pm, solution]
created: '2020-04-03T15:57:07.832Z'
modified: '2020-07-14T10:24:59.817Z'
---

# ing2-solution-olap

## faq

- Apache Druid vs Elasticsearch
  - Elasticsearch is a search system based on Apache Lucene. It provides full text search for schema-free documents and provides access to raw event level data. Elasticsearch is increasingly adding more support for analytics and aggregations. Some members of the community have pointed out the resource requirements for data ingestion and aggregation in Elasticsearch is much higher than those of Druid
  - Elasticsearch also does not support data summarization/roll-up at ingestion time, which can compact the data that needs to be stored up to 100x with real-world data sets. This leads to Elasticsearch having greater storage requirements.
  - Druid focuses on OLAP work flows. Druid is optimized for high performance (fast aggregation and ingestion) at low cost, and supports a wide range of analytic operations. Druid has some basic search support for structured event data, but does not support full text search. Druid also does not support completely unstructured data. Measures must be defined in a Druid schema such that summarization/roll-up can be done.
  - ref
    - https://druid.apache.org/docs/latest/comparisons/druid-vs-elasticsearch.html

## druid

## summary

- ElasticSearch is a great alternative to a cube, we use it to build reports with pivot-like functionality  
  - One huge benefit is that with a cube you need to know what dimensions you want to create reports on. 
  - With ES you just shove in more and more data and figure out later how you want to report on it.
- At our company we regularly have data go through the following life cycle.
  - record is written to SQL
  - primary key from SQL is written to RabbitMQ
  - we respond back to the customer very quickly
  - When Rabbit has time, it uses the primary key to gather up all the data we want to report on
  - That data is written to ElasticSearch
- A word of advice: If you think you might want to report on it, get it from the beginning. 
  - Inserting 1M rows into ES is very easy, updating 1M rows is a bigger pain.
- ref
  - https://stackoverflow.com/questions/35513249/reasons-against-using-elasticsearch-as-an-olap-cube
