---
title: lib-editor-slate-community-stars
tags: [community, slate-editor]
created: 2022-05-15T18:41:58.641Z
modified: 2023-02-05T19:03:12.722Z
---

# lib-editor-slate-community-stars

# guide

- 渲染长文档的思路
  - virtualized render
    - 参考 ajaxorg/ace、codemirror、typewriter
    - 虚拟渲染能提高安全性?
  - defer render
# discuss
- ## 

- ## 

- ## 

- ## [tinymce: execCommand() is deprecated. What will TinyMCE do?_202203](https://github.com/tinymce/tinymce/discussions/7718)
- This API has been deprecated for a long time. Many many websites depend on it, it's not going away anytime soon. 
  - Having said that the majority of the calls to execCommand within the TinyMCE codebase are handled internally not by the browser. 
  - We might look at renaming the method in a future release to clear up this confusion.
  - Our long-term plan to address this deprecation is the new editor model developed for real-time collaboration: https://www.tiny.cloud/blog/real-time-collaborative-editing-slate-js/
  - Once the model is ready for general use it will be added to our open source offering and the plan is it will eventually become the default for TinyMCE.

- ## [Store paths instead of keys on selection data for `set_selection` operations](https://github.com/ianstormtaylor/slate/issues/1567)
- In a collaborative environment, keys can appear and disappear, but paths can be transformed and stay valid. In order to support both collaboration and undo / redo, set_selection needs to store both the old selection and the new selection as paths, instead of keys.
- Yep, for OT I'm already completely ignoring keys

- ## [consider using paths instead of keys_201711](https://github.com/ianstormtaylor/slate/issues/1408)

- PROS
  - For many things, like "find node by key", the "find node by path" equivalent would actually be much quicker, since you wouldn't have to search the entire tree, you'd just know exactly where to descend by just following the path.
  - It would also make operations expressed in the same terms as the local changes are applied.
  - When inserting fragments or nodes, we wouldn't have to do the current behavior where we iterate all the new nodes, insuring that their keys aren't already in the document—which would save performance.
  - I think a lot of the logic in the "at current range" transforms that determines what the selection will be after the change has applied could be simplified, because path changes are deterministic, compared to key changes which cannot be guessed ahead of time since they are unique.

- CONS
  - Finding a node in the DOM currently searches for its "key", which doesn't change across renders. But if paths were used instead then whenever a node was inserted, each node after it would have to re-render to update DOM attributes. This could potentially be mitigated by moving the key generation into the view layer, as a view-level concern instead of the data layer. Keeping it around only for locating nodes in the DOM.
  - To update a specific node, you no longer have the key reference. 
    - This could be solved by either searching for the node instance itself (with the same performance). 
    - Or it could be by passing the path to places that need the node. The path approach is awkward though, since it means the information needed can change without the node itself changing. But that's okay, because comparing by instance would work still I think, so not really an issue.

- Right now we use the concept of unique "keys" to keep track of the anchor and focus of a node in a range. And we use them to look up a node by key in the document, for updating, etc.
  - But keys are local-only, and once we convert the change information into operations, we convert "keys" into "paths", which are just an array of indices that locate a node in the document—like [2, 1, 2]. Because these don't rely on local information.

- One alternative would be to actually keep the keys, but move to using paths for most of the internal things and for operations. This might be the best of both worlds, keeping lookups fast for things like change.insertText() and so on. But allow the more precise ByKey(key, ...) behavior to persist across changes. Although those ByKey methods would be much slower by comparison. 

- I don't really depends on keys in my use case, but paths do have similar problem domain with operation transform: all paths that are stored in memory have to be transformed if an operation is performed on the editor, in order to maintain its integrity. 
  - I think translation between keys and paths might be simpler and saner implementation while improving internally using paths. If it ever reach a point where key become obsolete, it could be remove then?
- I was thinking of not storing any of the path information in the node itself. So the only things that keep paths are referencing the node from outside itself, like a range. I'm not totally sure I understand the second part you mentioned, but I agree that if there are ways to transition without removing the keys that make it much easier, we should definitely consider them

- the place I'd be most worried about would be anywhere where you grab a node, run some changes, and then get updated nodes by key from the new change.value for the rest of your function. Right now, keys make that easy. It'll take more thought without them, to make sure your paths or nodes are still valid.
  - very good point. Normalizing currently uses this technique.

- I am in favour of keeping keys, because it makes it possible to have a completely different data structure for the data storage - that doesn't necessarily map 1:1 to the Slate structure. With keys you will always know exactly what to target. I would actually prefer if the the operations too dealt with keys in stead of paths. We store and patch our documents a completely different format and using the operation's paths can be a challenge sometimes to know what do target in our document structure.

- https://github.com/TheGuardianWolf/treepack
  - v1 of changing the index of an object causes a lot of adding and deleting. This is a limitation of the path based scheme.

