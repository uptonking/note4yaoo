---
title: toc-office-draw-annotation
tags: [annotation, drawing, office, toc]
created: 2023-11-03T17:42:38.566Z
modified: 2023-11-03T17:43:01.518Z
---

# toc-office-draw-annotation

# guide
- 画板或批注类产品要参考规范 [Web Annotation Data Model](https://www.w3.org/TR/annotation-model/)
  - 富文本格式也可参考
# whiteboard

# annotation

- https://github.com/apache/incubator-annotator /apache2/ts
  - https://annotator.apache.org/
  - provides annotation enabling code for browsers, servers, and humans.
  - The goal is to help developers of annotation tools create their applications without having to reinvent the wheel, while applying a standards-driven approach based on the W3C’s Web Annotation data model, in order to facilitate an ecosystem of interoperable annotation tools 
  - [Web Annotation Protocol Server](https://github.com/apache/incubator-annotator/issues/70)

- https://github.com/goodmansasha/annotation-model /js
  - https://goodmansasha.github.io/annotation-model/
  - Javascript implementation of the W3C Web Annotation Data Model, useful for Web Extensions and serializing references to specific resources on a HTML page

- https://github.com/openannotation/annotator /js
  - http://annotatorjs.org/
  - Annotation tools for the web. Select text, images, or (nearly) anything else, and add your notes.
  - It provides a set of interoperable tools for annotating content in webpages.

- https://github.com/hypothesis/pdf.js-hypothes.is /js
  - https://web.hypothes.is/
  - This is a copy of Mozilla's PDF.js viewer with Hypothesis annotation tools added.

## anno-server

- https://github.com/jankaszel/simple-annotation-server /MIT/202007/js/inactive
  - simple annotation server intended for testing purposes, implementing both the Web Annotation Protocol as well as the Web Annotation Data Model with simple REST-based user management. 
  - The server is written in JavaScript and runs in Node.js, running an in-process LevelDB database.

- https://github.com/BigBlueHat/anno-proto-coucho /201610/js
  - Web Annotation Protocol Server built on Apache CouchDB
  - Apache CouchDB's HTTP API is quite similar to the Web Annotation Protocol except the later is specific to Annotation.
# more
