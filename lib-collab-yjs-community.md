---
title: lib-collab-yjs-community
tags: [collaboration, community, yjs]
created: 2022-04-05T10:11:24.612Z
modified: 2022-04-05T10:11:40.379Z
---

# lib-collab-yjs-community

# guide

# discuss
- ## 

- ## 

- ## yjs vs peritext
- https://news.ycombinator.com/item?id=29328431
- They way I see it there are two (or maybe more of a spectrum of) types of CRDT, from generic and to domain specific. 
  - Yjs actually has multiple different types, very generic types (Array and Map), slightly more specific types (XMLFragment and XMLElement), and then there is the Text type that covers both a generic plain text type but also has provision for rich formatting if needed. 
  - Peritext is basically a different method of implementing the Text type which aims to maintain a little more editor intent than Yjs currently does.
- For a full document, you need to represent both text elements with rich text formatting marks, but also block elements. With Yjs you would do this with the XMLElement type which as you would expect has attributes and can nest further XMLElements or Text within it. 
  - Peritext does not yet have support for block types.
- So, although the most common use of Yjs is for collaborative rich text editing, it can be used for many other things such as 2D/3D drawing or even gaming.







- ## Main takeaways from toying with both Yjs and Automerge
- https://news.ycombinator.com/item?id=29507948

1. Extremely difficult to build backend in other programming languages than Nodejs
2. Both communities are great.
3. Watch out implementations of underline libraries. Trace lib0 libraries usage and internals in Yjs for example;JavaScript engines use UTF-16 encoding. Golang (my main backend language) is using UTF-8 ... reimplementing Yjs code in Golang with algorithms and optimization and futher scaling might become impossible for small startups.
4. Rich editing similar to Google Doc is very very complicated subject with lot of landmines
5. There's ProseMirror editor for collaborative editing. However you might not like its internals compare to Slatejs 


# automerge
- ## Automerge: A JSON-like data structure (a CRDT) that can be modified concurrently_202202
- https://news.ycombinator.com/item?id=30412550

- ## Automerge: JSON-like data structure for building collaborative apps_201802
- https://news.ycombinator.com/item?id=16309533
