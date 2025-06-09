---
title: thread-lang-js-code-doc
tags: [docs, lang-js, typescript]
created: 2025-04-19T10:42:51.351Z
modified: 2025-04-19T10:43:17.651Z
---

# thread-lang-js-code-doc

# guide

- code-doc-solutions
  - [JSDoc](https://jsdoc.app/about-getting-started)
  - [TSDoc is a proposal to standardize the doc comments used in TypeScript code](https://tsdoc.org/)
  - [TypeDoc converts comments in TypeScript's source code into HTML documentation or a JSON model](https://typedoc.org/)
# docs

## jsdoc

## tsdoc

- TSDoc is a proposal to standardize the doc comments used in TypeScript code, so that different tools can extract content without getting confused by each other's markup. 

- 🤔 Why can't JSDoc be the standard? 
  - The JSDoc grammar is not rigorously specified, but rather inferred from the behavior of a particular implementation. 
  - The majority of the standard JSDoc tags are preoccupied with providing type annotations for plain JavaScript, which is not a primary concern for a strongly-typed language such as TypeScript.

- 
- 
- 

# discuss-stars
- ## 

- ## 

- ## 
# discuss-ts-toc
- ## 

- ## 

- ## [Hover documentation for typescript uses jsdoc rules and not tsdoc · Issue · microsoft/vscode _202504](https://github.com/microsoft/vscode/issues/246952)
  - Write some typescript code and use the syntax required by tsdoc
  - Observe that hover documentation and highlighting completely ignore tsdoc and instead assume parity with jsdoc

# discuss
- ## 

- ## 

- ## [TSDoc, relevant? : r/typescript _201809](https://www.reddit.com/r/typescript/comments/9ikuq7/tsdoc_relevant/)
- The TSDoc format states the following goals:
Design a grammar for TypeScript while extending JSDoc

Allow Markdown within comments

A common set of documentation tags

Extensible mechanism for adding tags

Interoperable, so custom tags won’t break parsing of non-custom tags and handling Markdown ambiguities

Cross-referencing between packages and dependencies

Open standard

- Additionally, the TSDoc reference parser also aims to provide:

Strict and lax modes, with lax attempting to parse existing JSDoc-based grammar

Bi-directional round-tripping between doc comments and abstract syntax trees

Self-contained, no dependency on the TypeScript compiler API, allowing the abstract syntax tree for comments to be a simple JavaScript object tree

- TypeScript developers should expect that JSDoc type annotations that are redundant with type information already provided > by TypeScript be optional with TSDoc.
