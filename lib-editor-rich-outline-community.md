---
title: lib-editor-rich-outline-community
tags: [community, outline-wiki]
created: 2021-09-09T18:30:39.033Z
modified: 2021-09-09T18:31:03.467Z
---

# lib-editor-rich-outline-community

# guide

# issues
- ## 

- ## 📈 [Add Notion-like inline databases · outline/outline _202402](https://github.com/outline/outline/discussions/6507)
- If we could attach NocoDB as a plugin, and in every row of the table, add a hidden column which links to an Outline page, we could have a bidirectional sync between Outline and NocoDB.

- I think Outline already supports Grist too, but which low-code DB module is less of a point. The point is that ANY good enough low-code DB should have some tighter integration with Outline. So we can be more creative with documents.

- ## 🌲 [Move to sending JSON rather than Markdown to client](https://github.com/outline/outline/issues/3000)
- 数据库保存的是markdown内容文本，服务端发给客户端的是字符串而不是json

- The format already exists, it's what the Markdown gets parsed into. It also exists inside the CRDT in the database which contains the collaborative state of any given document

- [pr已合并: JSON to client _20240524](https://github.com/outline/outline/pull/5553)

- ### This took many months of effort to move away from Markdown as @getoutline 's  canonical data storage, so that features like this can finally be built. _202406
- https://x.com/tommoor/status/1798382428844913012
- Is this using the same infra as Linear's new table?
  - Both are built on ProseMirror, other than that the implementations are different actually
  - outline has source code available if you want to dig through its table implementation
# discuss
- ## 

- ## 

- ## 

- ## 
# discuss-collab
- ## 

- ## 

- ## 

- ## [Collaborative editing · Pull Request log](https://github.com/outline/outline/pull/1660)
