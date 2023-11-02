---
title: toc-lib-olap4j
tags: [lib, olap, olap4j, toc]
created: 2020-07-13T03:03:54.791Z
modified: 2020-10-22T06:50:47.668Z
---

# toc-lib-olap4j

# guide

# olap4j
- CBoard /2.9kStar/apache2/202104/js+java/angularjs/inactive
  - https://github.com/TuiQiao/CBoard
  - https://tuiqiao.github.io/CBoardDoc/#/
  - An easy to use, self-service open BI reporting and BI dashboard platform
- davinci /4.5kStar/Apache2/202111/ts/java/inactive
  - https://github.com/edp963/davinci
  - https://edp963.github.io/davinci
  - Davinci is a DVsaaS (Data Visualization as a Service) Platform
  - https://github.com/running-elephant/datart /java/echarts/inactive
    - datart 是新一代数据可视化开放平台，支持各类企业数据可视化场景需求，如创建和使用报表、仪表板和大屏，进行可视化数据分析，构建可视化数据应用等。
    - 由原 davinci 主创团队出品，datart 更加开放
- poli /1.7kStar/MIT/202005/java/inactive
  - https://github.com/shzlw/poli
  - https://shzlw.github.io/poli
  - An easy-to-use BI server built for SQL lovers. Power data analysis in SQL and gain faster business insights.
- datagear /166Star/LGPLv3/202012
  - https://github.com/datageartech/datagear
  - http://www.datagear.tech/
  - 源免费的数据可视化分析平台，使用Java语言开发，采用浏览器/服务器架构，支持SQL、CSV、Excel、HTTP接口、JSON等多种数据源， 
  - 主要功能包括数据管理、SQL工作台、数据导入/导出、数据集管理、图表管理、看板管理等。
- https://github.com/activeviam/autopivot /apache2/202304/java
  - https://www.activeviam.com/
  - AutoPivot is a standalone application for online analysis (OLAP) of CSV files.
  - automatically creates in-memory OLAP cubes from CSV files, that you can explore from Excel, Tableau or using the embedded Atoti UI web frontend
  - 依赖spring-boot、activeui

- https://github.com/dataease/dataease
  - 开源的数据可视化分析工具
  - DataEase 支持丰富的数据源连接，能够通过拖拉拽方式快速制作图表，并可以方便的与他人分享。
- https://github.com/helicalinsight/helicalinsight
  - https://helicalinsight.github.io/helicalinsight/#/
  - Open Source Business Intelligence framework which can help you derive insights out of multiple datasources. 
  - it comes with a unique Workflow rule engine
  - XML driven Workflow
- https://github.com/apache/zeppelin
  - Web-based notebook that enables data-driven, interactive data analytics and collaborative documents with SQL, Scala and more.

- https://github.com/xianfengyi/MixQuery
  - 在实际的业务场景中，不同特点的数据会存储到不同的存储引擎里。 然而异构的存储和数据源，却给分析查询带来了挑战，比如跨源查询，以及跨集群查询将变得困难
  - 因此，需要一款支持混合查询的引擎。
  - 希望更多的以学习和探索的视角，去开发一个混合查询引擎
  - https://github.com/xianfengyi/SparrowDB
    - A simple database, small but complete, so call Sparrow DB

- bitlap /11Star/MIT/202211/kotlin+scala
  - https://github.com/bitlap/bitlap
  - A table schema-less OLAP Analytics Engine for Big Data.
  - 开源的、并行的、低延时的分布式行为数据分析引擎。
  - bitlap所创建的表是没有表结构约束的，这就意味着你可以随意的添加指标和维度，而不需要关心表太宽的问题。
  - 支持SQL查询接口，所查即所得。支持任意指标维度的查询，无需构建cube

- https://github.com/openblocks-dev/openblocks /ts+java
  - The Open Source Retool Alternative
  - An all-in-one IDE to create internal or customer-facing apps.
  - A place to create, build and share building blocks of web applications.
# solutions
- elasticsearch /Apache2/49.9kStar/202007
  - https://github.com/elastic/elasticsearch
  - https://www.elastic.co/guide/en/elasticsearch/reference/current/index.html
  - Open Source, Distributed, RESTful Search Engine
- kibana /Apache2/14.5kStar/202007
  - https://github.com/elastic/kibana
  - https://www.elastic.co/guide/en/kibana/current/index.html
  - Kibana is your window into the Elastic Stack. 
  - a browser-based analytics and search dashboard for Elasticsearch.

- saiku /1.3kStar/apache2/201910/js+java/inactive
  - https://github.com/OSBI/saiku
  - http://community.meteorite.bi/
  - Saiku的主要工作是根据事先配置好的schema，将用户的操作转化成MDX语句提供给Mondrian引擎执行。
  - Saiku allows business users to explore complex data sources, using a familiar drag and drop interface and easy to understand business terminology, all within a browser
- mondrian /EPLv1/907Star/202007
  - https://github.com/pentaho/mondrian
  - http://mondrian.pentaho.com/
  - Mondrian是一个OLAP分析的引擎，主要工作是根据事先配置好的schema，将输入的多维分析语句MDX(Multidimensional Expressions)翻译成目标数据库／数据引擎的执行语言（比如SQL）。
  - an Online Analytical Processing (OLAP) server that enables business users to analyze large quantities of data in real-time
  - https://github.com/Datawheel/olap-client
    - Javascript client to interact with mondrian-rest and tesseract-olap servers.
  - https://github.com/Datawheel/vizbuilder
    - React component to visualize multiple kinds of charts according to the data returned by a olap-client query.
- kettle /Apache2/4.1kStar/202007
  - https://github.com/pentaho/pentaho-kettle
  - https://community.hitachivantara.com/s/article/data-integration-kettle
  - Pentaho Data Integration (ETL) a.k.a Kettle
- pentaho-reporting /LGPLv2/196Star/202007
  - https://github.com/pentaho/pentaho-reporting
  - http://www.pentaho.com/products/reporting/
  - Java class library for generating reports.
  - based on jfreechart
