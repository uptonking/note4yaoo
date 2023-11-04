---
title: toc-lib-format-json-utils
tags: [format, json, toc, utils]
created: 2022-11-06T15:45:12.591Z
modified: 2022-11-06T15:45:36.913Z
---

# toc-lib-format-json-utils

# guide
- tips
  - > also see tree; editor-render-only
  - 本地保存为文本过于灵活，易损坏格式，折中选择是本地保存为office格式如docx/xlsx
# popular
- https://github.com/streamich/json-joy
  - JSON utilities for joy and collaborative editing with OT and CRDT approaches. 

- https://github.com/panva/jose
  - "JSON Web Almost Everything" - JWA, JWS, JWE, JWT, JWK, JWKS for Node.js, Browser, Cloudflare Workers, Deno, Bun, and other Web-interoperable runtimes.

- https://github.com/gregsdennis/json-everything /c#
  - System. Text. Json-based support for all of your JSON needs.

- https://github.com/paularmstrong/normalizr
  - Many APIs, public or not, return JSON data that has deeply nested objects. Using data in this kind of structure is often very difficult for JavaScript applications, especially those using Flux or Redux.
  - Normalizr is a small, but powerful utility for taking JSON with a schema definition and returning nested entities with their IDs, gathered in dictionaries.
  - https://github.com/anseal/normalizr
    - The main point of difference from the original - performance
    - API is the same as in the original
  - forks/ts
    - https://github.com/madonoharu/ts-norm
    - https://github.com/napolab/normalizr_ts

- https://github.com/krispo/simplifr /201607/js
  - Simplifies JSON into a flat single-level path-value structure.
  - It's designed for React/Redux/Flux apps. Inspired by Normalizr.
  - We can transform the whole Redux store, that can incude complex nested json objects, into a simple flat structure using Simplifr.
  - https://github.com/krispo/redux-json-tree

- https://github.com/CondeNast/atjson /ts
  - https://atjson.condenast.io/docs/getting-started
  - atjson is a living content format for annotating content
  - we need a format that can be rich, extensible, and portable. It is important that the content source provide little ambiguity about how a story should be displayed
  - A document has a content field and a list of annotations, each of which have a spatial offset in the document.
  - atjson came out of trying to build a text editor called Poetica
# json-editor/viewer
- https://github.com/plantain-00/schema-based-json-editor
  - https://plantain-00.github.io/schema-based-json-editor/packages/react/demo/
  - A reactjs and vuejs component of schema based json editor.

- https://github.com/TexteaInc/json-viewer
  - a React component for displaying and editing JavaScript/TypeScript arrays and JSON objects.
  - https://github.com/mac-s-g/react-json-view

- https://github.com/blitlabs/online-json-diff
  - https://json-diff.com/

- https://github.com/josdejong/jsoneditor
  - A web-based tool to view, edit, format, and validate JSON

- https://github.com/json-editor/json-editor /4kStar/MIT/202310/js
  - https://json-editor.github.io/json-editor/
  - JSON Schema Based Editor

- https://github.com/b-gran/object-editor-react /js
  - https://b-gran.github.io/object-editor-react/githubExample.html
  - Schema-aware editor for structured JSON objects (drop-in React component)
# examples

# parser-generator

- https://github.com/jgranstrom/zipson /ts
  - a drop-in alternative to `JSON.parse/stringify` with added compression and streaming support.

- https://github.com/uhop/stream-json /js
  - It can parse JSON files far exceeding available memory streaming individual primitives using a SAX-inspired API.
  - `jsonl/Parser` parses a JSONL file producing objects similar to StrIt can parse JSON files far exceeding available memory.
  - a micro-library of node.js stream components with minimal dependencies for creating custom data processors oriented on processing huge JSON files while requiring a minimal memory footprint. 
  - Streaming SAX-inspired event-based API is included as well.

- https://github.com/jimhigson/oboe.js /js
  - Oboe.js is an open source Javascript library for loading JSON using streaming, combining the convenience of DOM with the speed and fluidity of SAX.

- https://github.com/WebReflection/flatted /js
  - A super light (0.5K) and fast circular JSON parser, directly from the creator of CircularJSON.

- https://github.com/nolanlawson/vuvuzela /201409/js
  - Simple and non-recursive JSON parse/stringify library
  - No functions-within-functions, just a while loop and a stack.

- https://github.com/simdjson/simdjson-java /java
  - A Java version of simdjson - a JSON parser using SIMD instructions, based on the paper Parsing Gigabytes of JSON per Second
  - Support for Unicode characters
  - Full support for parsing floats
  - Support for 512-bit vectors

- https://github.com/Breus/json-masker /java
  - used to mask string and/or numeric values from JSON messages, corresponding to a (set of) target key(s). 
  - The implementation is focused on maximum (time) performance using Java and requires no additional runtime dependencies.
# diff
- https://github.com/zgrossbart/jdd /js
  - JSON Diff expands on the amazing work by the team at jsonlint.com and provides a semantic compare tool for JSON documents.
  - JSON Diff sorts, formats, and compares two JSON documents to find the actual semantic differences instead of just the text ones.
# merge
- https://github.com/avian2/jsonmerge /python
  - merge a series of JSON documents into a single one
  - We call the document we are merging changes into base and the changed document head. 
  - jsonmerge by default returns fields that appear in either base or head document. For other JSON types, it simply replaces the older value. These principles are also applied in case of multiple nested JSON objects.
# utils
- https://github.com/datavis-tech/json-templates
  - Simple templating within JSON structures
  - `parse("{{foo.value:baz}}")`

- https://github.com/RedisJSON/RedisJSON /rust
  - https://redis.io/docs/stack/json/
  - RedisJSON is a Redis module that implements ECMA-404 The JSON Data Interchange Standard as a native data type. 
  - It allows storing, updating and fetching JSON values from Redis keys (documents).
  - JSONPath syntax for selecting elements inside documents
  - Documents are stored as binary data in a tree structure, allowing fast access to sub-elements
# more
- [JSON Merge Strategies: 2-way, 3-way Merges and Graft - DeltaXML](https://www.deltaxml.com/blog/json/json-merge-strategies/)
  - To combine the information in two JSON files – simple JSON Data Merge
  - Merging Changes between JSON files
  - If we make the changes we want in one of the files, can we use merge to apply those changes to the other file? The answer is yes, and it is a merge very similar to the one described above but it is not quite the same. A name given to this particular type of merge in some source code control systems is ‘graft’, i.e. we graft the changes from one branch onto another branch
