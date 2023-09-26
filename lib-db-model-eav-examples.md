---
title: lib-db-model-eav-examples
tags: [database, entity-attribute-value, examples, toc]
created: 2023-09-25T17:56:12.065Z
modified: 2023-09-25T17:56:50.116Z
---

# lib-db-model-eav-examples

# guide

# query-property-graph
- https://github.com/fictiveworks/mementus /js
  - In-memory property graphs with composable query pipelines
  - Property graph data structures for JS applications.

- https://github.com/kracr/pg-benchmark /java
  - A Property Graph (PG) benchmark that generates PG dataset and the queries to run on the dataset

- https://github.com/oracle/pgql-lang /apache2/java
  - https://pgql-lang.org/
  - PGQL is an SQL-based query language for the property graph data model, bringing graph pattern matching capabilities to SQL and NoSQL users.

- https://github.com/ravifrancesco/PGQL-Query-Planner /java
  - Query planner for graph queries using PGQL (Property Graph Query Language).

- https://github.com/itergia/pgql-go /go
  - A skeleton implementation of the Property Graph Query Language (PGQL).
  - Both openCypher and PGQL are being considered in GQL, an attempt to standardize a graph query language under ISO's SQL.

- https://github.com/abakisita/rdf_to_property_graph /python
  - Library to map RDF data to Property Graph Model data

- https://github.com/LiorKogan/V1 /paper
  - https://v1.ms/V1/
  - V1: A Visual Query Language for Property Graphs
# eav
- https://github.com/PsychoSanchez/mongodb-vs-mysql-eav-benchmark /202211/js
  - This is a benchmark of MongoDB vs MySQL for EAV (Entity-Attribute-Value) data model.
  - Both MongoDB and MySQL are running in Docker containers, gateway is a Node.js app running fastify.
  - 比较了 mongodb/mysql-json/mysql-eav/pg-jsonb
  - benchmarks的结果是json/jsonb在大多数场景下性能好于eav

- https://github.com/adriano-di-giovanni/reaves /MIT/201811/js/inactive
  - a Javascript implementation of the Entity-Attribute-Value model and the event sourcing pattern for Node.js.
  - Simply put, it lets you save and retrieve present and past string values of attributes that belong to entities identified by string IDs. 
  - Reaves is backed by Redis.

- https://github.com/smallhelm/entity-wharf-js /MIT/201412/js/inactive
  - Store data as entity attribute values in memory
  - All data stored in Wharf is organized uniformly as eav
  - designed to be used as a state management solution for applications that need to be performant for quickly mutating state over many different types of entities with similar characteristics.

- https://github.com/madnl/eav-store /js/inactive
  - Entity-Attribute-Value store

- https://github.com/dst/cars /201610/js/java/inactive
  - Entity-attribute-value (EAV) model implementation based on car. 
  - Cars in EAV model are kept in a rational database (embedded H2). 
  - Attributes together with basic fields are also kept in a document database (embedded MongoDB) to support faster search operations.

