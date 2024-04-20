---
title: lib-editor-quill-issues
tags: [issues, quill]
created: 2024-04-15T16:03:08.745Z
modified: 2024-04-15T16:03:16.853Z
---

# lib-editor-quill-issues

# guide

# issues-stars
- ## 

- ## 

- ## 
# issues-high
- ## 

- ## 

- ## [How to add difference between ENTER and SHIFT+ENTER ](https://github.com/quilljs/quill/issues/1187)
- 201912: I must admit I was surprised when I realized that Shift + Enter does not work out of the box. 
  - Differentiating between newlines and paragraphs is why there are `<br> and <p>` tags in the first place, and they are not interchangeable. 
  - `<p>` tags can be styled, while `<br>` tags cannot. 
  - The difference between the two is a big part in styling HTML documents, and since Quill produces HTML, I expected it to support both.
  - I quite like Quill, and how easy it is to integrate - I will have a look at the solutions proposed so far to add this functionality, as everyone who will be using it in my project know how to use and need both paragraphs and newlines.

- I am using react-quill, so you might need to translate to vanilla usage if that's what you're doing but this very simple setup worked fine for me, no complicated selections, insertions or anything. Just an embed with a tag of br, inserted on shift-return.

- This is by far the best implementation of Shift + Enter for Quill
  - use Enter to insert paragraph, use Shift+Enter to insert break
  - both Enter and Shift+Enter preserve styles that were applied on previous line

- [Support for shift + enter ](https://github.com/quilljs/quill/issues/252)
# issues
- ## 

- ## [Window is scrolled to top after paste ](https://github.com/zenoamaro/react-quill/issues/394)
- This is not a react-quill issue, its a Quill issue. A simple search will show lots of threads on this across github and SO. There are 2 connected issues: scroll and flicker.

- 
- 

- ## [How to drag and drop blocks in quill _202112](https://github.com/quilljs/quill/issues/3507)
- 

# issues-done
- ## 

- ## 🐛🤼🏻 [2.0.0-dev quill drag text not working how make it drag text - Stack Overflow _202401](https://stackoverflow.com/questions/77725637/2-0-0-dev-quill-drag-text-not-working-how-make-it-drag-text)
- First of all, Quill intentionally blocked the dragging, so it is important to ensure that you have a proper use case before enabling it.
  - [Allow optional drag event enabling _201904](https://github.com/quilljs/quill/pull/2579)
  - Quill 2.0 disabled drag events by calling e.preventDefault() in the dragstart event handler ( `handleDragStart` ). 
  - This handler used to be in the Quill class, but has been moved to `Scroll` to allow overwriting. 
  - Note that this change applies only after 2.0.0-dev.4 (and 2.0.0-beta.0), so you can't use 2.0.0-dev.3.
- Once you've addressed the 'drag' issue, you also need to fix the 'drop' part. 
  - Method 1: Have the browser handle the insertion like Quill 1.3
  - Method 2: Instead of having the browser handle the elements' insertion, you could create a dragend/drop event handler that moves the dragged elements to their dropped position. (I don't know how, so I'll leave it for someone else who knows how to implement a correct one.)

- ## [Supporting selection of blocks in Quill (like Slab) _202104](https://github.com/quilljs/quill/issues/3324)

- ## [Drag and Drop event within editor will be supported? _202004](https://github.com/quilljs/quill/issues/3019)
  - I found it that quill prevent default the drag start in core/quill.js and scroll.js.
  - But I want to realize drag the text within editor, any suggestions?
