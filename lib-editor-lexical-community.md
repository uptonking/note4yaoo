---
title: lib-editor-lexical-community
tags: [community, lexical-editor]
created: 2021-12-21T03:12:44.032Z
modified: 2022-05-15T18:35:39.272Z
---

# lib-editor-lexical-community

# discuss-stars

- ## [Differences between Prosemirror and Lexical _202204](https://discuss.prosemirror.net/t/differences-between-prosemirror-and-lexical/4557)
- They(lexical) affirm that their value proposition differentiates them from RTE as Prosemirror in the following points:
  - **Mutable state approach**: I would appreciate if someone can elaborate on this point.
  - **Prevent the DOM from being manipulated externally (i.e. extensions)** to guarantee that the DOM always matches the EditorState
  - **React +18 support**: The main point here and the one that is the biggest new thing in React 18 is concurrency. This feature allows you to choose which nodes to render instead of the whole tree/page

- 202205
- 💡 I was on the React Core team for 3+ years, and we spent a lot of time looking into APIs and how we could eliminate whole classes of issue by simply making the edge-cases implementation details of the framework itself. The same thing applies to Lexical.
- We look at Lexical as being the React of editors – in terms of its declarative approach to promoting imperative APIs and how you go about reasoning intent. 
- An example might be schemas from ProseMirror. 
  - **Lexical doesn’t have schemas as a hot keyword, but it does offer the same functionality via Lexical’s node APIs**. 
  - Many ElementNode and TextNode methods define the intent of an interaction or a relationship with a parent, sibling, or child. 
  - You can extend one of the Lexical core nodes and just over-ride those methods and specific your heuristics for your node as needed. Which is far less boilerplate, and fully type-able in Flow/TypeScript – which is priority at Meta.
- we’re also investing in building native versions of Lexical for mobile (in native mobile languages) and also investing into building React Native bindings for those who use those surfaces. 
  - So we need something that can scale now, not something that can scale later.
  - Lexical is in a fortunate position, where we can take from what has existed previously – including ProseMirror, React, Yjs, and leverage it with latest browser APIs. 
  - Lexical doesn’t support IE, or legacy Edge, and we work closely with engineers from Mozilla and Google to patch bugs in their evergreen browsers to ensure all web editors work better (that’s why we leverage `beforeinput` so much).
- We are also trying to do best in-class for **accessibility**
  - VoiceOver, Dragon Naturally Speaking and JAWS being key tools that fail with most web editors today. 
  - A good example is the horizontal caret that is awesome in ProseMirror. Unfortunately, this doesn’t pass WCAG guidelines and doesn’t work well on mobile, so whilst we supported this in the past, we’re now going back to look at how we can insert whitespace upon moving selection to a place where the user might struggle with it (like a paragraph, for example).
- For collaboration, I worked closely with Kevin (author of Yjs) to ensure we could “sync” the Lexical editor state between many clients. 
  - We use the tree structure of Lexical to sync to `Y.XmlElement`, and `Y.Text` accordingly. 
  - We flatten text within a given block, and use inline Y. Map nodes between characters to infer the beginning and end of Lexical TextNodes. The Y. Map also holds all the properties of the TextNode, or user extended TextNode and scales well without having to use attribute ranges, which isn’t performant in Lexical’s case with CRDT. 
  - We are internally shipping Lexical with Yjs today and we hope to expand this in the future to more surfaces, including mobile.
- If anything, the reason I’m here on the ProseMirror discussion board is to praise ProseMirror’s efforts and ideas. Without them, we wouldn’t have the Lexical we have today. 
# discuss-mobile
- ## 

- ## 

- ## 

- ## 📱 [React Native Support _202204](https://github.com/facebook/lexical/discussions/2410)
- As Dominic has hinted elsewhere, I’m leading a project to build native Lexical on iOS. I’m in the very early days of looking in to what a React Native wrapper around Lexical iOS would look like. 
  - 👉🏻 The main sticking point is ensuring synchronous callbacks from JS to native, which requires bleeding edge RN features, but aside from that the issue will be the completely different layout engine for TextKit on iOS compared with DOM/CSS. So even if we enable building node subclasses in JS under RN, those node subclasses will have to use iOS semantics (providing string attributes rather than Dom nodes). That’s why I’m trying to find out what the most useful level of RN support would be, to ensure we focus on making that a good experience first.
  - I know I’ve not mentioned Android either. We have nothing to talk about there yet, alas

- ## is there an ETA for react-native support yet?_20221002
- https://discord.com/channels/953974421008293909/955972012541628456/1026124845232177224
- Not that I’m aware of

# discuss-version-history
- ## 

- ## 