- ## [Unique identifier for Nodes_202002](https://github.com/ianstormtaylor/slate/issues/3489)
- the API was rewritten to effectively not rely on keys to locate nodes anymore, instead this is done with paths. 
  - This alleviates the need for the API to recursively search the node hierarchy to locate a node by its key and is a performance improvement. 
  - If you would like to bind keys to your nodes, the API allows this because you can freely add arbitrary properties to your nodes as you see fit (as long as you don't run into name collision with properties on the core interface). You can use this to write your own locate by key utilities and then that should yield you a path. 
- A good example on how to do this can be found in the embedded example.

- ## [How to have unique node ids?](https://github.com/ianstormtaylor/slate/discussions/4462)
  - to have a unique, stable identifier for each node.

- I have a similar problem in my project where each node has a unique id, but it would not work correctly when copying and pasting.
  - My solution was to override editor.insertFragment which could be called when pasting node and mark these nodes, then I am able to know which nodes are pasted and modify their ids on `onChange`.
- a general idea on how to archive something like this in a performant way by intercepting `editor.apply`. 

- plate提供了参考方案
  - https://www.npmjs.com/package/@udecode/plate-node-id

- ## [Collaborative editing](https://github.com/ianstormtaylor/slate/issues/259)
- I've started some preliminary exploration of a slate-ottype library
- The rich-text ottype isn't quite expressive enough to encode a Transform object, because it's limited to just insert, delete, and retain (format). It's fundamentally a string with attributed ranges rather than a tree structure.
- The json0 ottype isn't sufficient to granularly express the operations indicated by a Transform object. As a list of operations, however, it seems like a relevant starting point.
- Comparing the approaches taken by rich-text and json0, I quite like the "sparse traversal" format of a rich-text delta over the "list of operations" format of json0 as a way to encode a changeset. The time complexity of a "sparse traversal" should be lower than that of a "list of operations" implementation. 
- If taking the "list of operations" approach, is seems like there needs to be a transform function for each pair of fundamental operation types. With 13 different operations (addMark, insertNode, insertText, joinNode, moveNode, removeMark, removeNode, removeText, setMark, setNode, setSelection, splitNodeAtOffset, splitNode), that's 78 different functions (13 choose 2)! Is that right? Maybe there are some shortcuts or symmetry to take advantage of.

- ## [next v0.50, remove immutablejs_201911](https://github.com/ianstormtaylor/slate/pull/3093)
- Plugins are now plain functions that augment the Editor object they receive and return it again.

- ## [remove all `key` usage from Slate's core](https://github.com/ianstormtaylor/slate/issues/2864)
- Right now we use keys all over the place, because we didn't use to have "paths" as a concept. 
  - Often the key usage is a crutch( 依) for logic that can be made even simpler and more performant by using paths—although this isn't always true. Either way we need to eliminate keys to for #2495 to be able to remove the instantiation step.

- ## [switch from immutablejs to plain JSON models_201812](https://github.com/ianstormtaylor/slate/issues/2495)
- [consider migrating from Immutable.js "Records" to plain objects](https://github.com/ianstormtaylor/slate/issues/2345)
- immutablejs-cons
  - makes debugging harder.
  - Reading values is more expensive
  - requires a fromJS step to build the collections/records

- ## [Modeling RichText with Automerge](https://github.com/automerge/automerge/issues/193)
- I have spent a while thinking about this too, and I also think that a single document sequence with marker characters is the way to go. 
  - If you represent a document as a tree, there are a lot of operations that require deleting and re-inserting nodes (e.g. hitting enter in the middle of a paragraph, causing it to split into two paragraphs), which don't merge well in a concurrent setting. 
  - If a document is just a flat sequence, hitting enter in the middle of a paragraph just means inserting a '\n' element into that sequence.
- My intention was that Automerge. Text should be usable for this purpose. That is, I want Automerge. Text to be able to contain marker objects as well as characters from the text
- Maybe I am overlooking something, but "If a document is just a flat sequence, hitting enter in the middle of a paragraph just means inserting a '\n' element into that sequence." means we can not express tree structures. I can not imagine WYSIWYG without at least an anchor which has to be split as well.

- there is new development going on: next month, @geoffreylitt and @sliminality will be kicking off a research project to figure out the best way of handling rich text in CRDTs such as Automerge, with the support of the @inkandswitch research lab. 
  - https://www.inkandswitch.com/peritext/

- ## Dynamic Rendering Feature (performance improvement); only render visible blocks and not render blocks hidden within the y-overflow.__201705
- https://github.com/ianstormtaylor/slate/issues/790
- The Ace Editor: ajaxorg/ace does this by rendering two divs: 
  - a full height "scroller" div and then a "content" div that dynamic adjusts based on scrolls while updating it's content (removing hidden dom nodes and adding newly shown dom nodes).
  - https://github.com/ajaxorg/ace/blob/master/src/virtual_renderer.js
  - https://github.com/clauderic/react-tiny-virtual-list

- I don't think it's possible to arbitrarily render any part of a Slate Document at a given scroll position because it is difficult, possibly impossible, to tell how much space a Slate block will take until after it is rendered. 
  - Ace editor is an editor for monospace text so it is easy to predict how much space text will take before we render it.
- That said, what could work and could improve performance, is to render the visible portion of the page first before giving control back to the user. The rest of the content could fill in afterwards.
  - I think this might be a good low hanging fruit. Just render up to the visible portion, then use setTimeout to render a few blocks at a time for the rest without blocking the UI.

- For anyone needing this, I would highly recommend looking into other performance improvements in the general rendering case first, because they are probably much lower-hanging fruit.

- Rendering is very fast, almost instantly, with or without react-window, and deserializeHugeText is also fast. But before rendering, loading it to slate is slow.

- Interested to know everyones thoughts on a deferred rendering method (Such as described in this article on Twitter Lite)
