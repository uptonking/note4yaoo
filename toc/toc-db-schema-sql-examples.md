---
title: toc-db-schema-sql-examples
tags: [database, examples, sql, toc]
created: 2021-08-30T18:56:31.626Z
modified: 2021-08-30T18:57:27.645Z
---

# toc-db-schema-sql-examples

# guide

- 经典数据库
  - northwind, chinook, AdventureWorks, Sakila
  - foodmart
  - imdb/omdb, realworld
  - wikipedia
  - 学生选课
  - 购物订单
  - imdb

- [Database Examples - Wikiversity](https://en.wikiversity.org/wiki/Database_Examples)
# popular-db-schema-examples
- [IMDb Non-Commercial Datasets](https://developer.imdb.com/non-commercial-datasets/)
  - Subsets of IMDb data are available for access to customers for personal and non-commercial use.
  - [IMDb data files available for download](https://datasets.imdbws.com/)
  - Each dataset is contained in a gzipped, tab-separated-values (TSV) formatted file in the UTF-8 character set.

- [MongoDB Atlas: Load Sample Data](https://www.mongodb.com/docs/atlas/sample-data/)
  - Sample Mflix Dataset
    - Contains movie data.
  - Sample AirBnB Listings Dataset
    - Contains details on AirBnB listings.
  - Sample Analytics Dataset
    - Contains training data for a mock financial services application.
  - Sample Geospatial Dataset
    - Contains shipwreck data.
  - Sample Guides Dataset
    - Contains planet data.
  - Sample Restaurants Dataset
    - Contains restaurant data.
  - Sample Supply Store Dataset
    - Contains data from a mock office supply store.
  - Sample Weather Dataset
    - Contains detailed weather reports.

- [PostgreSQL wiki - Sample Databases ](https://wiki.postgresql.org/wiki/Sample_Databases)
  - MySQL has a popular sample database named Sakila. 
  - Pagila is a more idiomatic Postgres port of Sakila.
  - IMDB - the original IMDB source data.
  - OMDB - Open Media database, ~30MB compressed, 300MB when loaded
  - DBpedia - Wikipedia data export project
  - Data.gov - US federal government data collection
  - Openstreetmap - Openstreetmap source data
  - Freebase - Various wiki style data on places/people/things

- [Postgres sample data - Neon Docs](https://neon.com/docs/import/import-sample-data)
  - Netflix data
    - A dataset containing information about movies and tv shows on Netflix.
  - Chinook database
    - A sample database for a digital media store, including tables for artists, albums, media tracks, invoices, customers, and more.
  - Titanic passenger data
  - Pagila database
    - Sample data for a fictional DVD rental store. Pagila includes tables for films, actors, film categories, stores, customers, payments, and more.
  - Lego database 乐高积木
  - Employees database
  - Wikipedia vector embeddings
    - An OpenAI example dataset containing pre-computed vector embeddings for 25000 Wikipedia articles. 
  - Postgres air
    - An OpenAI example dataset containing pre-computed vector embeddings for 25000 Wikipedia articles. 

- [DoltHub - Discover Databases](https://www.dolthub.com/discover?tab=discover)
  - 类似数据库版github

- https://github.com/ClickHouse/ClickBench /CC-NC-SA/202402
  - https://benchmark.clickhouse.com/
  - ClickBench: a Benchmark For Analytical Databases
  - It covers the typical queries in ad-hoc analytics and real-time dashboards.
  - 比较了很多数据库，包括clickhouse、sqlite、mysql、pg、duckdb、doris、druid、mongodb、es
  - 提供了很多 Similar Projects/alternatives
  - This benchmark represents typical workload in the following areas: clickstream and traffic analysis, web analytics, machine-generated data, structured logs, and events data. 
  - The dataset from this benchmark was obtained from the actual traffic recording of one of the world's largest web analytics platforms.
  - The dataset is available in CSV, TSV, JSONlines and Parquet formats

- https://github.com/prisma/database-schema-examples /202102/inactive
  - Database Schema Examples we strive to support in Prisma
  - This repository contains examples for database schemas, grouped by database. 
  - Useful whenever we need a real world example
  - 提供了很多常用的公开数据集，在`mysql/pg/sqlite`各文件夹下数据不同
  - 很多是从docker中的db导出的

- https://github.com/oracle/db-sample-schemas /202308
  - Oracle Database Sample Schemas
  - Human Resources; Order Entry; Online Catalog; Product Media; Information Exchange; Sales History; Customer Orders
  - [Introduction to Sample Schemas](https://docs.oracle.com/en/database/oracle/oracle-database/21/comsc/introduction-to-sample-schemas.html)
- https://github.com/oracle/oracle-db-examples
  - This repository stores a variety of examples demonstrating how to use the Oracle Database.
- https://github.com/oracle/json-in-db
  - Oracle Database JSON Examples

- https://github.com/microsoft/sql-server-samples/tree/master/samples/databases /202310
  - code samples that demonstrate how to use Microsoft's Azure Data products including SQL Server, Azure SQL Database, Azure Synapse, and Azure SQL Edge. 
  - 经典示例包括 wide-world-importers、contoso-data-warehouse、AdventureWorks、northwind
  - AdventureWorks is the OLTP sample, and AdventureWorksDW is the data warehouse sample.

- https://github.com/julianhyde/foodmart-data-mysql /201512/java
  - Foodmart data set in MySQL format
  - https://github.com/julianhyde/foodmart-queries /201503/java
    - SQL queries issued by Mondrian against the FoodMart data set, in JSON format
    - It was generated by the test suite of the Pentaho Mondrian OLAP engine, but serves as a challenging benchmark for any SQL engine.
- https://github.com/OSBI/foodmart-data /201408/inactive
  - A wrapper to the Mondrian FoodMart Data Loader
  - takes the FoodMart SQL Creation script and loads the data onto the database of your choice.
  - Drivers that are included on this version are: ProstgreSQL, MySQL, SQL Server & Sybase

- https://github.com/awesomejt/database-schema-examples
  - 经典的shopping_cart例子
# eg-northwind
- https://github.com/microsoft/sql-server-samples/tree/master/samples/databases/northwind-pubs
  - [Northwind 2.0 Developer Edition - Microsoft Support](https://support.microsoft.com/en-us/office/northwind-2-0-developer-edition-32eb79d2-bede-4ea4-b575-0714ca8dc1e2)
  - [Northwind sample database | YugabyteDB Docs](https://docs.yugabyte.com/preview/sample-data/northwind/)
    - The Northwind database contains the sales data for a fictitious company called “Northwind Traders”

- https://github.com/harryho/db-samples /202012/js/inactive
  - Northwind sample database for MySql, PostgresQL, mongo, sqlite etc.
  - This folder contains scripts to create and load the Northwind sample databases.
  - 提供了ER图
  - This project is inspired by Microsoft Sample Databases, but it only targets other databases, such as MySql, PostgresQL, etc.

- https://github.com/valoni/northwindextended /202308
  - Northwind Microsoft Database Sample which one is extended and created in other databases
  - XML, Json

- https://github.com/jpwhite3/northwind-SQLite3 /MIT/202312/python
  - This is a version of the Microsoft Access 2000 Northwind sample database, re-engineered for SQLite3.
  - The Northwind sample database was provided with Microsoft Access as a tutorial schema for managing small business customers, orders, inventory, purchasing, suppliers, shipping, and employees.
  - All the TABLES and VIEWS from the MSSQL-2000 version have been converted to Sqlite3 and included here.

- https://github.com/pthom/northwind_psql /202210
  - A simple sql script that will populate a database with the famous northwind example, adapted for postgres.
  - Use the provided sql file `nortwhind.sql` in order to populate your database.
  - https://github.com/engindemirog/Northwind-Database-Script-for-Postgre-Sql /202105

- https://github.com/joovitor12/northwind-node /202210/ts/js/sequelize
  - northwind-node, northwind-react

- https://github.com/MrsLecter/Traders /202210/ts/ejs/sequelize
  - Creating a database from existing tables, queries to the database
  - Express + PostgreSQL + Sequelize + Bootstrap

- https://github.com/drizzle-team/drizzle-northwind-benchmarks /202304/ts/inactive
  - 测试项目 sqlite3、knex、prisma、mikro
  - https://github.com/drizzle-team/drizzle-northwind-benchmarks-pg
    - Postgres benchmarks between Drizzle ORM and other popular ORM

- https://github.com/dalers/mywind /201604
  - a MySQL version of the Microsoft Access 2010 Northwind sample database.
  - https://github.com/jasny/mongodb-northwind /202010/js
    - A MongoDB version of the Microsoft Access 2010 Northwind sample database.
    - created from MyWind; a MySQL version of Northwind.

- https://github.com/tmcnab/northwind-mongo /201306/inactive
  - Northwind dumped to MongoDB

- https://github.com/therealyo/northwind2
  - northwind traders task implementation using different ORMS

- https://github.com/Mayowa-Taiwo/Tabular-Database-and-OLAP-Cube-with-Northwind_OLTP /202309
  - Second part of the Northwind Relational database to OLAP Cube project. 
  - This portion deals with Layering the semantic layer on the Datawarehouse for end users

- https://github.com/priye-1/OLAP_Dimensional_Modeling_for_Advanced_Analytics /202307
  - This project unlocks the power of advanced analytics and reporting by transforming an OLTP architecture into an efficient OLAP system. 
  - It Leverages the capabilities of DBT and BigQuery to implement dimensional modelling and drive data-driven decision-making.
  - https://github.com/Chisomnwa/Building-OLAP-Dimensional-Model-using-BigQuery-and-DBT

- https://github.com/Yasmeen-Shamakh/Northwind-DataWarehouse /202312
  - A data warehouse is designed and implemented on the "Northwind" database.
  - Developed ETL data pipelines using SQL Server Integration Services (SSIS) to automate the extraction, transformation, and loading of data from the source database (OLTP) to the data warehouse (OLAP)
  - https://github.com/Dmnk28/NorthwindDataWarehouse /202208
    - A Three Day Project about creating a Staging and an OLAP Database for the Northwind Samplefiles
  - https://github.com/ricardomilhazes/MDDBS-NorthWind /202001

- https://github.com/michael-wolfenden/dynamodb-toolbox-northwind /202008/js
  - This is an implementation of northwind using a DynamoDB single table design
  - This is an implementation using Jeremy Daly's dynamodb-toolbox library

- https://github.com/Breeze/northwind-demo /202106/ts/js
  - Breeze end-to-end demo with client and server
  - Client is one of Angular Aurelia React Vue
  - Server is one of . NET, NodeJS with Sequelize
  - 前后端都依赖breeze-client
  - Breeze Client (breeze-client) is a JavaScript library for managing data on the client, much as an ORM manages it on the server.

## apps-northwind

- https://github.com/Musili-Adebayo/Northwind-Database /202308
  - This repository contains 50 queries and answers to the popular northwind database using MySQL
  - [50 SQL Practice Queries and Answers _202101](https://musiliadebayo.medium.com/50-sql-practice-queries-and-answers-3fc896650b2e)

- https://github.com/ndleah/northwind /202111
  - perform an analysis for 10 Business Questions
- https://github.com/biancashiromoto/basic-sql-queries /202310/sql
  - A set of SQL queries to retrieve and manipulate data from the "Northwind" database

- https://github.com/kmvx/northwind /202401/ts/纯前端
  - https://northwind.kmvx.tk/
  - 依赖tanstack-query.v5、react-chartjs-2、d3

- https://github.com/elessartech/northwind-dashboard /202311/ts
  - https://northwind-dashboard.vercel.app/
  - Northwind Dashboard
  - 依赖express、mongoose、sqlite3、react-csv、nivo-chart
  - 用户元数据存在mongodb，订单数据寻在sqlite

- https://github.com/DaniilBaldin/NorthwindTraders /202301/ts
  - Back end part for Northwind Traders, using TypeScript and MySQL.
  - 依赖express、mysql2、multer
  - https://github.com/DaniilBaldin/northwind-traders-frontend /202302/ts
    - https://northwind-traders-frontend.vercel.app/
    - 依赖react-redux、mui.v5

- https://github.com/MeralTd/NorthwindApp /202101/js/mock接口数据
  - 依赖json-server、react-redux
  - https://github.com/berkesayin/northwind-store /202312/ts
  - https://github.com/ahmet-cetinkaya/northwind-json-server /202211/js
  - https://github.com/abdulkadir-caglar/northwind-redux /202401/js

- https://github.com/ibrahim1912/React-Northwind-Frontend /202106/js
  - https://github.com/ibrahim1912/Java-Northwind-Backend
  - https://github.com/ibrahim1912/Angular-Northwind-Frontend

- https://github.com/esrasnck/reactForNorthwind /202106/js
  - https://github.com/esrasnck/JavaNorthwind

- https://github.com/cloudflare/d1-northwind /MIT/202307/js
  - https://northwind.d1sql.com/
  - Northwind Traders D1 Demo
  - a demo of the Northwind dataset, running on Cloudflare Workers, and D1 - Cloudflare's newest SQL database, running on SQLite.
  - 使用cf全家桶
  - D1 for database
  - Cloudflare Workers for computing
  - Remix for the React framework
  - https://github.com/jacob-ebey/remix-d1-northwind

- https://github.com/bbraithwaite/NorthwindNode /201506/js/可参考后端
  - This example project accompanies the Learn the Mean Stack- Beginner Tutorial
  - 依赖express、mongoose、passport、angular.v1
  - [Mean Stack Tutorial - Beginners Tutorial _201502](https://www.bradoncode.com/tutorials/learn-mean-stack-tutorial/)
  - https://github.com/bbraithwaite/NorthwindStart

- https://github.com/bhaeussermann/northwind-api /202209/ts
  - A RESTful API providing CRUD functionality for managing Employees in a PostgreSQL database
  - 依赖express、pg、openapi

- https://github.com/RohitPradhan0518/Northwind-Workshop /202312/js
  - https://github.com/RohitPradhan0518/northwind-workshop-express-server-main /202312/js
    - the backend for the Shop at Northwind workshop.
    - 数据基于内存，未使用数据库

- https://github.com/coditech0926/fullstack-northwind /202104/ts
  - React and Node(Typescript) with Northwind MySQL Db
  - MikroORM/Inversify

- https://github.com/dorbar7/Northwind-Traders /202312/ts
  - frontend + backend
  - https://github.com/AlexanderVasilenko99/northwind-full-stack /202312/ts
  - https://github.com/DanilVo/Northwind-Full-Stack /202312/ts
  - https://github.com/YogevBar1/NorthWind-React /202310/ts

- https://github.com/OleksiiKH0240/Northwind_Traders /202401/ts/仅后端
  - 依赖express、drizzle-orm、postgres
  - https://github.com/heorhiikovalskyi/NorthwindTraders /202311/ts
  - https://github.com/realmikesolo/northwind
    - typeorm/prisma

- https://github.com/sammorton11/nodejs-northwind-server /202401/js
  - a simple Express server using SQLite databases for demonstration purposes. 
  - It provides RESTful API endpoints for managing users, orders, and interacting with the Northwind database.
  - https://github.com/sammorton11/go-northwind-server /go

- https://github.com/Kybbot/northwind-traders
  - http://northwind-traders.vercel.app/
  - 用ts重写前端

- https://github.com/telerik/kendoui-northwind-dashboard /asp/c#
  - https://demos.telerik.com/aspnet-mvc/html5-dashboard-sample-app/
  - A dashboard for Northwind built with Telerik UI for ASP. NET MVC.

- https://github.com/vasyl1312/24.northwind_traders /202310/ts
  - Realise a backend 
- https://github.com/Sir-Aguiar/Northwind-Backend /202311/ts
  - 未使用数据库

- https://github.com/raynaldmo/northwind-mongodb /201407/js
  - A command line tool to display northwind traders db reports
  - This app is meant to be learning tool for those learning how to implement mongodb CRUD and aggregation operations using the node native mongodb driver.

- https://github.com/Breeze/northwind-demo
  - Breeze demo with . NET and NodeJS servers and Angular, Aurelia, React, and Vue clients
  - https://github.com/Breeze/breeze.js /202105/js/inactive
    - http://breeze.github.io/doc-js/
    - BreezeJS is a JavaScript library that helps you manage data in rich client applications
    - Breeze applications rely mostly on data binding to coordinate the flow of values between a Breeze entity and the widgets on screen. 

- https://github.com/nullpointer-excelsior/nestjs-northwind-hexagonal /202212/ts
  - Implementation of design patterns for microservices with hexagonal architecture

- https://github.com/thangchung/northwind-rs /202105/rust
  - The northwind application with the clean architecture approach powered by Rust
  - actix-web, sqlx, jwt
# eg-chinook
- https://github.com/lerocha/chinook-database /202402
  - a sample database available for SQL Server, Oracle, MySQL, etc. 
  - It can be created by running a single SQL script. 
  - Chinook database is an alternative to the Northwind database, being ideal for demos and testing ORM tools targeting single and multiple database servers.
  - The name of this sample database was based on the Northwind database. Chinooks are winds in the interior West of North America
# eg-AdventureWorks
- https://github.com/lorint/AdventureWorks-for-Postgres /MIT/202301
  - Set up the AdventureWorks sample database for use with Postgres
  - Provided is a ruby file to convert CSVs available on CodePlex into a format usable by Postgres

- https://github.com/NorfolkDataSci/adventure-works-postgres /201702
  - Adventureworks OLTP for training, tutorials
  - convert the csv's to be compatible with postgres

- https://github.com/alaahgag/data_mart_building /202212
  - In this project, I focus on building a sales data mart for a company by extracting new and updated data from the AdventureWorks2019 (OLTP data) database, creating a star schema and load data to dimensions and fact tables after transforming the data
# eg-imdb/omdb
- https://github.com/df7cb/omdb-postgresql /202309
  - This database contains CSV data downloaded from omdb, imported into a normalized PostgreSQL database schema. 
  - The data is basically unmodified, except for the removal of entries that would violate foreign key constraints. 
  - The database import script also removes some adult movies.
  - The database schema is intentionally not optimized (no indexes besides primary keys) in order to serve as a playground for database optimization.
# db-examples
- https://github.com/gregorybarros/QyonAdventureWorks
  - Backend JSON-Server, frontend Reactjs com TS e Material-ui

- https://github.com/marcelopwmendes/adventure-works-api-basic-auth
  - A small TypeScript API that connects to the MS SQL Server sample database "Adventure Works"; 
  - Authentication was done with Json Web Token based on the Email and Password of the user that comes in the request body; 
- https://github.com/Deividwb/QyonAdventureWorks
  - front-web-react + 后端仅json

- https://github.com/Guilherme-Ciano/Qyon_Adventure_Works_frontend
  - https://github.com/JonatasFreireDev/QyonAdventureWorks
  - https://github.com/Guilherme-Ciano/Qyon_Adventure_Works_backend

- https://github.com/JulianSalinas/adventure-works-ui
  - https://github.com/JulianSalinas/adventure-works-api /c#
  - react

- https://github.com/arlo47/adventure-works-ts
  - TypeScript API Using Adventure Works
  - https://github.com/arlo47/AdventureWorks-API
    - An ASP.NET Web API built with Entity Framework

- https://github.com/tonmoy-dev/FoodMart-client-side
  - https://github.com/tonmoy-dev/FoodMart-server-side /单文件
  - http://food-mart-web.vercel.app/
  - React, Next.js, Redux Toolkit, Node.js, MongoDB, Firebase Authentication, Tailwind CSS, Stripe Payment Gateway.
  - It has a dynamic admin panel
  - 作者写了很多示例
# more-db-data
- https://github.com/cheikhnadiouf/sql-relational-database-schema
  - Data tables and their relational models including users, sections, items/products, addresses, events, assets files, orders, payments, etc.
