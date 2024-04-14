---
title: lib-editor-quill-community-storage
tags: [community, quill, storage]
created: 2023-11-27T15:56:38.083Z
modified: 2023-11-27T15:57:01.179Z
---

# lib-editor-quill-community-storage

# guide

# discuss-stars
- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## 

- ## [which format of content should be stored into database postgresql? _201904](https://github.com/quilljs/quill/issues/2590)
- You should store the Delta returned from getContents(). 

- ## 💡 [Proposal: (Doc) write about **the correct way** to store & display quill editor content _201808](https://github.com/quilljs/quill/issues/2276)
- There are 2 way to store and then display content when using quill editor to write content.
  - (Delta) Store Delta into database (MySQL/PostgreSQL as JSON). then, when Display, use some library convert Delta to HTML and then display
  - (HTML) Store HTML using `quill.root.innerHTML` into database (MySQL/PostgreSQL) and then just Display these HTML

- HTML from users is unsafe. Best way is to store Delta in the database and render it to HTML if needed.

- In case anyone comes across this and finds this useful. You don't need to use innerHTML to render the delta, you can instantiate a new quill object with the settings of readonly and no toolbar
