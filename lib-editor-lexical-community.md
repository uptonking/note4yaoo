---
title: lib-editor-lexical-community
tags: [community, lexical-editor]
created: 2021-12-21T03:12:44.032Z
modified: 2022-05-15T18:35:39.272Z
---

# lib-editor-lexical-community

# discuss-stars

- ## Differences between Prosemirror and Lexical_202204
- https://discuss.prosemirror.net/t/differences-between-prosemirror-and-lexical/4557
- They(lexical) affirm that their value proposition differentiates them from RTE as Prosemirror in the following points:
  - Mutable state approach: I would appreciate if someone can elaborate on this point.
  - Prevent the DOM from being manipulated externally (i.e. extensions) to guarantee that the DOM always matches the EditorState
  - React +18 support: The main point here and the one that is the biggest new thing in React 18 is concurrency. This feature allows you to choose which nodes to render instead of the whole tree/page

- 202205
- I was on the React Core team for 3+ years, and we spent a lot of time looking into APIs and how we could eliminate whole classes of issue by simply making the edge-cases implementation details of the framework itself. The same thing applies to Lexical.
- We look at Lexical as being the React of editors – in terms of its declarative approach to promoting imperative APIs and how you go about reasoning intent. 
  - An example might be schemas from ProseMirror. 
  - Lexical doesn’t have schemas as a hot keyword, but it does offer the same functionality via Lexical’s node APIs. 
- we’re also investing in building native versions of Lexical for mobile (in native mobile languages) and also investing into building React Native bindings for those who use those surfaces. 
  - So we need something that can scale now, not something that can scale later.
- Lexical is in a fortunate position, where we can take from what has existed previously – including ProseMirror, React, Yjs, and leverage it with latest browser APIs. 
  - Lexical doesn’t support IE, or legacy Edge, and we work closely with engineers from Mozilla and Google to patch bugs in their evergreen browsers to ensure all web editors work better (that’s why we leverage `beforeinput` so much).
- We are also trying to do best in-class for accessibility
  - VoiceOver, Dragon Naturally Speaking and JAWS being key tools that fail with most web editors today. 
  - A good example is the horizontal caret that is awesome in ProseMirror. Unfortunately, this doesn’t pass WCAG guidelines and doesn’t work well on mobile, so whilst we supported this in the past, we’re now going back to look at how we can insert whitespace upon moving selection to a place where the user might struggle with it (like a paragraph, for example).
- For collaboration, I worked closely with Kevin (author of Yjs) to ensure we could “sync” the Lexical editor state between many clients. We use the tree structure of Lexical to sync to Y. XmlElement, and Y. Text accordingly. 
  - We flatten text within a given block, and use inline Y. Map nodes between characters to infer the beginning and end of Lexical TextNodes. The Y. Map also holds all the properties of the TextNode, or user extended TextNode and scales well without having to use attribute ranges, which isn’t performant in Lexical’s case with CRDT. 
  - We are internally shipping Lexical with Yjs today and we hope to expand this in the future to more surfaces, including mobile.
- If anything, the reason I’m here on the ProseMirror discussion board is to praise ProseMirror’s efforts and ideas. Without them, we wouldn’t have the Lexical we have today. 
# discuss
- ## 

- ## 

- ## 

- ## 

- ## 

- ## Lexical is now open-source
- https://twitter.com/trueadm/status/1514298427840024581
  - We're also experimenting with a Lexical for iOS, which will be a Swift based implementation of Lexical using TextKit.

- How does this compare to slateJS? Seems the approach to nodes and transforms is pretty similar
  - Yep, we took inspiration from Slate. 
  - One area that we differ on is the fact Lexical has different event handling for composition/IME and also the compatibility around third-party browser extensions that can mutate the DOM (spellcheck etc).

- Were collaboration features a consideration when building?
  - Yep, we having collaboration bindings for yjs.
  - We use Yjs internally, and maybe externally in the future.

- Is Lexical a replacement of Draft.js?
  - Internally, we've been replacing Draft.js with Lexical. To be clear though, they're different projects with little API compatibility.
  - Why you don't simply improve Draft js ?
  - Draft.js was built many years ago when the web was in a different place. It's architecture doesn't really fit the ethos that we're trying to promote today – we are trying to promote extensibility and a different kind of take on how you can build editors.

- Is there LSP support? Or we would need to make a plugin if we want to use it? 
  - Folks have also asked about this internally. We don't yet have support, but it shouldn't too difficult to add support. If anyone is feeling ambitious and would like to work on this, that would be epic! : D

- Is Lexical support partical render when text content is very huge?
  - We're exploring virtualization, but we have a bunch of higher-pri things to attend to first :)

- huge congrats! always so awesome when you ship stuff. i'd love to see unfurls and "paste-in images" implemented in this, thats the last thing i look for in these solutions tho im sure you already thought of it and i just need to look harder

- ## Lexical is a next-gen JavaScript web text editor framework we've been building at Meta – with an emphasis on reliability, accessibility and performance.
- https://twitter.com/trueadm/status/1506461323160428558
- As a replacement for draftjs?
  - Lexical is very different from DraftJS, but you could think of it as that. Internally, we've been slowly migrating our surfaces to Lexical, and using that process to help inform us of missing features/functionality before open sourcing Lexical.
  - Lexical doesn't have any dependencies, let along on ImmutableJS. It has its own typed immutable EditorState object internally which can be serialised to JSON, so it's highly flexible.

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
- Blocks and ranges have an interesting byproduct: they are friendly with realtime collaboration using CRDT/OT algorithms. What's the story of multiplayer support for DOM like tree structure? Just curious.
  - We have outline-yjs bindings for collaboration with Yjs and we keep our tree structure there using Y. XmlElement, Y. XmlText and few other clever implementation details. We actually found that avoided some common issues with blocks/ranges by going this approach (lists come to mind)
  - I'm thinking through what could be a good CRDT direction for block elements exactly like lists (and tables) 
  - [What could be the direction for making Peritext support block elements](https://github.com/inkandswitch/peritext/issues/27)
  - https://github.com/inkandswitch/peritext
    - A CRDT for asynchronous rich-text collaboration, where authors can work independently and then merge their changes.
- CodeMirror 6 also uses a concept of separate state and view. Is outline different?
  - In outline we have the notions of an editor, nodes and immutable editor states (which are the source of truth). 
  - There are two editor states, a current one which is what you see on the DOM, and a pending one that is currently being generated. The editor reconciles the editor state
  - Plus the editor provides high-level listeners, command handling and node transforms. So there are similarities with CM6, but also many differences too. 
  - In CM6 the state also immutable, and the state mutates via transactions. But the real power is in extensions and facets/fieldState

- My hope is that they’re using contenteditable and have enough clout to get some of the bugs fixed in the different browsers.
  - For the web, we're using contenteditable, with support for modern browsers only.
  - Interesting! Last I recall even modern browsers had a variety of ways they differed in implementation (not including actual bugs) that caused a lot of edge case issues. The amount of workarounds in this changelog is disheartening to say the least! https://prosemirror.net/docs/changelog/
- We are on our fourth editor in our product because these projects have a habit of being abandoned. Please or please let this be the one that isn’t 
