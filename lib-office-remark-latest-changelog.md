---
title: lib-office-remark-latest-changelog
tags: [changelog, remark]
created: '2021-06-03T15:57:32.197Z'
modified: '2021-06-03T15:58:30.094Z'
---

# lib-office-remark-latest-changelog

# guide

# changes

## remark.v13.0.0__202010

- This is a giant change for remark. 
  - It replaces the 5+ year old internals with a new low-level parser: micromark.
  - The old internals have served billions of users well over the years, but markdown has changed over that time.
  - micromark comes with 100% CommonMark (and GFM as an extension) compliance

- remark-parse
  - `remark-parse` now defers its work to `micromark` and mdast-util-from-markdown.
  - `from-markdown` turns its tokens into the previously (and still) used syntax tree: mdast. 
  - Extensions to remark-parse work differently: they’re a two-part act.

- remark-stringify
  - remark-stringify now defers its work to mdast-util-to-markdown
  - It’s a new and better serializer with powerful features to ensure serialized markdown represents the syntax tree (mdast), no matter what plugins do. 
  - Extensions to it work differently

- Changes to output/the tree
  - All of these are for CommonMark compatibility. 

- [pr: Change to use micromark](https://github.com/remarkjs/remark/pull/536)
# changelog