- https://github.com/jazzband/django-eav2 /LGPLv3/202309/python/Django
  - https://django-eav2.readthedocs.io/
  - EAV storage for modern Django
  - Data in EAV is stored as a 3-tuple (typically corresponding to three distinct tables): entity, attribute, value
  - Entities in django-eav2 are your typical Django model instances.
  - EAV is a trade-off between flexibility and complexity. 
  - In some use-cases, JSONB (binary JSON data) datatype (Postgres 9.4+ and analogous in other RDMSs) can be used as an alternative to EAV.
    - JSONB supports indexing, which amortizes performance trade-off. 
    - It's important to keep in mind that JSONB is not RDMS-agnostic solution and has it's own problems, such as typing.
  - [Django EAV 2 – Entity-Attribute-Value Storage for Django | Hacker News_201807](https://news.ycombinator.com/item?id=17628685)
- https://github.com/powered-by-wq/vera /python/inactive
  - Python/Django reference implementation of the ERAV data model

- https://github.com/ssledz/eav-model-pattern /201502/java/inactive
  - EAV is also known as object–attribute–value model, vertical database model and open schema.

- https://github.com/zakyalvan/simple-java-eav /201506/java/inactive
  - Simple implementation of Entity Attribute Value (EAV) pattern written using Java

- https://github.com/zavyalovartem/mybatis-entity-attribute-value-test /java
  - Weekend test project to learn basics of MyBatis and EAV database model. Very incomplete and hacky example - work in progress

- https://github.com/Workiva/eva /558Star/EPL/201907/clojure/inactive
  - A distributed database-system implementing an entity-attribute-value data-model that is time-aware, accumulative, and atomically consistent
  - Its API is by-and-large compatible with Datomic's.
- https://github.com/bowbahdoe/eva /clojure/fork
  - a distributed database-system implementing an entity-attribute-value data-model that is time-aware, accumulative, and atomically consistent.
  - My hope is to clean up the code, make an HTTP layer for a remote peer, and make a Rust embedded peer so that this sort of Database can finally escape the JVM.
  - If you want to use something open source today that has the same query language but a different data model, https://xtdb.com/ is high quality.
# triplestore
- https://github.com/rubensworks/rdf-stores.js /MIT/ts
  - A TypeScript/JavaScript implementation of the RDF/JS store interface with support for quoted triples.
  - provides an in-memory triple/quad store with triple/quad pattern access. 
  - It allows you to configure indexes to tune performance for specific cases.
  - Note that this library only focuses on triple storage and provide triple pattern query access. If you want to execute more complex queries over this store (such as SPARQL queries), engines such as Comunica may be used
  - In-memory indexing
  - Quoted triples support (RDF-star / RDF 1.2)
  - Implements the RDF/JS Store and RDF/JS DatasetCore interfaces

- https://github.com/Symatem/SymatemJS /202010/js/inactive
  - A graph database which combines triple-store, key-value-store and distributed version control

- https://github.com/crubier/Hexastore /201506/js/inactive
  - http://crubier.github.io/Hexastore/
  - A fast, pure javascript triple store implementation, also useful as a graph database.
  - Hexastore is based on this research paper. 
    - It is a way to structure RDF data such that queries are really fast. 
    - However, as implemented here, it has a 6 fold increase in memory usage as compared to a naive implementation of a triple store.
  - Go check the factis package and factis.io instead

- https://github.com/Factisio/factis /201506/js
  - The Factis modular database system in one package

- https://github.com/SUNRUSE-Junk-Drawer/narragen /ts
  - Procedural narrative generation through recursive triple-store pattern matching
  - All state is stored in a triple-store; this means that all information is stored as an entity, an attribute of that entity, and the value of that attribute of that entity
  - Rules look for patterns in the data, and can make changes to it based on those patterns

- https://github.com/terminusdb/terminusdb-store /341Star/apache2/202309/rust
  - a tokio-enabled data store for triple data
  - This library implements a way to store triple data - data that consists of a subject, predicate and an object, where object can either be some value, or a node
  - This library is intended as a common base for anyone who wishes to build a database containing triple data.
  - This library is tokio-enabled. Any i/o and locking happens through futures, and as a result, many of the functions in this library return futures. 
  - The HDT format, which the terminusdb-store layer format is based on
  - We are constantly developing terminusdb-store to make it a high quality succinct(简洁的) graph representation versioned datastorage layer. 
  - Starting with version 0.20.0, terminus-store uses a new storage format, which bundles all files into a single archive, and also supports value types. 

- https://github.com/spacejam/triple /rust/inactive
  - embeddable/standalone rust triple store

- https://github.com/IBM/expressive-reasoning-graph-store /java
  - Expressive Reasoning Graph Store (ERGS) is an OWL reasoner and an RDF triple store built on top of a Property Graph architecture.
  - ERGS uses Janus Graph as the underlying graph store which can be replaced by any Apache TinkerPop compliant graph store.
  - RDF to Property Graph conversion: allows storing RDF/OWL datasets in a TinkerPop compliant graph store

- https://github.com/the-qa-company/qEndpoint /java
  - A highly scalable RDF triple store with full-text and GeoSPARQL support

- https://github.com/spy16/fabric /go
  - Fabric is a triple-store written in Go. 
  - Fabric provides simple functions and store options to deal with "Subject->Predicate->Object" relations or so called triples

- https://github.com/thundergolfer/simplegraphdb /go/inactive
  - Basic Golang implementation of a Triple Store. 
  - Built to learn the Golang language before an internship.

- https://github.com/wallix/triplestore /go/inactive
  - Nifty library to manage, query and store RDF triples. 

- https://github.com/google/badwolf /go
  - BadWolf is a temporal graph store loosely modeled after the concepts introduced by the Resource Description Framework (RDF). 
  - BadWolf began as a `triplestore`, but triples have been expanded to `quads` to allow simpler and flexible temporal reasoning
  - Because BadWolf is designed for generalized relationship storage, most of the web-related idiosyncrasies of RDF are not used and have been toned down or directly removed and focuses on its time reasoning aspects.

- https://github.com/eBay/akutan /go/archived
  - a distributed knowledge graph store, sometimes called an RDF store or a triple store.

- https://github.com/lilspikey/mini-sparql /python
  - an experiment in writing a simple (in memory) triple store. 
  - It can be used to read in files or triple data, which can be queried using sparql. 
# rdf/knowledge-graph
- https://github.com/linkeddata/rdflib.js /ts-js
  - Javascript RDF library for browsers and Node.js.
  - Reads and writes RDF/XML, Turtle and N3; Reads RDFa and JSON-LD
  - Read/Write Linked Data client, using WebDav or SPARQL/Update
  - Real-Time Collaborative editing with web sockets and PATCHes
  - Compatible with RDFJS task force spec
  - SPARQL queries (not full SPARQL - just graph match and optional)

- https://github.com/comunica/comunica /ts
  - https://comunica.dev/
  - A knowledge graph querying framework
  - Flexible SPARQL and GraphQL over decentralized RDF on the Web.
# graph-db
- https://github.com/benjholla/chpg /js/java
  - CHPG is a lightweight graph database for storing property graphs (attributed, multi-relational graphs) with hierarchical and compound relationships.
# examples
- https://github.com/metasoarous/tripl /python
  - This one weird trick turns JSON documents into semantic graph databases!
  - A data format for "all the things", inspired by Datomic and the Semantic Web
  - RDF is based on the Entity Attribute Value (EAV) data modelling pattern, in which facts about entities are stored as a set of (entity, attribute, value) triples

- https://github.com/innogames/serveradmin /python
  - Serveradmin is central server database management system of InnoGames.

- https://github.com/nickapopolis/go-entity-attribute-value /go/js/inactive
  - A small entity attribute value application using a Go REST server and react front end.
  - Entity-attribute-value tables allow the dynamic creation of new data structures without need for any table migrations.
# more
