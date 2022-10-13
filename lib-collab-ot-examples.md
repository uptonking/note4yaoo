---
title: lib-collab-ot-examples
tags: [collaboration, examples, ot]
created: 2022-10-02T20:50:54.901Z
modified: 2022-10-02T20:51:30.444Z
---

# lib-collab-ot-examples

# guide

- [I'm looking for a library that would allow me to synchronize text in real-time between multiple users (ala Google Docs).](https://stackoverflow.com/questions/2043165)
# popular
- https://github.com/Progyan1997/Operational-Transformation
  - http://operational-transformation.github.io/
  - A collection of Algorithms to Synchronise changes across multiple clients using Operational Transformation
# ot-rewrite
- https://github.com/vitotafuni/JSOTTEST
  - http://vitotafuni.github.io/jsottest/
  - a simple simulator for Operational Transformation algorithms written in JavaScript.

- https://github.com/Operational-Transformation/ot.js /js
  - http://operational-transformation.github.io/
  - Visualization of OT with a central server
  - Requires CodeMirror >= 4.0
  - [Operational Transformation in JavaScript](http://operational-transformation.boltdoggy.com/ot-for-javascript.html)
  - https://github.com/YingshanDeng/ot.js-demo
  - https://github.com/abucraft/operational-transform

- https://github.com/ottypes/text-unicode /ts
  - This OT type can be used to edit plaintext documents, like sourcecode or markdown. 
  - text-unicode counts positions based on the number of unicode codepoints instead of javascript string length (UCS2 2-byte offsets). 
- https://github.com/ottypes/text  /js
  - This OT type can be used to edit plaintext documents, like sourcecode or markdown.
  - This OT type counts characters using UTF16 offsets instead of unicode codepoints. 
  - This is slightly faster in javascript, but its incompatible with ot implementations in other languages. 

- https://github.com/ottypes/json1 /ts
  - JSON1 implements a superset of JSON0's functionality.
  - an operational transformation type for arbitrary JSON trees. It supports concurrently editing arbitrarily complex nested structures.
  - Support for arbitrarily moving objects in the JSON tree. 
  - Supports embedded subtypes, like embedding rich text documents using quilljs or something inside your JSON tree
  - can be configured to reject operations which would result in lost data.
  - JSON0 and JSON1 use different embedded string types. 
    - JSON1 uses text-unicode which uses proper unicode offsets. 
    - JSON0 uses the older text type which uses UTF16 pair offsets. 
    - These are normally the same, but notably differ when embedding emoji characters.
  - limitations
    - Your document must only contain pure JSON-stringifyable content. No dates, functions or self-references allowed. Your object should be identical to JSON.parse(JSON.stringify(obj)).
- https://github.com/ottypes/json0 /js
  - The JSON OT type can be used to edit arbitrary JSON documents.
  - JSON0 is an invertable type - which is to say, all operations have an inverse operation which will undo the original op. 
    - As such, all operations which delete content have the content to be deleted inline in the operation.
  - Embedded string editing, using the old text0 OT type as a subtype
  - limitations
    - doesn't support moves between object keys
    - doesn't support moving child values from one object to another
    - Set if null (object insert with first writer wins semantics)
    - Efficient list insert-of-many-items

- https://github.com/yiminghe/ot-engine
  - https://ot-engine-rich-text.herokuapp.com/
  - Operational transformation engine
  - 示例使用quill
  - support presence(cursors)
  - support local undo/redo

- https://github.com/josephg/appstate
  - This is a little toy prototype exploring the idea that each client shares a single JSON object with the server. 
  - Both the client and the server can read & edit the session object using OT. 
  - The object has all the data the client needs to know to run the app.

- https://github.com/tOkeshu/ot.js /js/2013
  - ot.js is a pure JavaScript library to work with operational transformations.

- https://github.com/otjs/ot /js
  - A line-based operational transform algorithm

- https://github.com/cricklet/operational-transform-demo
  - http://cricklet.github.io/sites/blue/index.html
  - an implementation/demo of collaborative text editing via operational transforms.
  - https://github.com/fitzgen/operational-transformation

- https://github.com/fitzgen/operational-transformation-example
  - an implementation of a real time collaborative document editor which uses my Operational Transformation library.

- https://github.com/rclarey/simple-ot
  - A simple operational transform library that uses the domain-agnostic GOTO control algorithm.
  - https://github.com/rclarey/cloudcode

- https://github.com/kizahasi/ot-string
  - Operational Transfomation library for string.

- https://github.com/Jaeyo/Operational-Transformation-Example
  - Operational Transform Example with node.js
  - 直接在控制台测试，无需server

- https://github.com/hanupratap/Operational-Transform
  - Operational Transform algorithm used by google Docs
  - https://github.com/kshitij86/operational_transform
# ot-examples
- https://github.com/GarinZ/collaborative-textarea
  - 支持协作编辑的文本框
  - A text area supporting real-time collaborative editing plain text. And display all the online attendees.
  - 依赖 reduxjs/toolkit、iff-match-patch
  - [如何实现协同编辑 - 理解Operational Transformation](https://garinzhang.com/coding/how-to-implemente-collaborative-editing-understanding-operational-transformation.html)

- https://github.com/YingshanDeng/SharedPen
  - A (web-based) rich-text real-time collaborative editor using CodeMirror and ot.js
  - [SharedPen 之 Operational Transformation](http://objcer.com/2018/03/05/SharePen-Operational-Transformation/)
# ot-utils
- https://github.com/kbadk/json0-ot-diff
  - Finds differences between two JSON object and generates operational transformation (OT) operations for transforming the first object into the second according to the JSON0 OT Type.

- https://github.com/slevental/operational-transformation /java
  - a reference implementation for OT protocol described introduced in Google Wave and described in their documentation
- https://github.com/Fleischers/OT_example /java
  - simple local console implementation of Operational Transformation
