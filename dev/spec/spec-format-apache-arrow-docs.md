---
title: spec-format-apache-arrow-docs
tags: [apache-arrow, docs, format, spec]
created: 2021-07-24T08:15:26.155Z
modified: 2021-07-24T08:17:55.019Z
---

# spec-format-apache-arrow-docs

# guide

# overview

# [Feather File Format](https://arrow.apache.org/docs/python/feather.html)
- Feather is a portable file format for storing Arrow tables or data frames (from languages like Python or R) that utilizes the Arrow IPC format internally. 
  - Feather was created early in the Arrow project as a proof of concept for fast, language-agnostic data frame storage for Python (pandas) and R. 

- [Status of JS reader for feather files](https://github.com/wesm/feather/issues/308)
  - The recommended path for JavaScript is to use the Arrow IPC protocol which is supported and integration tested in JavaScript and being used in a variety of places (finos/perspective is a good example)
