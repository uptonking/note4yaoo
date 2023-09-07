---
title: lib-draw-app-community-collab
tags: [collaboration, community, drawing, whiteboard]
created: 2023-09-07T04:18:07.542Z
modified: 2023-09-07T04:18:42.020Z
---

# lib-draw-app-community-collab

# guide

# discuss
- ## 

- ## 

- ## [Show HN: Muse 2.0 with local-first sync | Hacker News_202205](https://news.ycombinator.com/item?id=31494498)
  - [Show HN: Muse – Tool for Thought on iPad | Hacker News_202008](https://news.ycombinator.com/item?id=24294397)
  - Client-side CRDT written in Swift, streaming sync server written in Go
  - **Sync server is generic**, doesn’t have any knowledge of the Muse app domain (cards, boards, ink, etc). Just shuffles data between devices
  - Transactional, blob, and ephemeral(短暂的) data are all managed by this one single state system. For example ephemeral data (someone wiggling a card around) for example, isn’t even transmitted if there are no other clients listening in realtime.
  - I’d encourage you to try the free version just to see how local-first sync feels in practice. My opinion is that is fundamentally different from web/cloud software is well as from classic file-based software—and an improvement on both. 

- I consider Muse’s ink engine pretty good, although I’ve never found anything that comes close to GoodNotes. So that would be the one to emulate – including nice features like their “pause and hold for straight line”, which I really miss in Muse

- I'm very intrigued(饶有兴味的) for the CRDT approach. I always want to try CRDT but always end up giving up local-first for simpler approaches, because I can't convince myself fully since there's a risk of accumulating CRDTs data structures too large.
  - Yes, CRDTs are risky in the sense that they are computer science that is only just at the edge of what's possible in software today. A few folks have put them into practice in small ways (Figma comes to mind) but I wouldn't recommend it for most software projects.
  - That said I hope we (meaning everyone working on CRDTs and local-first) can help make it suitable for production use and perhaps it will be a common, maybe even standard, way to build software five or ten years from now

- 
- 
- 
- 
