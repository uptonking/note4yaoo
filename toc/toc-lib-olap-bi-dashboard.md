---
title: toc-lib-olap-bi-dashboard
tags: [bi, dashboard, olap, toc]
created: 2020-08-02T07:21:21.345Z
modified: 2020-12-09T09:30:24.694Z
---

# toc-lib-olap-bi-dashboard

# guide

- resources
  - https://github.com/thenaturalist/awesome-business-intelligence

- [乐居中后台管理系统教程](http://doc.bufanui.com/docs/leju-admin/leju-admin-1cmave6kurtts)
  - [day7主页大屏数据展示, vue+echarts](http://doc.bufanui.com/docs/leju-admin/leju-admin-1cmgcm5kelp3c)
  - [不凡学院 文档](http://doc.bufanui.com/)
# bi-analytics
- https://github.com/djouallah/Testing_BI_Engine /jupyter
  - Testing OLAP SQL Engine using TPC-H
  - so Far Tested Snowflake, BigQuery, Databrciks SQL, SingleStore, DuckDB, and PowerBI Datamart, I only include DB that take less than 100 second to finish the benchmark

- lightdash /2kStar/MIT/202301/ts/dbt
  - https://github.com/lightdash/lightdash
  - https://lightdash.com/
  - https://demo.lightdash.com/
  - [Setup Development Environment](https://github.com/lightdash/lightdash/blob/main/.github/CONTRIBUTING.md#setup-development-environment-without-docker)
  - open-source BI (Looker alternative) for teams that move fast.
  - 后端依赖 express、knex、pg、passport、puppeteer
  - 前端依赖 blueprintjs、echarts、jspdf、react-ace、react-beautiful-dnd、uiw/react-md-editor、casl
  - 主要功能模块
    - workspace
    - dashboard
    - charts/query
    - 用户与权限
  - 后端graphql只用来获取dbt元数据

- Superset /50.4kStar/Apache2/202301/ts/python
  - https://github.com/apache/superset
  - http://superset.apache.org/
  - a modern, enterprise-ready business intelligence web application
  - originally made for Druid
  - [Why Apache ECharts is the Future of Apache Superset™_202104](https://preset.io/blog/2021-4-1-why-echarts/)
  - https://github.com/apache-superset/superset-ui
  - https://github.com/apache-superset/examples-data
  - https://github.com/dropbox/incubator-superset-internal
  - https://github.com/yangfei4913438/superset-api-client
    - superset默认的ui没办法提供浏览器自适应，个性化图表渲染等功能，但是superset提供了一系列的API。所以我们可以使用这些API来定制适合我们自己需求的前端界面。

- mprove /270Star/apache2/202302/ts/inactive
  - https://github.com/mprove-io/mprove
  - https://mprove.io/
  - Open Source Self-service Business Intelligence with Version Control
  - Inspired by Looker.

- https://github.com/drinkjs/mojito /202205/ts/inactive
  - http://mojito.drinkjs.com/
  - Mojito是一个可视化数据分析、数据展示和轻业务开发的平台
  - 支持使用React/Vue开发上传自定义组件
  - 100%开源，支持私有化部署
  - 前端依赖 antd4、animejs、mobx、re-resizable、react-dnd、react-moveable、next10
  - 后端依赖 fastify、mysql、mongodb、typeorm

- https://github.com/abilian/olapy
  - an experimental OLAP engine based on Pandas
  - https://github.com/abilian/olapy-web
    -  web-based tool for exploring and analyzing OLAP databases served by the OlaPy.

- spotrix /11Star/apache2/202211/ts/flask
  - https://github.com/Spotrix/spotrix
  - https://spotrix.github.io/spotrix-web/
  - A modern, enterprise-ready business intelligence web application.
  - 依赖flask-appbuilder、sqlalchemy

- https://github.com/rawgraphs/rawgraphs-app /8.5kStar/apache2/202311/js
  - https://www.rawgraphs.io/
  - RAWGraphs is an open web tool to create custom vector-based visualizations on top of the amazing d3.js
  - 依赖d3.v7、sparqljs、@rdfjs-elements/sparql-editor、dayjs、lit-html、react-bootstrap、react-dnd
  - RAWGraphs works with tabular data (e.g., spreadsheets and comma-separated values) as well as with copied-and-pasted texts from other applications. 
  - Based on the SVG format, visualizations can be easily edited with vector graphics applications 
  - data injected into RAWGraphs is processed only by the web browser: no server-side operations or storages are performed.
- https://github.com/rawgraphs/rawgraphs-core
  - https://rawgraphs.io/rawgraphs-core/docs/
  - This javascript library was born to simplify and modularize development of the RawGraphs web app, but it can be used to implement the RAWGraphs workflow and rendering charts from javascript code.
  - 只依赖d3
- https://github.com/rawgraphs/rawgraphs-charts
  - A curated selection of charts provided through RAWGraphs interface
  - It uses the RAWGraphs core API to define charts behaviours.

- https://github.com/getredash/redash /24.1kStar/BSD/202311/python/flask
  - http://redash.io/
  - 依赖flask、antd、d3.v3.5.17
  - SQL users leverage Redash to explore, query, visualize, and share data from any data sources.

- tellery /323Star/apache2/202210/ts/inactive
  - https://github.com/tellery/tellery
  - https://tellery.io/
  - https://demo.tellery.io/
  - Tellery lets you build metrics using SQL
  - A modern SQL editor with multi-tabs and auto-complete

- turnilo /643Star/Apache2/202301/ts
  - https://github.com/allegro/turnilo
  - https://allegro.tech/2018/10/turnilo-lets-change-the-way-people-explore-big-data.html
  - Business intelligence, data exploration and viz web application for Druid
  - https://github.com/implydata/pivot

- evidence /2.5kStar/MIT/202311/js/svelte
  - https://github.com/evidence-dev/evidence
  - https://evidence.dev/
  - Build a polished business intelligence system using only SQL and markdown.

- https://github.com/ricklamers/gridstudio
  - a web-based spreadsheet application with full integration of the Python programming language.
  - 依赖Flask、golang、plotly、jquery

- panel /2.5kStar/BSD/202301/python
  - https://github.com/holoviz/panel
  - https://panel.holoviz.org/
  - the most flexible data app framework for Python
  - A high-level app and dashboarding solution for Python
  - Panel is a member of the ambitious HoloViz dataviz ecosystem and has first class support for the other members like hvPlot (simple .hvplot plotting api), HoloViews (powerful plotting api), and Datashader (big data viz).
  - Panel is built on top of Param. Param enables you to annotate your code with parameter ranges
  - You can share your data and models as
    - a web application running on the Tornado (default), Flask, Django or Fast API web server.
    - a stand alone client side application powered by Pyodide or PyScript via panel convert.
    - an interactive Jupyter notebook component.
    - a static .html web page, a .gif video, a .png image and more.

- tabix /1.1kStar/apache2/202205/ts/inactive
  - https://github.com/tabixio/tabix
  - http://dash.tabix.io/
  - simple business intelligence application and sql editor tool for Clickhouse.
  - 依赖antv/s2、monaco-editor、antd4、mobx-react、react-virtualized、handsontable.v6
  - https://github.com/rizalgowandy/tabix

- https://github.com/nzzdev/Q-editor /MIT/202308/js
  - https://editor.q.tools/
  - editor for the Q Toolbox. 
  - 依赖handsontable.v6、hapi
  - https://github.com/nzzdev/Q-server /202305/js
    - Q is a system that lets journalists create visual elements for stories. It is developed by NZZ Editorial Tech and NZZ Visuals and used in the NZZ newsroom. 
    - 依赖hapi、puppeteer

- countly /4.7kStar/AGPLv3/202101/js
  - https://github.com/Countly/countly-server
  - built with mongodb, express
  - Countly is a product analytics solution that helps teams track product performance and customer journey and behavior across mobile, web, and desktop applications. 
  - Countly relies on a wide diversity of SDKs for deployment
  - 依赖express、mongoose
  - [Download & Install Countly](https://github.com/osoner/countly-documentation/blob/master/installation/countly-server-installation.md)

- grafana /Apache2/36.5kStar/202008/go
  - https://github.com/grafana/grafana
  - https://grafana.com/
  - The tool for monitoring and metric analytics & dashboards for Graphite, InfluxDB & Prometheus & More
- https://github.com/saasforge/open-source-saas-boilerpate
  - Free SaaS boilerplate (Python/PostgreSQL/ReactJS/Webpack)
- https://github.com/keen/dashboards /10.8kStar/201911
  - CSS Grid-based templates
  - All examples have been updated to use keen-dataviz.js and keen-analysis.js

- https://github.com/streamlit/streamlit
  - https://streamlit.io/
  - The fastest way to build data apps in Python
  - [Streamlit已经强大到如此地步，可以完全代替flask吗？](https://zhuanlan.zhihu.com/p/270590933)
    - streamlit是基于tornado的，应该拿flask和tornado比较。flask活的比tornado滋润
  - https://github.com/PablocFonseca/streamlit-aggrid
    - Implementation of Ag-Grid component for Streamlit
  - https://github.com/cceyda/common-voice-explorer
    - https://28a3b43b-3997-4649-adda-93f52445562a.job.gra.training.ai.cloud.ovh.net/
# reporting
- jsreport /1.1kStar/LGPLv3/202305/js
  - https://github.com/jsreport/jsreport
  - https://jsreport.net/
  - jsreport is a reporting server letting developers define reports using javascript templating engines like handlebars. 
  - It supports various report output formats like html, pdf, excel, docx, and others. 
  - It also includes advanced reporting features like user management, REST API, scheduling, designer, or sending emails.
# viz-dashboard
- https://github.com/kantord/just-dashboard /1.5kStar/201907
  - https://kantord.github.io/just-dashboard/
  - Dashboards using YAML or JSON files
- https://github.com/plouc/mozaik /3.5kStar/201905
  - http://mozaik.rocks/
  - http://mozaik.herokuapp.com/
  - a tool based on react/redux/d3 to easily craft dashboards.

- https://github.com/Smashing/smashing
  - handsome dashboard framework in Ruby and Coffeescript.
  - a Sinatra based framework

- https://github.com/mlcraft-io/mlcraft
  - a low-code metrics layer and a modern open-source alternative to Looker.
  - Cube.js is used as a primary query layer and makes it suitable for handling trillions of data points.
# examples
- https://github.com/amcharts/covid-charts
  - A collection of JS-based data visualization tools and data for depicting spread of the COVID-19
- https://github.com/covid19cubadata/covid19cubadata.github.io
  - Covid19 - Dashboard for Cuba
- https://github.com/stevenliuyi/covid19
  - an interactive, animated COVID-19 coronavirus map to track the outbreak over time by country and by region

- https://github.com/savecost/datav
  - Visualization for metrics, traces and logs etc, datav is a lightweight but better alternative to Grafana. 
  - 后端依赖go
# misc
- snorkel
  - https://github.com/logv/snorkel
  - https://snorkel.logv.org/
  - a realtime exploratory data analysis tool that is complementary to your monitoring software
  - built with flask, bootstrap, nvd3
- insights
  - https://github.com/mariusandra/insights
  - Open Source Self-Hosted Business Intelligence Platform
  - a tool to visually explore a PostgreSQL database, with an emphasis on generating graphs that show business performance over time.
- raw /Apache2/6.8kStar
  - https://github.com/rawgraphs/raw
  - The missing link between spreadsheets and data visualization
