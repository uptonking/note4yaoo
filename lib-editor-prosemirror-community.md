---
title: lib-editor-prosemirror-community
tags: [community, editor, prosemirror]
created: 2021-06-12T02:40:46.194Z
modified: 2021-06-12T02:41:33.389Z
---

# lib-editor-prosemirror-community

# guide
- prosemirror-experts
  - https://github.com/benrbray
    - https://github.com/benrbray/noteworthy
    - https://github.com/benrbray/prosemirror-math
  - https://github.com/ocavue
    - Core team member at remirror
    - https://github.com/ocavue/rino
      - A better way to write Markdown
  - https://github.com/YousefED
    - https://github.com/YousefED/BlockNote
    - https://github.com/YousefED/Matrix-CRDT
    - https://github.com/YousefED/SyncedStore

- prosemirror-lovers
  - https://github.com/namiwang
  - https://discuss.prosemirror.net/u/zlv-thisF
    - 块编辑器
  - https://discuss.prosemirror.net/u/Julian123
    - 块编辑器
# discuss
- ## 

- ## 

- ## ProseMirror is now a TypeScript project_v20220520
- https://discuss.prosemirror.net/t/prosemirror-is-now-a-typescript-project/4624
- the code is now typed using strict TypeScript
- No breaking changes should have been made to the JavaScript interface.

- ##  Why did you pick that over Slate or Draft?
- https://twitter.com/nikgraf/status/1415726807446401024
- Afaik all of the are maintained.
  - Draft’s data updates don’t allow for an integration with a CRDT.
  - Slate is awesome, but the API changed a lot over the years and still lacks Android support.
  - Every team that I know where the editor is part of the core UX switched to Prosemirror.

- ## Minimal UI Math Editor - Treena
- https://discuss.prosemirror.net/t/minimal-ui-math-editor-treena/3117
- can you share how you implemented the type ahead. i know there are a bunch of open source implementations ( `atlaskit` , `prosemirror-suggest` ), did you use any of those ?
  - So i based the insert menu on the code in the `prosemirror-mentions` package. 
  - I basically refactored the code to remove reliance on the included schemas in that package. 
  - The code is quite flexible so i just added a `fuzzy-search` for the displayed elements and a custom callback for each of the options. 
  - The callbacks are super similar to the included prose functions such as toggleMark! I hope thats helpful!

- ## parseDom Content for Inline Node (footnotes)
- https://discuss.prosemirror.net/t/parsedom-content-for-inline-node-footnotes/642
- Your node doesn’t allow content, so indeed, as you noticed, the parser won’t it won’t look for content.
  - Still, to be able to properly edit these, your node view is going to have to do a bunch more work (at the very least, it’ll have to set the `contenteditable` – or create a textarea with the content). Embedding an extra ProseMirror to edit a node like this will also get easier in the next release.
- I plan on adding a textarea to the nodeView’s dom for editing the annotation comment. And will be storing the value of the comment in an attribute when serialized into my dom structure.

- ## Using DOMSerializer inside a NodeView
- https://discuss.prosemirror.net/t/using-domserializer-inside-a-nodeview/1498
  - I’m trying to use `DOMSerializer` to produce DOM nodes so i can set the dom property inside a NodeView:
- The reason i’m doing this is that i want to set up event handlers on the resulting dom. 
  - The expected dom is too complicated to produce with the `document.createElement` method, so i tried to do it with `DOMSerializer` .
  - This almost works: the view is rendered, but it is not possible to interact with it.

```JS
class TodoListView {
  constructor(node, view, getPos) {
    const domSerializer = DOMSerializer.fromSchema(mySchema)

    const serializedDom = domSerializer.serializeNode(node, {})

    this.dom = serializedDom;
  }
}
```

- By defining a node view like this, you’re telling ProseMirror that the node is an opaque element that it shouldn’t manage. 
  - For things to be editable, you have to let the editor render them. 
  - So don’t render the children in the node view implementation, just provide a `contentDOM` property that the editor will render the children into.

- ## Understanding the interaction between parseDOM, DOMChange and NodeView
- https://discuss.prosemirror.net/t/understanding-the-interaction-between-parsedom-domchange-and-nodeview/678
- The issue centers around the way that dom mutations are parsed by PM, and this interacting poorly with my custom node view.
  - When you enter a character directly after the node view (and I suspect in other cases), PM tries to figure out what changed by parsing the content of the view, and analyzing the diff against the previous state. 
  - During general operation, this seems to happen pretty infrequently (the transactions are generated through some other means, that don’t rely on diffing the dom).
  - My custom view has a rather complex DOM structure
  - I initially didn’t realize that my NodeView would be parsed this way, and it seems that I lose the latex annotations inside my node during this parsing.
