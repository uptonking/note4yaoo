---
title: lib-editor-quill-community-delta-format
tags: [community, delta-format, quill]
created: 2023-11-27T15:58:00.212Z
modified: 2023-11-27T15:58:19.532Z
---

# lib-editor-quill-community-delta-format

# guide

# discuss-stars
- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## [How to append an existing delta to the end of current Quill content _201711](https://github.com/quilljs/quill/issues/1838)
- I have stored existing Quill content as JSON in a database. I need to append this to the end of the existing Quill content and have been unable to do it so far. UpdateContents(delta) adds it to the beginning of the current content and I have not been successful in specifying an insertion point.

```JS
const Delta = Quill.import('delta');
const passedDelta = new Delta(JSON.parse(passedValue));
const existingDelta = this.get("quill").getContents()
const combinedDelta = existingDelta.concat(passedDelta);
this.get("quill").setContents(combinedDelta)
```

- ## [Render quill delta without instantiating an editor](https://github.com/quilljs/quill/issues/993)
- Current best solution seems to be to convert the deltas to HTML
- The reason why I do not choose to use Quill editor currently is that I got stuck while trying to convert delta to pure HTML for display purpose
- As with other people, though, my main stumbling block for using it is that there are actually no guides or demos showing how to use it where the use-case is to have editors create content and have that content rendered in HTML for reading by consumers.
  - The path from editing to rendering isn't clear.

- I wrote my own delta renderer; it's not perfect, and its API needs a serious overhaul (very hard to customize) but it has thorough tests and, with effort, you can teach it to handle custom formats
  - https://github.com/xeger/quill-deltacvt
    - Converts Quill Delta to HTML (or other formats) without depending on quill, parchment or quill-delta.
- I experimented with using JSDom plus an actual Quill instance for delta->HTML, and although this is good for backend use, I needed something that was synchronous and instantaneous for use in browsers where the Quill editor itself is not available.

- Spent over a week trying to figure out what was the best solution for react, and I guess it's still creating a readonly quill and hoping there's no XSS issues? 
  - Some people have mentioned converting deltas to html, but that's really not secure. And on JS frameworks like ReactJS, you really want to avoid using dangerouslySetInnerHTML. (And there's nothing that will convert a delta to JSX)
