---
title: lib-db-model-eav-examples
tags: [database, entity-attribute-value, examples, toc]
created: 2023-09-25T17:56:12.065Z
modified: 2023-09-25T17:56:50.116Z
---

# lib-db-model-eav-examples

# guide

# eav
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

- https://github.com/ssledz/eav-model-pattern /201502/java/inactive
  - EAV is also known as object–attribute–value model, vertical database model and open schema.
# triple-store
- https://github.com/spy16/fabric /go
  - Fabric is a triple-store written in Go. 
  - Fabric provides simple functions and store options to deal with "Subject->Predicate->Object" relations or so called triples

- https://github.com/google/badwolf /go
  - BadWolf is a temporal graph store loosely modeled after the concepts introduced by the Resource Description Framework (RDF). 
  - BadWolf began as a `triplestore`, but triples have been expanded to `quads` to allow simpler and flexible temporal reasoning
  - Because BadWolf is designed for generalized relationship storage, most of the web-related idiosyncrasies of RDF are not used and have been toned down or directly removed and focuses on its time reasoning aspects.

- https://github.com/eBay/akutan /go/archived
  - a distributed knowledge graph store, sometimes called an RDF store or a triple store.
# rdf
- https://github.com/linkeddata/rdflib.js /ts-js
  - Javascript RDF library for browsers and Node.js.
  - Reads and writes RDF/XML, Turtle and N3; Reads RDFa and JSON-LD
  - Read/Write Linked Data client, using WebDav or SPARQL/Update
  - Real-Time Collaborative editing with web sockets and PATCHes
  - Compatible with RDFJS task force spec
  - SPARQL queries (not full SPARQL - just graph match and optional)
# more
