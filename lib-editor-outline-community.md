---
title: lib-editor-outline-community
tags: [community, outline-editor]
created: '2021-12-21T03:12:44.032Z'
modified: '2021-12-21T03:14:26.843Z'
---

# lib-editor-outline-community

# discuss
- ## We've been building Outline – an extensible text editor library that does things differently. 
- https://twitter.com/trueadm/status/1472377356044099587
  - If you use http://facebook.com or http://workplace.com, you've likely already used it.
  - We're expecting to open source it early 2022.
- Another important implementation detail: **Outline's core library doesn't have any dependencies**. 
  - This means it can be used with any framework. 
  - However, we will provide React bindings with Outline when we go open source, as these bindings are already used and battle-tested at Meta.
- Does this replace Draft?
  - It would replace, although the libraries aren't API compatible so it's not a simple swap. 
  - We'll build some documentation around how you might upgrade from DraftJS nearer the time.
- You guys dropping draftjs? I thought Facebook was using that for most to all input fields. You guys also use it for notes. No?
  - We still use DraftJS in many places, but we're slowly migrating usages over to Outline, where it makes sense.
- What are the key ways it improves on DraftJS? We’re these incompatible with modifying DraftJS and having a clean upgrade path? Are there strengths of DraftJS that would be lost with moving to Outline?
  - The editors take very different approaches to how they work both at an implementation level and an API level. 
  - **The biggest differences are that Outline has its own renderer and graph state model, and doesn't depend on React or ImmutableJS**.
  - So unfortunately, there's no compatibility between the two. This is intentional too – we wanted to reimagine how text editors could be built, rather than build on the existing paradigms around how they're built today.
- How it relates to prose-mirror?
  - It's got many similarities in a bunch of areas, but it aims to be a far better developer experience abstraction – kind of like how React with components. Not to mention code size and performance improvements.
- Code text editing? As in an eventually competitor to Monaco? Or more for document drafting?
  - We've built Outline in a way that you could build solutions for either use-case.
- Do you provide support for tablet/mobile use cases?
  - Outline works great on iOS and Android web.
- Any plans for making it work in React Native as well?
  - Not concrete plans right now, but we have some ideas for how this might work in the future.

- want to build an outliner not sure this will work with roam/notion-like block-based editing style or just plain wysiwyg?
  - Outline has its own internal editor state like other editor libraries. 
  - **Outline's EditorState is in a tree structure, rather than a flat structure with blocks and ranges**. You can think of it more like a DOM structure.
  - There's an example of the Outline API
- CodeMirror 6 also uses a concept of separate state and view. Is outline different?
  - In outline we have the notions of an editor, nodes and immutable editor states (which are the source of truth). 
  - There are two editor states, a current one which is what you see on the DOM, and a pending one that is currently being generated. The editor reconciles the editor state
  - Plus the editor provides high-level listeners, command handling and node transforms. So there are similarities with CM6, but also many differences too. 
  - In CM6 the state also immutable, and the state mutates via transactions. But the real power is in extensions and facets/fieldState

- My hope is that they’re using contenteditable and have enough clout to get some of the bugs fixed in the different browsers.
  - For the web, we're using contenteditable, with support for modern browsers only.
  - Interesting! Last I recall even modern browsers had a variety of ways they differed in implementation (not including actual bugs) that caused a lot of edge case issues. The amount of workarounds in this changelog is disheartening to say the least! https://prosemirror.net/docs/changelog/
- We are on our fourth editor in our product because these projects have a habit of being abandoned. Please or please let this be the one that isn’t 
