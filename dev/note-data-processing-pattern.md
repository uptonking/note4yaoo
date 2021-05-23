---
title: note-data-processing-pattern
tags: [data, data-processing, pattern]
created: '2021-05-23T17:09:35.689Z'
modified: '2021-05-23T17:10:01.846Z'
---

# note-data-processing-pattern

# guide

# blogging

## [Frictionless Data Lib - A Design Pattern for Accessing Files and Datasets](http://okfnlabs.org/blog/2018/02/15/design-pattern-for-a-core-data-library.html)

- The pattern is focused on access and use of:
  - individual files (streams)
  - collections of files (“datasets”)
- It defines a standardized “stream-plus-metadata” interface for file and dataset objects, along with methods for creating these from file or dataset pointers such as file paths or urls.

- The pattern is based on the following principles:
  - Data wrangler focused: focus on the core data wrangler workflow: open a file and do something with it
  - Zen-like: Simplicity and power. As simple as possible: does just what it needs and no more.
  - Use Streams: stream focused library, including object streams (aka iterators).
