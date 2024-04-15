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

- ## 

- ## 
# issues-done
- ## 

- ## 

- ## 
