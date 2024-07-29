---
title: lib-editor-codemirror-dev-diff
tags: [codemirror, diff, json-patch]
created: 2024-07-29T11:49:17.052Z
modified: 2024-07-29T11:49:33.248Z
---

# lib-editor-codemirror-dev-diff

# guide

# diff-formats

## [nbdime jupyter](https://nbdime.readthedocs.io/en/latest/diffing.html)

- nbdime – diffing and merging of Jupyter Notebooks
  - Jupyter notebooks are useful, rich media documents stored in a plain text JSON format. 
  - However, primitive line-based diff and merge tools do not handle well the logical structure of notebook documents
  - nbdime provides “content-aware” diffing and merging of Jupyter notebooks.
- A diff object represents the difference B-A between two objects, A and B, as a list of operations (ops) to apply to A to obtain B
- The diff objects in nbdime are: 
  - json-compatible nested structures of dicts (with string keys) 
  - and lists of values with heterogeneous(不同种类的) datatypes (strings, ints, floats)

- nbdime vs json-patch
- operations
  - JSONPatch contains operations move, copy, test not used by nbdime.
  - nbdime contains operations addrange, removerange, and patch not in JSONPatch.
- patch 
  - JSONPatch uses a deep JSON pointer based path item in each operation instead of providing a recursive patch op
  - nbdime uses a key item in its patch op.
- diff object
  - JSONPatch can represent the diff object as a single list.
  - nbdime uses a tree of lists.

- nbdime implements a three-way merge of Jupyter notebooks and a subset of generic JSON objects.

- A merge operation with a shared origin object base and modified objects, local and remote, outputs these merge results:
  - a fully or partially merged object
  - a set of merge decision objects that describe the merge operation

- Each three-way notebook merge is based on the differences between the base version and the two changed versions – local and remote. These differences, ``base`` with local and base with remote, are then compared, and for each change a set of decisions are made. A merge decision object represents such a decision, and is represented as a dict with the following entries

- 
- 
- 
- 

# discuss
- ## 

- ## 

- ## 

- ## 
