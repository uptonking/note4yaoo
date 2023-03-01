---
title: toc-lib-format-json-utils
tags: [format, json, toc, utils]
created: 2022-11-06T15:45:12.591Z
modified: 2022-11-06T15:45:36.913Z
---

# toc-lib-format-json-utils

# guide

# popular
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
# examples
- https://github.com/TexteaInc/json-viewer
  - a React component for displaying and editing JavaScript/TypeScript arrays and JSON objects.
  - https://github.com/mac-s-g/react-json-view
# parser-generator
- https://github.com/uhop/stream-json
  - It can parse JSON files far exceeding available memory streaming individual primitives using a SAX-inspired API.
  - `jsonl/Parser` parses a JSONL file producing objects similar to StrIt can parse JSON files far exceeding available memory. eamValues
  - a micro-library of node.js stream components with minimal dependencies for creating custom data processors oriented on processing huge JSON files while requiring a minimal memory footprint. 
  - Streaming SAX-inspired event-based API is included as well.

- https://github.com/WebReflection/flatted /js
  - A super light (0.5K) and fast circular JSON parser, directly from the creator of CircularJSON.
# more
