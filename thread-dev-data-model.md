---
title: thread-dev-data-model
tags: [architecture, data-model, dev]
created: 2023-10-27T08:03:11.658Z
modified: 2023-10-27T08:06:00.698Z
---

# thread-dev-data-model

# guide

# discuss-stars
- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## 

- ## 

- ## 

- ## Why do we need to name so many things. Files, functions, variables. Just give them a UUID and infer semantic meaning from their contents.
- https://twitter.com/JungleSilicon/status/1717600477859442929
- I worked on a uuid based system and it caused a surprising number of weird side effects. 
  - 1. Heirarchical data can't be copied recursively. 
  - 2. DB index performance goes to shit. Due to 1. there is an uptick in broken copying bugs from wonky(不稳的; 摇晃的; 有差错的; 有毛病的) references.
- Data can still have relationships to one another.
  - Yeah. For sure, and uuids have many advantages, but the experience made me appreciate the value in relative addressing for some situations too. Something I used to take for granted.
  - Uuids flatten hierarchy in a global namespace. Composite identifiers make more sense in hierarchical systems, and computers are full of heirarchies
- UUIDs are great, you never want to identify something by it as a human, but it means that when you make modifications to that thing in a distributed setting it knows you mean *that thing*.
  - UUIDs are great for that purpose, yes. But you mentioned functions and variables, for which UUID is overkill (and adds a great deal of complexity) But for config vars and things (and distributed), yes.
- UUIDs are non-memorable, look bad in URLs, don't allow serendipitous discovery/joins (like in a tagging system)
- I tried this approach - it works at a level - ended up having to add meta info to help where a name w have been better - like here is a list of media files - a list of UUID’s don’t help the user so you have to have the name somewhere

- 
- 
