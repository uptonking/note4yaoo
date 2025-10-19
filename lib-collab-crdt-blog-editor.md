---
title: lib-collab-crdt-blog-editor
tags: [blog, collaboration, crdt, editor]
created: 2023-10-28T09:02:53.320Z
modified: 2023-10-28T09:03:33.687Z
---

# lib-collab-crdt-blog-editor

# guide

# blogs

# blogs-text

## 📌 [Some notes on editor frameworks (eg. Monaco, Lexical, Codemirror, etc) + collaborative editing/conflict resolution technologies (eg. OT, CRDT, etc)](https://gist.github.com/0xdevalias/2fc3d66875dcc76d5408ce324824deab)

- [Some thoughts RE: Copy on Write + Event Sourcing for edit history](https://gist.github.com/0xdevalias/20cfaaeb33698440b58b00ab97dd3bbc)

## [Why RichText facets in Bluesky | Paul's Dev Notes _202401](https://www.pfrazee.com/blog/why-facets)

- Why not Markdown
- Problem 1: Syntax barfing(呕吐)
  - Suppose you want to add a behavior that markdown doesn't usually support, others cannot parse/render correctly
- Problem 2: Parsing sucks
  - Your markdown variation is going to need a library for every environment.
- Problem 3: Character counting
  - In microblogging networks, the character limit is a somewhat defining feature.
  - You have to strip the syntax first.

- Bluesky's answer: Richtext Facets
  - Our answer was to use strings annotated by slices that point into the string.
  - Data in the AT Proto is transmitted as JSON or CBOR. No custom parsing is required.
  - If there's a facet-type your client doesn't understand, it's just ignored and the original text carries through. 

```JS
// slightly simplified
{
  text: "Hello @bob.com",
  facets: [
    { feature: "mention", index: { start: 6, end: 14 } }
  ]
}
```

- Bonus discussion: maintaining intent

## [cola: a text CRDT for real-time collaborative editing_202309](https://nomad.foo/blog/cola)

# more
