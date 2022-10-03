---
title: lib-collab-blog-stars
tags: [blog, collaboration]
created: 2021-10-14T11:18:06.356Z
modified: 2022-04-05T10:10:22.091Z
---

# lib-collab-blog-stars

# guide

# [To OT or CRDT, that is the question_202001](https://www.tiny.cloud/blog/real-time-collaboration-ot-vs-crdt/)
- Conclusions
- CRDT is the holy grail of collaboration, it's an active area of research, and the prospect of peer-to-peer editing with end-to-end encryption is an exciting one. 
  - The technology isn't ready for our needs yet, but I believe in the future some incredible products will be made possible. 
  - In the meantime TinyMCE will rely on OT for collaboration, coming later this year.

- [Real-time collaboration is the new responsive design_20212](https://www.tiny.cloud/blog/real-time-collaboration-essential/)

- [How to migrate from Slate.js to TinyMCE_202209](https://www.tiny.cloud/blog/migrate-from-slatejs-to-tinymce/)
- The Real-Time Collaboration plugin built for TinyMCE makes use of Slate.js for the core model.
# [Collaboration needs a clean Slate_202002](https://www.tiny.cloud/blog/real-time-collaborative-editing-slate-js/)
- 👉🏻️ Note: this model will only be used for RTC, not the default editing experience

- Our real-time collaboration project has been split into a collection of sub-projects:
  - A custom VDOM rendering engine for the Slate model, and reverse-map logic for selection and content input, targeting a pure ContentEditable div so it is not TinyMCE specific
  - An implementation of low-level editor features built on Slate core APIs
  - A layer that loads TinyMCE configuration and content to set up and compose the low-level features into a working editor
  - Collaboration control (transforms, cursors, server interaction)
  - Hooks in the TinyMCE core to relinquish control of ContentEditable and redirect all model APIs to the external RTC code
