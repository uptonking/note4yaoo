---
title: toc-lib-format-xml-html
tags: [format, html, ooxml, toc, xml]
created: 2023-03-01T15:04:29.279Z
modified: 2023-09-19T07:24:15.040Z
---

# toc-lib-format-xml-html

# guide

# popular

# examples

# parser-generator
- https://github.com/isaacs/sax-js /js
  - A sax-style parser for XML and HTML.
  - 支持浏览器和nodejs
  - A very simple tool to parse through an XML string.
  - A stepping stone to a streaming HTML parser.

- https://github.com/snappyjs/node-xml-stream /js
  - A tiny simple and fast XML/HTML stream parser with an easy-to-use interface (using NodeJS streams)
  - It is a perfect match for use in feed parsers (e.g. ATOM/RSS/RDF)
  - If you need a parser that is more heavy-weight with more functionality I recommend node-sax-js

- https://github.com/lddubeau/saxes /ts
  - A sax-style non-validating parser for XML.
  - 支持浏览器和nodejs
  - Saxes is a fork of sax 1.2.4. 
  - saxes does not support HTML, or pseudo-XML, or bad XML
  - There's no Stream API. A revamped API may be introduced later. (It is still a "streaming parser" in the general sense that you write a character stream to it.)
# extension-superset

# stream
- https://github.com/cloudflare/lol-html /rust
  - Low Output Latency streaming HTML rewriter/parser with CSS-selector based API.
  - It is designed to modify HTML on the fly with minimal buffering. 
  - It can quickly handle very large documents, and operate in environments with limited memory resources. 

- https://github.com/worker-tools/html
  - HTML templating and streaming response library for Worker Runtimes such as Cloudflare Workers.
  - This library is using tagged template strings to create streaming response bodies on the fly, using no special template syntax and giving you the full power of JS for composition.
# utils

# more
