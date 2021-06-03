---
title: lib-office-remark-community
tags: [community, remark]
created: '2021-06-02T16:49:17.923Z'
modified: '2021-06-02T16:49:39.300Z'
---

# lib-office-remark-community

# pieces

- ## 

- ## 

- ## 

- ## 

- ## How to support JIRA tables? writing a plugin to convert markdown to Jira's horrible markdown syntax. 
- https://github.com/remarkjs/remark/issues/720
  - I have this implemented similar to how your strip-markdown plugin works, but i've changed the following three formatters
-  here's how i solved this. It's a hack. I copied remark-gfm entirely, then i overrode how it uses the mdast-util-gfm to customize mdast-util-gfm-table usage with a hook
- Jira is like a cousin of GFM that speaks with a weird accent. 
  - It's the same in spirit just using different control characters in some places. Summary:
  - lists, ordered lists: same
  - blockquotes: same
  - tables: nearly the same, headers have 2 bars, doesn't support alignment syntax
  - emphasis: uses _text_
  - strong: uses *text*
  - delete: uses -text-
  - horizontalRule/thematicBreak: uses ----
  - headers: h1 vs ##, ex h1. or h2.
  - code block: uses {code:language}text{code}
  - code inline: uses {{text}}
- I think copying `strip-markdown` was a wrong rabbit hole to take probably. Only dealing with serialization handlers in this case, where you‘re turning a tree into a string, seems best, as it’s made for that.