- ## [Implement track changes _202306](https://github.com/facebook/lexical/discussions/4707)
- Have you figured it out? If not the CharacterLimitPlugin from the playground might help which basically does the same, only wrapping characters (or text) which is longer than allowed and then instead of wrapping deleted it unwraps

# discuss
- ## 

- ## 

- ## 

- ## What about the usage of the 'beforeinput' event on contenteditable? 
- https://twitter.com/Pryscy/status/1650081070413496320
  - I think Lexical uses it, but Prosemirror does not and warns about issues with it in their source code
- We worked hard helping browser vendors to fully get beforeinput shipped, so it has great support today.

- ## we look at Meta's new @lexicaljs framework and how we can use it to build a simple WYSIWYG editor
- https://twitter.com/kmuenster/status/1615363796671041544
  - [How To Build A Text Editor With Lexical and React](https://konstantin.digital/blog/how-to-build-a-text-editor-with-lexical-and-react)
- Although Lexical is framework-agnostic, it integrates so smoothly with React! 
- Even though we use Lexical in a React application, Lexical comes with its own renderer that flushes updates to the DOM. In that, it utilizes a virtual DOM approach to re-render only DOM nodes that have changed. This is neat performance-wise!

- ## Out of curiosity why’d you choose lexical?
- https://twitter.com/trueadm/status/1596600189913296898
- We looked at using Slate before even starting on Lexical. 
  - It has far too many issues around IME/Android and with browser extension and text autocomplete replacement. Hold down e so it becomes è at the start of an empty editor to see what I mean. This was also a common Draft bug

- ## I'm storing the output as JSON. I also need to consume the JSON on my ReactNative app and allow the user to edit the post_20220910
- https://discord.com/channels/953974421008293909/1017916026249281627
- 👉🏻 I've read the older questions about ReactNative support for Lexical on this Discord and understand from the answers that I need to use WebView till the time official ReactNative support is available.
- Here is what I think is the only way forward for me to achieve a working Lexical Editor on React Native:
  1. Write an HTML file consisting of HTML & inline CSS and inline JS. The lexical editor related HTML markup, styles and lexical related vanilla JS functions all needs to be included in this HTML file so I can call it inside web-view. 
  2. Import the HTML file and pass the file into web-view component using uri prop.
  3. Since I need an external dependency like Lexical, I need to add it using `<script>` tag in my HTML file.

- I've been trying to implement something like this, ended up having a uri endpoint serving only the lexical editor instance for webview usage and communicate between RN / lexical by assigning methods on `window` object or  `postMessage` from lexical -> RN; 4. So far it's looking good 🙂
  - May I know whether you have hosted the endpoint on some domain or did you have to write all the functions in an HTML file ?
  - i hosted in my web app and simply just render that uri with webview. after all that it's just a website with a lexical editor in it

- ## 🚀 [Lexical is now open-source (web text-editor) _202204](https://news.ycombinator.com/item?id=31017943)
- Why write Lexical over using something like ProseMirror or CodeMirror 6? 
  - Lexical is a different take compared to ProseMirror and CodeMirror. 
  - We took a lot of inspiration from them, but we felt that having a source-of-truth that wasn't the DOM was a better approach. 
  - We also looked to improve on code-size, performance and accessibility, which are often forced on the user to implement in those editors.

- Could you elaborate on what you mean by "source-of-truth that wasn't the DOM" and "performance and accessibility"?
- They are intentionally similar, ProseMirror has some great ideas. 
  - We tried to tackle those ideas from an extensible angle where nodes themselves, which form part of a tree, are the core to everything in Lexical. 
  - There are no "marks", instead you just use properties on the given nodes and treat them in an immutable sense. 
  - Nodes also present a set of createDOM/updateDOM methods, that allow you to define you DOM element, and its properties, to be passed back to Lexical's DOM reconciler.
- You can imagine the EditorState in Lexical as not only the source-of-truth for your editor's data, but also the virtual DOM for your view. 
  - Lexical diff's both and applies delta based on dirty node logic to improve performance. 
  - Furthermore, any mutations to the DOM outside of Lexical and reverted back to Lexical's EditorState – to preserver source of truth.
- Lexical also promotes different types of "text" properties on the TextNode class. Such as if the node is segmented, tokenized etc. This is a far better accessibility experience, as it ensures you can build rich text nodes – like custom emojis, or hashtags, or mentions without bailing out to contentEditable="false" which is what almost every other editor promotes. Which is also a major hinderance in terms of the ability to properly utilizie NVDA, Jaws and VoiceOver to move selection through the characters (in most cases, they skip non contenteditable elements entirely, which is terrible).

- ## Facebook open sources Lexical, an extensible text editor library__202204
- https://news.ycombinator.com/item?id=31019778
- I have quite a few questions though:
1. Is there any specific motivation behind building one from scratch?
2. How is this different from Facebook's own DraftJS lib?
3. What's the story of realtime collaboration support with OT/CRDT? Prosemirror had this in mind when designing its state model and delta model, so it comes with out of the box support for realtime collaborations. Can we expect the same with Lexical?
4. What's the cross platform strategy for Lexical? If I store the editor's state as JSON on the server, how will I render it on devices and native desktop apps?
- Internally, we've been replacing Draft.js with Lexical. To be clear though, they're different projects with little API compatibility. no deps; types; modern events
- Lexical is not strictly tied to collaboration but its plugin system was built to be extensible enough to cater all developers needs. 
  - Collaboration is just another plugin (@lexical/yjs) and does listen and perform the conversion every time there's changes in the EditorState.
  - This model of independent plugins that can be plugged-and-played without further ado also simplifies devX as collaboration can be added later when the application is mature without the need to rethink any of the plugins that were originally created for non-collab plain/rich text.
- Lexical Web is just the first of many. We want to port the API and fundamentals to various others platforms, including iOS for which we are already performing the initial set of testing. 
  - Cross-platform means the API, including Node's will look alike and EditorState and node's properties will be compatible even if behind the scenes the reconciler is constrained by the toolkit available on each platform (and doesn't render or behave 100% like Web's).

- I'm keener to understand the different between Prosemirror vs Lexical. 
- I think we've just taken a different approach when it comes to the design of things. 
- In Lexical, you rarely concern yourself with the DOM – and typically you deal with Lexical's node API directly and that's really all you touch.
- Lexical also treat its own EditorState as the source of truth. 
  - We use DOM MutationObservers to ensure the DOM matches the EditorState at all times. 
  - We do allow external mutations from things like spellcheckers update Lexical – otherwise people wouldn't be able to use Grammarly and other tools with Lexical. However, that's really constrained so that they don't overreach.
- Lexical also has the notion of double-buffering. 
  - When you update Lexical, or use a node transform, you're actually mutating the "work in progress" EditorState. Once Lexical feels that the EditorState is ready, it will commit it to the DOM, and that EditorState will become immutable and will reflect what you see on the page.

- Any particular reason Meta decided to implement it's own editor library instead of building on top of ProseMirror?
  - ProseMirror wasn't a good fit for us because it's integration (especially with React 18+) isn't quite there. Furthermore, we're also looking into building native ports of Lexical, and given's Lexical's API isn't DOM centric, it allows us to do that.
  - Lastly, we found ProseMirror was too heavy in terms of bytes for very minimal almost plain-text interfaces where we only wanted mentions + hashtags + custom emojis. Lexical comes in at around 22kb min+gzip, so it works really well for us.

- I'm curious as to what areas Prosemirror could have taken a better approach
- I don't think ProseMirror has taken a bad approach. I think we've just taken a different approach when it comes to the design of things. In Lexical, you rarely concern yourself with the DOM – and typically you deal with Lexical's node API directly and that's really all you touch.
- Lexical also treat its own EditorState as the source of truth. We use DOM MutationObservers to ensure the DOM matches the EditorState at all times. We do allow external mutations from things like spellcheckers update Lexical – otherwise people wouldn't be able to use Grammarly and other tools with Lexical. However, that's really constrained so that they don't overreach.
- Lexical also has the notion of double-buffering. When you update Lexical, or use a node transform, you're actually mutating the "work in progress" EditorState. Once Lexical feels that the EditorState is ready, it will commit it to the DOM, and that EditorState will become immutable and will reflect what you see on the page.

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
- CodeMirror 6 also uses a concept of separate state and view. Is outline different?
  - In outline we have the notions of an editor, nodes and immutable editor states (which are the source of truth). 
  - There are two editor states, a current one which is what you see on the DOM, and a pending one that is currently being generated. The editor reconciles the editor state
  - Plus the editor provides high-level listeners, command handling and node transforms. So there are similarities with CM6, but also many differences too. 
  - In CM6 the state also immutable, and the state mutates via transactions. But the real power is in extensions and facets/fieldState

- My hope is that they’re using contenteditable and have enough clout to get some of the bugs fixed in the different browsers.
  - For the web, we're using contenteditable, with support for modern browsers only.
  - Interesting! Last I recall even modern browsers had a variety of ways they differed in implementation (not including actual bugs) that caused a lot of edge case issues. The amount of workarounds in this changelog is disheartening to say the least! https://prosemirror.net/docs/changelog/
- We are on our fourth editor in our product because these projects have a habit of being abandoned. Please or please let this be the one that isn’t 

- ## [Lexical – a web text editor framework that powers Facebook | Hacker News_202206](https://news.ycombinator.com/item?id=31813550)
