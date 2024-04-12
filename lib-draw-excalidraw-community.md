---
title: lib-draw-excalidraw-community
tags: [community, drawing, excalidraw]
created: 2023-06-19T12:34:22.103Z
modified: 2023-06-19T12:34:49.156Z
---

# lib-draw-excalidraw-community

# guide

# dev

# examples

- https://github.com/excalidraw/excalidraw-room /ts
  - Collaboration server for Excalidraw
# discuss-collab
- ## 

- ## [Collaboration mode - Self-hosting vs Collab on top of `<Excalidraw/>` _202108](https://github.com/excalidraw/excalidraw/discussions/3879)
- We have our own reconciliation algo which takes care of resolving merge conflicts.
  - Yes if you are implementing collaboration you will have to take care of it.
- Since collaboration is something consumer is taking care of so its completely up to you how you want to implement it. We trigger `onChange` callback whenever there is some change in excalidraw so there might be some additional data you might need along with elements and appState so that we can discuss based on the implementation.

- you can take a look at collaboration of how we do at excalidraw and reuse the same at your end so you don't have to clone the excalidraw repo and change end points etc.

- ## [[RFC] use CRDT for collaboration_202105](https://github.com/excalidraw/excalidraw/issues/3537)
- I think that using yjs would allow excalidraw to support concurrent edits to text boxes. It feels like quite a lot of work though.
- This wouldn't solve the "concurrent edits to the same element" problem though: it would just be a tech demo that using yjs is possible.

# discuss
- ## 

- ## 

- ## 

- ## Working on Excalidraw and Excalidraw+ we've been doing lots of modals. 
- https://twitter.com/dluzar/status/1418259104938795017
  - I thought I'd share some of the points from my experience.
- Let's start with accessibility: focus traps. 
  - Pressing Tab should never take you out of the modal. 
  - Instead, you should cycle back to the first focusable element.
  - (And make sure upon opening the modal you focus the first actionable element, usually the first input field.)
  - You can do this by listening on `keydown` , querying all focusable elements (inputs, buttons...) from the modal's root element, and manually focusing either the first or last element based on whether user pressed `shift` or not.
- Clicking outside the modal should close it, same as when pressing `escape` .
- What if the user just filled out the form and clicked away by mistake? Losing progress is annoying, so let's prevent that.
  - When the form is dirty, clicking outside (or Escape) won't close, and require you to explicitly hit `close` or `submit` button.
  - you can show the submit button only on a dirty form. This will give additional visual feedback.
- As a bonus, we can make pressing `escape` focus the close button as a courtesy to the user.
- Whenever your list exceeds a given number of items, you should provide a way to filter them for quick access.
  - Bonus points for adding a button to clear the filter for mobile users.
  - And you can set `min-height` to the list so that filtering doesn't result in layout shift.
- In large, scrollable modals, it's a good idea to make the header and the footer sticky so that the context and modal buttons are always visible.
- But how to deal with browser's back button ? Should it close the modal or go to previous page ? (Even more complex wizard steps inside modals)
  - I don't usually add modals to url
  - What I'm doing above is removing the modal url from history if we close it via UI, so we never get history like `page → modal → page → modal...`

- I don't think this is good UX, users shouldn't be constrained in any way. For me a better solution would be to persist the entries of the form.
  - I'm a big fan of keeping the state around and restoring later, but I don't think that applies to modals.
  - In this case we must ensure the user knows whether the operation was submitted or not.

- ## Just learned about how @excalidraw implements encryption by encrypting the data 
- https://twitter.com/christoomey/status/1351234746139947013
  - and then putting the key in the hash of the URL (which browsers don't send with the request). 
  - Self-contained security via browser features, so neat!
- Interesting, I didn’t think about adding it to the payload. 
  - That would solve the problem I was trying to avoid: increasing the length of the url. Thanks! Would you be interested in implementing it?

- ## [Open-source drawing tool – Excalidraw | Hacker News _202312](https://news.ycombinator.com/item?id=38499375)
- I like excalidraw for live discussions but if I want to make more detailed or better looking diagrams, I really enjoy these two tools:
  - For drag-and-drop/WYSIWYG, I really like DrawIO. 
  - For text-as-diagram, I think Mermaid wins this by default since GitHub added markdown support for these
- Excalidraw itself is also pretty cool as an embeddable widget, we recently built a cool real-time AI-accelerated drawing playground

# blogs

## 🔀 [Excalidraw: Building Excalidraw's P2P Collaboration Feature_202003](https://blog.excalidraw.com/building-excalidraw-p2p-collaboration-feature/)

- 协作编辑同一个shape时，协作算法并未特殊处理，可能会有数据丢失，但versionNonce保证了最终一致

- We did not want to store anything server-side. Therefore, we opted for a pseudo-P2P model, where a central server relays end-to-end encrypted messages to all the peers in the room, but does no centralized coordination.
  - our encrypted messages can be passed between the client and the server back to other clients as `ArrayBuffer`, so we don’t need to convert them to other data structures at any point in the transit.
  - when elements were added, we adopted an architecture of merging states when we receive them. 
    - local client A looks at all the ExcalidrawElement.ids it has locally, and all of the incoming ExcalidrawElement.ids, and creates a new ExcalidrawElement array containing the union of both the local and incoming set.
  - Peers would set `isDeleted` field to `true` to delete an element, and would filter the deleted elements out of the array at runtime.
    - we do remove any element with `isDeleted` set to `true` when saving to persistent storage, so long-lived drawings where this may become a problem are cleaned up.
  - Concurrent edits will still be lost, as our merge algorithm only looks at new elements being added or removed, and not changes to existing elements themselves.
    - when we merge multiple peers state together, we throw out old versions of each element and just keep the latest ones.
    - 👉🏻 This algorithm is simple but effective, and solved most of our collaboration problems.
  - The version number only solves race conditions when players are editing different elements concurrently. What if they’re editing the same element concurrently?
    - For Excalidraw, we don’t really care! We think this will be a pretty rare situation, and that users will tolerate some jankiness if it happens.
    - With that said, it is important that all peers converge on the same state. 
    - Any time we increment the version of an element, we set `versionNonce` to a random integer. 
    - At merge time, if we encounter two elements with the same version number but different data (i.e. two players editing the same element at the same time), we break the tie by favoring the one with the lower `versionNonce`. 
    - This ensures that one player will deterministically “win” on every peer.
  - One problem we haven’t solved yet is implementing multiplayer undo/redo. 
    - Our hack around this was to clear the undo/redo stack whenever you receive an update from a new peer.

## 🔒 [Excalidraw: End-to-End Encryption in the Browser_202003](https://blog.excalidraw.com/end-to-end-encryption/)

- Web Cryptography APIs are now widely available to all the browsers that let us implement this. 
  - That said, the APIs to deal with encryption, keys and binary data are not the most straightforward

## [Excalidraw: Deprecating Excalidraw Electron in favor of the Web version_202012](https://blog.excalidraw.com/deprecating-excalidraw-electron/)
