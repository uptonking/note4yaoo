---
title: lib-editor-rich-outline-docs
tags: [docs, outline-wiki]
created: 2021-09-09T18:29:59.214Z
modified: 2021-09-09T18:30:24.610Z
---

# lib-editor-rich-outline-docs

> The fastest wiki and knowledge base for growing teams.

# guide

# overview
- usecase
  - Documentation
  - Sales playbooks
  - Support scripts
  - Onboarding
  - HR documents
  - Meeting notes

- Outline allows you to organize documents in "collections", for example these could represent topics like Sales, Product, or HR. 
  - Within collections documents can be interlinked and deeply nested to easily build relationships within your knowledge base.
- You can start searching from anywhere with the CMD+K shortcut – then filter by time, author

- The heart of Outline is the document editor. 
  - If you’re comfortable writing markdown, then all of the shortcuts you are used to are supported
  - You can also paste markdown or html from elsewhere directly into a document.
  - The editor supports a variety of content blocks including images, tables, lists, quotes, videos, and more. 
  - Type "/" on an empty line or click on the "+" icon to trigger the block insert menu, you can keep typing to filter it down.

- Linking to another document automatically creates backlinks which are kept up-to-date and shown at the bottom of the document, 
  - so you can create a library of linked information and easily answer the question "which other documents link here?".

- [Revision history](https://docs.getoutline.com/s/guide/doc/revision-history-AiL6p22Ssq)
  - As documents are edited, Outline will automatically keep a record of revision history. 
  - At most, a version is recorded for every 5 minutes of editing.
  - Note that restoring a version will create another version and not rollback history to this point in time. In this way it is a non-destructive action.
# docs

## scaling

- [Horizontal scaling - Outline ](https://docs.getoutline.com/s/hosting/doc/horizontal-scaling-hkfU5Stao7)
  - Outline’s api, worker, and web processes are able to automatically scale horizontally – you can deploy as many instances as needed to handle traffic. 
  - collaboration however, is different due to it’s stateful nature…
  - If you would like to run Outline’s collaboration server in a horizontally distributed manner either for redundancy or large installation sizes an additional environment variable must be set: REDIS_COLLABORATION_URL – This should be the fully qualified url of a Redis server that will be used to syncronize edit transactions between processes.
  - [Improved horizontal scaling of collaborative servers  _202204](https://github.com/outline/outline/issues/3425)
    - I spent a lot of time working on the scaling extension for Hocuspocus, it is time to implement it in the backend.
# more
