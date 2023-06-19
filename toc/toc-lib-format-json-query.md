---
title: toc-lib-format-json-query
tags: [format, json, query, toc]
created: 2023-05-12T02:04:05.415Z
modified: 2023-05-12T02:04:52.918Z
---

# toc-lib-format-json-query

# guide
- ## [Add consideration to JSON Pointer and JSON Path](https://github.com/opengeospatial/architecture-dwg/issues/15)
- JSON pointer
  - This specification defines JSON Pointer, a string syntax for identifying a specific value within a JSON document. 
  - JSON Pointer is intended to be easily expressed in JSON string values as well as URI fragment identifiers.
  - `/foo/0` single value

- JSON path
  - Like XMLPath.
  - More expresive
  - Not an standard
  - `['foo'][0]` single value
  - `$.store.book[?(@.price < 10)].title` multi value
# popular
- sift.js /1.6kStar/MIT/202211/ts
  - https://github.com/crcn/sift.js
  - Use Mongodb queries in JavaScript
  - Supports node.js, and web

- https://github.com/protobi/query /202205/js/singleFile
  - lightweight API to query Javascript arrays using MongoDB syntax in the browser and Node.js.
  - This module originated as a proprietary module for Protobi core, implementing MongoDB syntax for Javascript data arrays.
  - This API matches much of underscore-query's documentation, and the code passes most of unit tests in the `underscore-query` module.

- https://github.com/aykutkardas/Json-Function /ts
  - It allows you to use methods such as schema, innerJoin, where, limit, select, orderBy on JSON data.

- https://github.com/sanity-io/GROQ /js
  - This is the specification for GROQ (Graph-Relational Object Queries), 
  - a query language and execution engine made at Sanity.io, for filtering and projecting JSON documents. 

- https://github.com/lgandecki/modifyjs /201803/js
  - Modify your objects with a mongo like syntax. 
  - This is based on a modify function of Meteor's brilliant minimongo package, cleaned up, rewritten to es6, changed to work without Meteor context
  - rxdb crdt使用
# jsonpath
- who is using #jsonpath
  - [Amazon States Language](https://states-language.net/spec.html)

- https://github.com/JSONPath-Plus/JSONPath /202209/js
  - https://jsonpath-plus.github.io/JSONPath/demo/
  - Analyse, transform, and selectively extract data from JSON documents (and JavaScript objects).
  - This project is not currently being actively maintained. 
  - Compliant with the original jsonpath spec
  - additions or elaborations not provided in the original spec:
    - ^ for grabbing the parent of a matching item
    - Type selectors for obtaining json types/compound types

- https://github.com/ashphy/jsonpath-online-evaluator
  - https://jsonpath.com/
  - A playground for JSONPath

- https://github.com/dchester/jsonpath /202104/js/inactive
  - Query and manipulate JavaScript objects with JSONPath expressions. 
  - Robust JSONPath engine for Node.js.

- https://github.com/json-path/JsonPath /java
  - Java JsonPath implementation
  - A Java DSL for reading JSON documents.

- https://github.com/dvdln/jsonpath-object-transform
  - Transform an object literal using JSONPath.
# json pointer
- who is using #json-pointer
  - json-patch
  - kubernetes

- https://github.com/whitlockjc/json-refs /201904/js
  - library for interacting with JSON References and JSON Pointers. 
  - While the main purpose of this library is to provide JSON References features, since JSON References are a combination of Object structure and a JSON Pointer, this library also provides some features for JSON Pointers as well.

- https://github.com/flitbit/json-ptr /ts
  - A complete implementation of JSON Pointer (RFC 6901) for nodejs and modern browsers.

- https://github.com/janl/node-jsonpointer /js
  - an implementation of JSON Pointer.

- https://github.com/APIDevTools/json-schema-ref-parser
  - a full JSON Reference and JSON Pointer implementation that crawls even the most complex JSON Schemas and gives you simple, straightforward JavaScript objects.
# more
- https://github.com/jsonata-js/jsonata /202302/js/ibm/xpath
  - https://jsonata.org/
  - Reference implementation of the JSONata query and transformation language.
  - Lightweight query and transformation language for JSON data
  - Inspired by the location path semantics of XPath 3.1
  - Format query results into any JSON output structure
  - forks
    - https://github.com/Stedi/jsonata

- https://github.com/jmespath/jmespath.js /202201/js/inactive
  - Javascript implementation of JMESPath, a query language for JSON

- https://github.com/evinism/mistql
  - A query / expression language for performing computations on JSON-like structures. 
  - Tuned for clientside ML feature extraction.

- https://github.com/jiren/JsonQuery /201502/js
  - Query your JSON data like database.
# discuss
- ## [JavaScript Object Notation (JSON) Pointer (2013) | Hacker News](https://news.ycombinator.com/item?id=35545384)
- I was wondering how this differs from JSONPath
  - jsonpointer just defines how to access to a single value inside a json document, whereas jsonpath has more powerful features like union (extract multiple values), filters and deep search (recursively match a path).
  - jsonpath is missing a proper specification, so some behaviors are implementation specific with some parts heavily depending on some javascript constructs (mainly filters).

- JSON Pointer is just not powerful enough except for the simplest use cases. I very much prefer JSON Path.

- ## [Interesting that they're using JSONPath, which isn't even specified formally anywhere... | Hacker News](https://news.ycombinator.com/item?id=13093607)
- The only other major implementor that I know about is Kubernetes, which has some odd extensions for templating. (JSONPath itself, of course, isn't very well designed in the first place.)
- 💡 Perhaps the most formally specified JSON-addressing dense declarative syntax is JSON Pointer (RFC 6901), but it's very limited: 
  - it only has exact index selectors, an end-of-array selector, and an exact object name selector. 
  - Still, given how JSON-Patch (RFC 6902) depends on it, it may be worthwhile to pursue a notation that extends it formally.
- IBM JSONata is another open source alternative. 
  - seems like a good alternative to XPath

- ## [Jsonpath – a query language for JSON in Postgres [pdf] | Hacker News_201905](https://news.ycombinator.com/item?id=19949240)
- Also of interest is RFC 6901, JSON Pointer 
  - That spec is much simpler (and syntactically incompatible, I may add), providing unique paths to elements inside a JSON document, and not handling any sorts of queries, as these Jsonpath and JSONPath things both do.
- JSON Pointer is not ubiquitous by any means, but it does got use in diverse APIs. Most recently, JMAP uses it for backreferences.

- another alternative is jsonata, backed by IBM

- ## 

- ## 

- ## 
