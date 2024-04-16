---
title: lib-editor-quill-community-collab
tags: [collaboration, community, quill]
created: 2023-11-27T15:54:48.383Z
modified: 2023-11-27T15:55:06.815Z
---

# lib-editor-quill-community-collab

# guide

# discuss-stars
- ## 

- ## 

- ## [Enhancement: Provide a way to track changes in editor · KillerCodeMonkey/ngx-quill_201909](https://github.com/KillerCodeMonkey/ngx-quill/issues/524)
- just listen to the output you want: onContentChanged, onEditorChanged or just grab the editor instance in the onEditorCreated output and call getContent

- [Quill Diff codepen](https://codepen.io/percipient24/pen/eEBOjG)
# discuss
- ## 

- ## 

- ## [What is the best way to modify text on a text-change event in Quill? _201904](https://github.com/quilljs/quill/issues/2558)
- Before Quill officially supports this, a workaround could be perform the changes with `queueMicrotask`

```JS
quill.on(Quill.events.TEXT_CHANGE, () => {
  queueMicrotask(() => {
    quill.updateContents( /* your changes */ );
  });
});
```

- You actually can't do that. Quill uses contenteditable and DOM mutation listeners (as far as I know). So DOM updates first and mutation events trigger Delta model updates.
  - In some cases you can use keyboard bindings to prevent DOM changes and change Delta first. I think we need pretty complex input interceptor.

- ## [Multiple Cursors Module ](https://github.com/quilljs/quill/issues/918)
- I'm having success with the quill-cursors module

- ## 🔀 [Quill Track Changes _201912](https://github.com/quilljs/quill/issues/2858)
- 
- 

- ## [How do I perform track changes in the quill editor just like Google docs? - Stack Overflow](https://stackoverflow.com/questions/58887843/how-do-i-perform-track-changes-in-the-quill-editor-just-like-google-docs)
- We tried to implement track changes / suggestions with QuillJS and came relatively far. But in the end it did not really work, since OT (Operational Transform, the format for syncing the changes) does not support hierarchical structures. The
  - Team from CKEditor changed the OT to support this. But unfortunately it seems to be a lot of work and their code is closed
  - Also Google solved it with OT, but also their code is not open. 
  - So to my knowledge there is up to today no Open Source solution to solve track changes / suggestions with html. And no one seems to be willing to do this, since the effort seems to be very high. So our conclusion: We stopped with this approach.

- Prosemirror has also a relative positioning format, but it's not OT, they call it a step. This seems to be more flexible and the doc structure of Prosemirror is similar to the DOM structure of a html document.

- Other approaches / inspirations
  - NIB
  - Fidus Writer
  - Wax Prosemirror
