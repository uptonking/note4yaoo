---
title: toc-lib-data-portal-solutions
tags: [data, portal, solutions, toc]
created: 2021-01-01T16:02:10.483Z
modified: 2021-01-01T16:02:50.598Z
---

# toc-lib-data-portal-solutions

# guide

- resources
  - [Projects tagged with opendata | Read the Docs](https://readthedocs.org/projects/tags/opendata/)
# popular
- CKAN /3.6kStar/AGPLv3/202301/python/js
  - https://github.com/ckan/ckan
  - https://ckan.org/
  - https://ckan.org/showcase
  - CKAN is an open-source DMS (data management system) for powering data hubs and data portals. 
  - CKAN makes it easy to publish, share and use data. 
  - who is using #ckan
    - [ata.gov.au ](https://data.gov.au/data/dataset)
    - [data.gov.sg ](https://data.gov.sg/datasets)
    - [Energi Data Service | Datasets ](https://www.energidataservice.dk/datasets)
    - [National Energy System Operator ](https://www.neso.energy/search#tab=Data%20Portal&f-content_type=Dataset)
    - [英国政府数据网站](https://data.gov.uk/)
    - [巴西政府数据网站](https://dados.gov.br/)
    - [Research Data Repository of the University of Porto](https://ckan-rdm.up.pt/)
    - [自治体オープンデータのCKANへようこそ](https://ckan.open-governmentdata.org/dataset)
    - [EDaWaX: Choosing CKAN for managing research data_202104](https://ckan.org/blog/edawax)

- DKAN /320Star/GPLv2/202301/php/js
  - https://github.com/GetDKAN/dkan
  - https://dkan.readthedocs.io/
  - DKAN is an open-source open-data platform inspired by CKAN and built on top of the very popular Drupal CMS
  - DKAN is a Drupal module that adds data management functionality.
  - [Comparing DKAN v7 and CKAN ](https://dkan.readthedocs.io/en/7.x-1.x/introduction/dkan-ckan.html)
    - CKAN has powerful publishing, auditing, and harvesting features for open datasets. Those using CKAN often choose to pair it with Drupal, Wordpress, Django, or other content management systems (CMS) or web publishing platforms to create pages, blogs and other content.
    - DKAN takes a different approach by integrating open data catalog features into an existing CMS. Datasets are treated as content that can unlock rich workflows. Drupal also provides a user interface for many site management activities. 
    - Again, DKAN is a complementary effort to CKAN in enabling people to publish open data using open source tools.

- datopian-portaljs /2.2kStar/MIT/202509/ts
  - https://github.com/datopian/portaljs
  - https://portaljs.org/
  - a framework for rapidly building rich data portal frontends using a modern frontend approach.
  - 依赖nextjs、ag-grid、tanstack-table、xlsx、material-ui.v4、mui-x-data-grid、react-plotly.js
  - built in Javascript and React on top of the popular Next.js framework. 
  - portal assumes a "decoupled" approach where the frontend is a separate service from the backend and interacts with backend(s) via an API. 
  - It can be used with any backend and has out of the box support for CKAN.
  - Portal.js used to be Recline(JS)
  - [FAQs about DataHub _202405](https://github.com/datopian/portaljs/discussions/1166)
    - DataHub can be used as a complement to CKAN. Specifically, DataHub PortalJS allows you to rapidly building powerful data portal frontends and integrates directly with CKAN. It is inspired by the "headless" CMS model and uses CKAN as a headless DMS.
    - It can be used to create a alternative frontend to CKAN using modern frontend tooling and integrate alternative content sources.
    - DataHub can also be used as a full replacement for CKAN if you want to manage your metadata and content differently than CKAN. DataHub offers its own native metadata management but it also provides an innovative integration with GitHub as well as connectors to other metadata management solutions 
    - DataHub's real power is it allows you to mix and match especially in the backend. 
    - DataHub can use many different data "backends" i.e. sources for data and metadata. For example, you can use CKAN, S3 etc. However, Git(hub) is our favorite and default backend.
  - https://www.datopian.com/solutions/open-data-portals
    - 👷🏻 Our team is proud to be led by the creator of CKAN
  - https://www.portaljs.com/data-portals
    - https://opendatanepal.com/dataset
    - https://fivethirtyeight.portaljs.org

- https://github.com/datopian/frontend-v2
  - Data Portal frontend. Designed for CKAN but usable anywhere. 
  - Microservice architecture so you can run and customize it standalone and connect to your backend of choice. 
  - https://github.com/datopian/playbook
  - https://github.com/keitaroinc/ckanext-visualize

- https://github.com/awslabs/open-data-registry /apache2/python
  - https://registry.opendata.aws/
  - A repository of publicly available datasets that are available for access from AWS resources
  - https://github.com/awslabs/open-data-registry-browser
    - a simple, web-based visualization of the data in registry

- https://github.com/simonw/datasette /apache2/202409/python
  - https://datasette.io/
  - https://global-power-plants.datasettes.com/global-power-plants/global-power-plants
  - open source multi-tool for exploring and publishing data
  - 不依赖flask和django
  - 依赖jinjia2、hupper、pint、pluggy、uvicorn、janus、asgiref、asyncinject
  - It helps people take data of any shape or size and publish that as an interactive, explorable website and accompanying API.
  - https://lite.datasette.io/
    - Datasette Lite is Datasette packaged using WebAssembly so that it runs entirely in your browser, no Python web application server required
  - [Architecture Notes: Datasette | Hacker News_202205](https://news.ycombinator.com/item?id=31530690)
    - Building a modern Python app using ASGI
    - "My breakthrough was the realization that read-only data packaged as a SQLite database could be deployed to inexpensive serverless hosting"
    - My breakthrough was the realization that any text data packaged as a SQLite database could be deployed to inexpensive serverless hosting. And binary data too
    - For sites that are running in CKAN using the datastore plugin on CSV/tabular resources, there is essentially a sql endpoint to make queries against that data. There are also automated conversions of that data to csv/json/xml. In my experience though, there's not a lot of activity around those apis -- people tend to just download the data.

- dataverse /826Star/apache2/202401/java
  - https://github.com/IQSS/dataverse
  - http://dataverse.org/
  - sharing, finding, citing, and preserving research data
  - who is using #dataverse
    - [北京大学开放研究数据平台](https://opendata.pku.edu.cn/dataverse.xhtml)
    - [复旦大学社会科学 Dataverse](https://dvn.fudan.edu.cn/dataverse.xhtml)
    - [Harvard Dataverse](https://dataverse.harvard.edu/)
    - [Australian Data Archive](https://ada.edu.au/popular-data/)

- https://github.com/DSpace/DSpace /816Star/BSD/202401/java
  - https://wiki.lyrasis.org/display/DSDOC7x/
  - The DSpace digital asset management system that powers your Institutional Repository
  - DSpace consists of both a Java-based backend and an Angular-based frontend.
  - Backend (this codebase) provides a REST API, along with other machine-based interfaces (e.g. OAI-PMH, SWORD, etc)
  - Frontend (https://github.com/DSpace/dspace-angular/) is the User Interface built on the REST API
  - Prior versions of DSpace (v6.x and below) used two different UIs (XMLUI and JSPUI). Those UIs are no longer supported in v7 (and above).
  - https://github.com/DSpace/RestContract
    - new DSpace REST API Contract beginning with version 7.0
    - At the ROOT of the API a HAL document lists all the primary endpoints allowing full discovery of the API.
    - all terms used are meant to reference RESTful terminology and/or terminology borrowed from Spring Data REST.

- https://github.com/magda-io/magda /apache2/202301/ts/js/scala
  - https://magda.io/
  - A federated, open-source data catalog for all your big data and small data
  - As an open data search engine
  - Powerful and scalable search based on ElasticSearch
  - Federated authentication via passport.js

- https://github.com/Inist-CNRS/lodex /js
  - Lodex is a tool to enable publishing a set of data csv, tsv, xml, json, ... in semantic web formats JSON-LD, N-Quads, ... and propose to manipulate them in a backoffice.
# data-ai
- https://github.com/Oxen-AI/oxen-release /apache2/202502/python/rust
  - https://oxen.ai/
  - fast data version control system for structured and unstructured machine learning datasets. 
  - We aim to make versioning datasets as easy as versioning code.
  - The interface mirrors git, but shines in many areas that git or git-lfs fall short. Oxen is built from the ground up for data, and is optimized to handle large datasets, and large files.
    - oxen clone https://hub.oxen.ai/ox/CatDogBBox
  - Oxen is comprised of a command line interface, as well as bindings for Rust 🦀, Python 🐍, and HTTP interfaces to make it easy to integrate into your workflow.
  - This repository contains the Python library that wraps the core Rust codebase. 
  - Oxen is designed to efficiently manage large datasets, including those with large individual files, for example CSV files with millions of rows. 
    - It also handles datasets comprising millions of individual files and directories such as the complete collection of ImageNet images.
  - Collaborate with your team (sync to an oxen-server)
  - Solutions like `git-lfs` are too slow when it comes to the scale of data we need for machine learning.
  - https://github.com/Oxen-AI/Oxen /apache2/202503/rust
    - Oxen.ai's core rust library, server, and CLI
    - Oxen at it's core is a data version control library, written in Rust.
    - Oxen Server: Remote repositories have the same internal structure as local ones, with the caviate that all the data is in the .oxen dir and not duplicated into a "local workspace".
# metadata
- https://github.com/GuinsooLab/darkseal
  - A Single place to Discover, Collaborate, and Get your data right
  - Darkseal depends on following components to build a metadata platform:
    - JsonSchemas for defining Metadata Schemas
    - Dropwizard/Jetty for REST APIs
    - MySQL 8.x to store Metadata (Guinsoo is coming)
    - ElasticSearch/OpenElasticsearch 7.x to index Metadata and power

- https://github.com/GeoNode/geonode /GPL/202405/python/js
  - GeoNode is an open source platform that facilitates the creation, sharing, and collaborative use of geospatial data.
# more
- https://github.com/feup-infolab/dendro /202006/js/inactive
  - "Open-source Dropbox" with added description features. 
  - It is a data storage and description platform designed to help researchers and other users to describe their data files, built on Linked Open Data and ontologies. 
  - Users can use Dendro to publish data to CKAN, Zenodo, DSpace or EUDAT's B2Share and others.
