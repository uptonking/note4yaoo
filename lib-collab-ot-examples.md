---
title: lib-collab-ot-examples
tags: [collaboration, examples, ot]
created: '2022-10-02T20:50:54.901Z'
modified: '2022-10-02T20:51:30.444Z'
---

# lib-collab-ot-examples

# guide

# popular

# ot-rewrite

- https://github.com/ottypes/text-unicode
  - This OT type can be used to edit plaintext documents, like sourcecode or markdown. 
  - It allows invertible or non-invertible text operations.
- https://github.com/josephg/appstate
  - This is a little toy prototype exploring the idea that each client shares a single JSON object with the server. 
  - Both the client and the server can read & edit the session object using OT. 
  - The object has all the data the client needs to know to run the app.

- https://github.com/ottypes/text  /js
  - This OT type can be used to edit plaintext documents, like sourcecode or markdown.
  - This OT type counts characters using UTF16 offsets instead of unicode codepoints. This is slightly faster in javascript, but its incompatible with ot implementations in other languages. 
