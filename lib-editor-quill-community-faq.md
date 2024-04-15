---
title: lib-editor-quill-community-faq
tags: [community, faq, quill]
created: 2024-04-15T15:48:54.784Z
modified: 2024-04-15T15:49:07.504Z
---

# lib-editor-quill-community-faq

# guide

# discuss-stars
- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## 

- ## [Correct way to delete all text content (everything) and clear the editor _202303](https://github.com/quilljs/quill/issues/3758)
- `quill.deleteText(0, quill.getLength())` would be simplest way. 
  - `quill.setContents(new Delta().insert('\n'))` also gives you the same result though.

- ## [How to clear the contents in the editor? _201711](https://github.com/quilljs/quill/issues/1821)
- `quill.setContents([{ insert: '\n' }]);`

- You can also `setContents([])` and `setText('')` which will clear the text. Internally Quill's data model requires at least `\n` so this will be added for you.
