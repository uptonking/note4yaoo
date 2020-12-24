---
title: thread-frontend-web
tags: [frontend, web]
created: '2020-12-05T07:43:47.005Z'
modified: '2020-12-05T07:44:12.022Z'
---

# thread-frontend-web

## pieces

- if I was building a CMS using MongoDB would you tell me to stop immediately? If so, why?
  - https://twitter.com/JakeDohm/status/1341892219511459842
  - Every developer build a CMS at some point in their career. 
    - Might as well check it off of your bucket list.
  - I’m going to get technical and ask what type of content your CMS would be housing. 
  - That would determine DB for me. 
  - Mongo doesn’t seem appropriate for most content I’ve worked with, as CMS tends to be highly relational.
  - Maker me: Build whatever you want with whatever tools you want.
  - Developer me: Don't use MongoDB, most of your stuff with be relational, 
    - and in the event you cannot use relational, use JSONB data type in PostgreSQL.
