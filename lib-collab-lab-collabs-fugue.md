---
title: lib-collab-lab-collabs-fugue
tags: [collaboration, collabs, crdt, fugue]
created: 2024-05-05T16:15:55.904Z
modified: 2024-05-05T16:18:04.696Z
---

# lib-collab-lab-collabs-fugue

# guide

- [Open-Source Software - Matthew Weidner](https://mattweidner.com/software.html)
  - [Collabs Documentation — Collabs documentation](https://collabs.readthedocs.io/en/latest/)
    - Collabs is a TypeScript collections library for collaborative data structures (CRDTs). It puts into practice many of the ideas from my first blog post, Designing Data Structures for Collaborative Apps.
  - position-strings and list-positions serve similar purposes. 
  - `position-strings` has a minimalist API designed for maximum compatibility with existing systems. 
    - position-strings is a TypeScript library that provides “position strings” for use in collaborative lists or text strings. 
    - Each position string points to a specific list element (or text character), and the list order is given by the lexicographic order on position strings.
    - position-strings essentially implements the `Fugue` list CRDT with a minimalist API.
  - `list-positions` is more comprehensive and uses less memory & storage, especially when used for text editing.
    - list-positions implements the `Fugue` list CRDT, while @list-positions/formatting implements Geoffrey Litt et al.’s Peritext rich-text CRDT. 
# blogs

# discuss-stars
- ## 

- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## 

- ## Announcing a new TypeScript library: list-positions. _20240429
- https://twitter.com/MatthewWeidner3/status/1784959530268242314
  - It is a library of local data structures that implement the "hard part" of list/text collaboration, which you then can use on top of various sync tools: authoritative server, NoSQL DB, version control system, etc.
- List-positions lets you represent a list as an ordered map (position -> value), where each "position" is immutable - it doesn't shift around like an array index. So you can store & share positions without worrying that they'll be invalidated by other edits.
  - List-positions is based on list/text CRDTs, but not itself a CRDT - it provides *local* data structures that you can edit however you like. E.g., a central server can inspect and reject/modify updates to its own state, even if that breaks causal ordering or monotonicity.