- the parser will get the node’s type and attributes from the node view.
- as long as you go through a transaction you should be fine.

- ## Offline, Peer-to-Peer, Collaborative Editing using Yjs
- https://discuss.prosemirror.net/t/offline-peer-to-peer-collaborative-editing-using-yjs/2488
- I haven’t dug into the y-prosemirror code in depth yet, but, is there any way with Yjs fragments to model changes that happen to a fragment as steps rather than replacing the whole document? 
  - It seems like in the current implementation of the sync plugin, **every synced change ends up replacing the whole document**  (taking care to maintain the local selection state, and managing the undo state with a Yjs specific plugin). 
  - Basically what I’m curious about is whether you could replicate ProseMirror data using Yjs, but still write ProseMirror plugins without needing to “know” that Yjs was handling remote state updates (e.g. where you could, for example, rely on transaction steps + step maps to figure out what ranges have changed during a given remote sync).
- Oh, no, that does seem like a sure way to break almost every ProseMirror plugin ever written.
- Yes, there is. I gave an outline here: ProseMirror + CRDT's? . The idea is to compute the steps based on the diff of the new and the old state of the document.
  - From my personal experience computing “minimal diffs” is a bit expensive and unnecessary for my use-cases. I’m still a bit indifferent about this feature. 
  - I’m not denying that it will break some ProseMirror plugins (i.e. plugins that render using decorations and ProseMirror mappings). 
  - But I have tested y-prosemirror successfully in Atlaskit and TipTap. 
  - For the reasons mentioned above I also needed to replace ProseMirrors history plugin with Yjs-based history plugin (y-undo-plugin).
- Comparing structure-sharing trees should actually be doable really efficiently (since you can skip all the shared nodes right away). 
  - (There was an implementation of this in a very early ProseMirror system that relied on it for its redrawing algorithm, and it wasn’t very complicated.)
- I do use the prosemirror state. 
  - But for me, the question was if it makes sense to use ProseMirror transforms to represent document changes. 
  - Currently, I simply replace the document state. This is easier to do for me.
  - I didn’t see any immediate benefit in Transforms, because they are mainly used to calculate change maps and to provide undo-redo functionality. 
  - y-prosemirror has an equivalent to change maps and undo functionality, that work better in p2p scenarios. 
  - But @saranrapjs brought up a good point for ProseMirror transforms.
- The main thing that we use, by way of example, that wouldn’t work without some kind of transaction mapping is indeed decorations; the ability to map positions transaction-wise is what allows us to do efficient transaction-wise computations only when needed (e.g. only recalculating a data structure for the parts of the document that have changed). If the tradeoff here is how expensive it is to compute the diffs that happen as part of a Yjs update vs. how full resolution the diffs are, for my part, I’d be happy with marginally lower resolution diffs 

- Yjs by itself is just a small CRDT implementation. 
- There are several modules around Yjs that allow you to do different things.
- Editor bindings, like y-prosemirror, y-codemirror, or y-quill make a specific editor collaborative. 
- Connectors, like y-webrtc, or y-websocket handle how to sync to other peers
- Persistence adapters handle how to persist data to a database to make it available offline (e.g. y-indexeddb for the browser, or y-leveldb for the server).
- The idea is to make Yjs as modular and unopinionated as possible and build a huge ecosystem around it. 

- ## Inlining a node for a comment plugin or best to use marks?
- https://discuss.prosemirror.net/t/inlining-a-node-for-a-comment-plugin-or-best-to-use-marks/2391
- Comments are usually not modeled as document nodes—rather, they are references to ranges, that are tracked separately, outside of the document.
- I will try with references to ranges outside the document. One downside is that it could be a bit trickier to preserving comments when users copy to clipboard.
  - That is absolutely true. I’m not aware of an actual good solution to that problem, though you can get pretty far by storing metadata to the side when copying and consulting that, comparing it to the pasted slice, when pasting.
- what are other arguments to not use marks for comments?
  - For decoration approach, there is clear separation of non-editable document with ability to comment in “read only” mode.
  - The data structure for decoration comments are a more straightforward model defined solely by a single from/to.

- ## A4 pages conceptual guide
- https://discuss.prosemirror.net/t/a4-pages-conceptual-guide/2901
- have a schema that looks like
  - https://github.com/todorstoev/prosemirror-pagination

    - Plugin for ProseMirror emulating A4 pages

