---
title: lib-db-triplitdb-dev
tags: [database, triplitdb]
created: 2023-10-11T21:36:32.775Z
modified: 2023-10-11T21:37:11.168Z
---

# lib-db-triplitdb-dev

# guide

- triplit-pros
  - triplit supports relational-style querying system without joins
  - no schema, flexible data for triple store
  - supports flexible storage adapter including sqlite
  - Partial replication (this is a big one)
  - Support for an authoritative server 
  - Provides an optional hosted cloud service 
  - Relational querying without SQL 
  - Typescript schemas and type hinting in queries in return types

- triplit-cons
  - js only, no implementation for other language

- sqlite-pros
  - popular with ecosystem
  - sql is supported everywhere
  - support full text search

- sqlite-cons
  - sqlite has no builtin support for reactivity
  - sqlite-wasm is hard to bundle
  - sqlite has too many feathers u might not need
  - for web, sqlite is slow for multiple layers of abstraction

- resources
  - [why we need a full-stack database - Lofi Meetup #7_202308](https://www.youtube.com/watch?v=SEB-hF1F-UU&list=PLTbD2QA-VMnXFsLbuPGz1H-Najv9MD2-H&t=1471s)
  - [Taking Node Server to the next level - pouchdb vs sql_201911](https://groups.google.com/g/TiddlyWiki/c/BtmLkx1mwtU)
# dev

# examples

- https://github.com/mweidner037/list-demos/tree/master/triplit-quill
  - Basic collaborative rich-text editor that synchronizes using the Triplit fullstack database. 
  - The editor is Quill.
  - https://discord.com/channels/1138467878623006720/1195033937026752522/1195033937026752522
    - I am working on some libraries to support CRDT-style rich-text editing on top of more traditional databases. Here is a demo using Triplit
    - I realize that this is a bit silly (e.g. it's storing one DB row per character - a lot of overhead), but I hope it is useful as a proof-of-concept.
  - https://twitter.com/matthew_linkous/status/1745542657890300384
    - It combines @triplit_dev @quilljs and Matt's library (https://github.com/mweidner037/list-positions) which is based on the Fugue CRDT that he and @martinkl invented
# more
