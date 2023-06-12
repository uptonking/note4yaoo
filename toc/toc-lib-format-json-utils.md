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

- https://github.com/json-editor/json-editor /js
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
# utils
- https://github.com/datavis-tech/json-templates
  - Simple templating within JSON structures
  - `parse("{{foo.value:baz}}")`
# more
