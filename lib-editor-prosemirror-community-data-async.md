---
title: lib-editor-prosemirror-community-data-async
tags: [community, data-model, prosemirror]
created: 2022-09-05T03:23:36.125Z
modified: 2022-10-03T10:47:44.104Z
---

# lib-editor-prosemirror-community-data-async

# guide

# discuss
- ## 

- ## 

- ## 

- ## my question is whether PM uses timeouts internally to wait for things, especially during initialisation but also during transactions and state updates. 
- https://discuss.prosemirror.net/t/timeouts-and-synchronising-external-dom-state/3928
  - And if yes, if there’s an API I could use to get a callback when an EditorView is fully initialised and attached to the DOM element.
- 👉🏻 ProseMirror updates (and initializes) synchronously. 
  - It does in some cases wait a moment before responding to DOM mutations in order to allow events related to the same change (which the browser models as a sequence of mutations and events) to accumulate, and has a few timeouts internally for other hacks, but that doesn’t sound like it would be the issue here.
- if I stick to responding to various PM events I should be back in synchronous land?
  - Yes, the API should protect you from these almost entirely (except possibly when you’re doing your own thing in response to DOM events without preventDefault-ing them).

- ## Creating Plugin that make request to backend
- https://discuss.prosemirror.net/t/creating-plugin-that-make-request-to-backend/4684
- 👉🏻 I would keep the asynchronous HTTP calls out of your plugins. 
  - Instead, use `dispatchTransaction` to get any updates from the editor you need. 
  - When such an update comes, you can send the document (or changes) to the server.
  - If you need to apply a change to the document as a result of such an HTTP call, you would create a new Transaction and dispatch that to the view. 👉🏻 The collab demo on the website is an example of this.

- ## Async toDOM
- https://discuss.prosemirror.net/t/async-todom/2762
  - href: await this.getPostLink(node.attrs.post)
- I am assuming this would make the editor quite slow to render, especially if it is re-rendered because something is changed. There are two things that come to mind:
  - 👉🏻 Save the URL in an attribute, when you load the document (or on some other action) run transactions on the document replacing all post URLs with current ones (you’d be replacing the attribute).
  - 👉🏻 Create a fixed route a la yourserver/post/ID123 and then let the server resolve to the current URL when the link is followed

- I’m only doing this on the website side, so not in the editor itself, because it’s nod required there. If there is a nicer way with ProseMirror I’m happy to hear so.
  - That sounds very reasonable if you need the information at the time of publishing. ProseMirror has no prescriptive way in that respect. The only thing it asks is, that you use transformations within the editor instead of just replacing nodes in its document tree - of course when you do the replacement just for rendering that should be fine.
  - At my job, we actually only render the JSON, not the ProseMirror state itself (and we do it server side so it can be cached).  渲染层只用json，而不是readOnly的编辑器
- That’s how I did it before as well. I built a block editor which saves to json on the server. On the server the content got parsed for short codes, i.e. code.post(click here).id(95), and the parsed content then is cached. It works fine, but the short codes aren’t very user friendly, so I went this route. Also hoping I can place the short code in the content with a Mark for example and then just have it displayed differently in the editor. That way I can still parse and cache as before. Do you see this being possible (and not being too hard) with ProseMirror?
  - ProseMirror is wonderful at editing text and even keeping attributes and marks up to date. What it doesn’t do well is keeping all the external metadata up to date because each modification to the document requires a transaction (e.g. I would save comment ids, links src etc directly in the document but would save comment texts and other information in a separate place).
  - I would ask myself: Is this something that is changed in the editor? Then definitely keep that in marks or node attributes and update the document through transactions.
  - Is this something that is changed in an outside system? Then probably it is best to just store an ID in ProseMirror where you want the link to go and then replace the metadata post editing.
  - Maybe someone else gets it better than me, or you may want to post a screenshot or something before I can recommend a pattern.