- What is done till now
  - correct split for single line paragraphs
- What should be done
  - correct split in tables
  - correct split for multiline paragraphs

```
doc(
   page(
       header(block+)
       body(block+)
       footer(block+)
       pageCounter(paragraph{1})
   )
)
```

- ## ProseMirror – A toolkit for building rich-text editors on the web
- https://news.ycombinator.com/item?id=18998042
- What sets ProseMirror apart from the rest (Slate, Quill, Trix, Draft, etc.) is - ProseMirror isn't simply a library. 
  - It's an entire platform with all bits and pieces needed to build a simpler rich text library. Rightly named "toolkit" instead of a "library".
- Interestingly, the platform design of ProseMirror is one of the key reason which drives me to Quill in one of my side projects. 
  - Don't get me wrong, if your goals mostly align with ProseMirror, it's a perfect tool, 
  - but if you want to deviate with ProseMirror in some aspects, the coupling design between different ProseMirror packages is actually a headache. 
  - On the other hand, Quill feels more like a simple library targeting exactly one use case.
  - In addition, I feel that Quill's [delta format](https://quilljs.com/docs/delta/) is much more elegant and easier to work with than ProseMirror's [changeset](https://github.com/ProseMirror/prosemirror-changeset), especially if your architecture uses a different language that's not JS.

- If any of you have used Quill and Prosemirror, what were your impressions of the differences between the two? Here's what I've observed so far:
- DraftJS (React) 
  - works on desktop, but has no plans for collaborative editing, mobile support, and limited development. 
  - We found it hard to extend the paste handling for custom behaviours too. 
  - On the other hand, there are a lot of nice libraries built around it (we used medium-draft)
- Slate (React) 
  - is definitely the way to go for React developers who don't yet need mobile support. 
  - It's mature and has a good community of developers. 
  - The one downside is that some of the popular plugins lost compatibility with the latest version of Slate
- Quill (non-React) 
  - seems very mature with a good ecosystem of plugins. 
  - Instead of relying on React Components, it relies on there being a strict mapping between the DOM and the model that you build. 
  - The "model" is the DOM, so-to-speak, but with heavy restrictions to avoid ContentEditable issues. 
  - We've found it to be very mature, and it's the only one of the 3 we've found to have great mobile and collaborative-editing support out of the box. That was important for us, so we ended up using it today

- I've briefly analysed ProseMirror as well as Quill. IMO ProseMirror seemed well built with better literature compared to Quill.
  - ProseMirror's author has truly thought out every API and has got most of the details just right.
  - For example, if I ought to build a grammar checker on top of Quill vs ProseMirror, I couldn't find any APIs in Quill that lets us decorate the view with grammar errors and suggestions, without polluting the core data-model with custom nodes/attributes. 
  - ProseMirror on the other hand had the concept of Decorators (https://prosemirror.net/docs/ref/#view.Decorations) for such a case. That was just one example.
  - More from the author of Quill himself

- ## ProseMirror 1.0 
- https://news.ycombinator.com/item?id=15465125
- Author of Quill here. 
  - Interested in hearing Marjin’s thoughts but here are some of my main observation is at a high level Prosemirror is much more willing than Quill to sacrifice simplicity for power. 
  - This value difference manifests in the target audience, architecture and API design:
  - Quill can be used for the get going quickly drop in use case. 
  - Prosemirror specifically warns against this: “If you're looking for a simple drop-in rich text editor component, ProseMirror is probably not what you need. (We do hope that such components will be built on top of it.) The library is optimized for demanding, highly-integrated use cases, at the cost of simplicity.”
- Prosemirror’s schema, as documented, is more flexible than Quill’s.
  - Prosemirror appears to allow anything, whereas Quill imposes some constraints. 
  - For example Quill requires all nodes to either be a leaf and cannot have children or a container and must at least one child. 
  - There cannot be a node that can optionally have children as is allowed in Prosemirror. 
  - In my experience the constraints Quill imposes lead to a more consistent and bug free experience across browsers. 
  - I will be curious to try out the edge cases I have encountered at this new 1.0 Prosemirror to see if it handles them the way an end user typist would expect. If Quill can benefit from a shift in the flexibility in its schema, it will do so.
- Quill is far more battle tested. Slack, Salesforce, LinkedIn, Intuit and many others are using Quill in their main user-facing production products, not an internal employee only tool. 
  - Prosemirror has a great start with the NY Times but there is a large difference in adoption at the moment.
