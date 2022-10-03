---
title: lib-collab-ot-community-stars
tags: [collaboration, community, ot]
created: '2022-10-02T20:53:52.128Z'
modified: '2022-10-02T20:54:07.621Z'
---

# lib-collab-ot-community-stars

# guide

 

# discuss
- ## 

- ## 

- ## 

- ## 

- ## Collaborative Editing in ProseMirror__201508
- https://news.ycombinator.com/item?id=10002553
- Hi! Joseph Gentle here, author of ShareJS.
- You're right about OT - it gets crazy complicated if you implement it in a distributed fashion. But implementing it in a centralized fashion is actually not so bad. Its the perfect choice for google docs.
- Here is my implementation of OT for plain text
  - https://github.com/ottypes/text
  - https://github.com/josephg/appstate
  - Note that its only 400 lines of javascript, with liberal comments. 
  - To actually use OT code like that, you need to do a little bookkeeping. 
  - Its nowhere near as bad as you suggest.
- Yes, but that implementation deals only with plain text. The complexity seems to ramp up pretty quickly as you support more types of operations, and since extendability is an important concern for my project, I decided to avoid OT.
