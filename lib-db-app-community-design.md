---
title: lib-db-app-community-design
tags: [community, database, design]
created: 2023-09-17T17:50:30.020Z
modified: 2023-09-17T17:50:49.932Z
---

# lib-db-app-community-design

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 
# discuss-markdown/ooxml/epub-db
- ## 

- ## 

- ## 💡 [Athens Research (YC W21) – Open-Source Roam Research | Hacker News_202103](https://news.ycombinator.com/item?id=26316793)
- My only real reservation is that files are not in Markdown.
- 👉🏻 The current **major difference between markdown-based and db-based apps is block references**. Over time, the difference will become significant as knowledge bases grow in size.
  - CSV -> Excel -> SQL -> Distributed Cloud DBs
  - Furthermore, our database supports data types, including numbers, dates, etc. I don't think any networked notetaking app has executed well on tables and non-string types. UX for tables is generally not great for markdown.
- That should be true, but so far it is Roam with the biggest problems with performance, from 30+ seconds of loading each time you load/refresh tab to constant lags in normal usage for some users
  - I personally like the most this mixed approach of Logseq - app internally uses DataScript, but data is ultimately stored in plain files.

- Roam's performance suffers mainly on first-load because they are server-first, and they load the entire db into memory at the beginning (such that it's quite fast thereafter).
  - Once we have true local-first data structures with something like https://github.com/replikativ/datahike, we could still have fast in-memory, but also fast initial load.

- 👉🏻 Not markdown, but **asciidoc has first class support for blocks and references/attributes**.

- I don't see the advantage of converting an HTML to RDF because it would cover the entire spectrum. All the semantics might be lost. RSS is the smallest common denominator. If you agree somehow, you might be interested in that tool [0], it converts HTML to RSS using pattern matching.

- Me and some friends have played around with Roam a bit and we are baffled by the app. It just does not work well. It is a badly-designed, lower performance, glitchy note-taking app. You end up staring at its gaudy giant astrolabe loading spinner more often than not. We look at it and end up baffled why anyone would pay a monthly subscription for it!

- Could you please share some of your experience/plans regarding implementing cross-device sync?
- Which db is the source of truth?
  - Currently index.transit is the source of truth. When a user sees new changes, their current db is saved, and they have the option of opening the new one or continuing to edit the current version. The entire history of the db is saved right now ({timestamp}-username.index.transit.bkp) while we work on better conflict resolution and merging
- How will conflicts from offline editing be handled?
  - Don't have conflict resolution yet for offline editing
- Will you be able to see edits made in realtime across the devices?
  - We plan to make a websocket server for some the real-time UX.
# discuss
- ## 

- ## 

- ## 

- ## 和ChatGPT聊DB设计获得新知，Nested Set Model：
- https://twitter.com/TooooooBug/status/1659041013800001536
  - 将父子关系映射到数轴上变为数字范围的包含关系，然后通过数字范围大小就能计算出各条记录的父子关系，避免反复递归。
