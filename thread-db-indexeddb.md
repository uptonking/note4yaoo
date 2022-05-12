---
title: thread-db-indexeddb
tags: [db, indexeddb]
created: '2022-05-11T16:25:08.946Z'
modified: '2022-05-11T16:25:26.808Z'
---

# thread-db-indexeddb


# discuss

- ## 

- ## 

- ## 

- ## What have you used IndexDB for? Would love to hear some stories / use cases, especially for media
- https://twitter.com/wesbos/status/1384949106011934720
- My impression is that people only use it as a weird intermediate layer for offline-first applications that only occasionally sync to a reflected cloud DB. 
  - Sounds like a mess to me but I'm lucky enough to not worry about offline first for the most part
- I use it a lot as a local cache/offline mode for hash to block mappings (think git's internal database)
  - I'll often combine it with a service worker so I can expose it as normal files with GET range request support so that html5 video widgets can stream and scrub videos through it.
