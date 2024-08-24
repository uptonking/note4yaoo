---
title: lib-ide-vscode-monaco-community
tags: [community, editor, monaco-editor]
created: 2023-01-21T18:56:44.012Z
modified: 2024-08-24T16:17:41.676Z
---

# lib-ide-vscode-monaco-community

# guide

# discuss-stars
- ##

- ##

- ## 📱 [Any Plan for Mobile · Issue · microsoft/monaco-editor _201610](https://github.com/microsoft/monaco-editor/issues/246)
-
-
-

# discuss
- ##

- ##

- ##

- ## [Is it possible to create WYSIWYG editor using monaco? - Stack Overflow](https://stackoverflow.com/questions/64549041/is-it-possible-to-create-wysiwyg-editor-using-monaco)
- Monaco is a code editor, created for helping to write source code in any form.
  - It has no support for multiple fonts, tables etc., nor can you draw arbitrary graphics in it (even though there are means to embed someting, but that's a different thing).

- ## monaco editor is a great piece of software, I wish it was more open for customization though
- https://twitter.com/alsugak/status/1566055190498795520
  - The source code is OO madness, everything is private.
  - So if you want to do something interesting, you either need to depend on the internals, or reimplement the internal behavior yourself, sad

- Compare that with Quill.js for example, which has its core text changes format (delta) and its algebra in a separate package, so anyone could use it

- Compare it with ProseMirror, which have own document schema, model and good layer separation between view/state/etc

- ## [How does Monaco Editor enable text editing on a web page?_201810](https://www.mozzafiller.com/posts/how-does-monaco-editor-enable-text-editing-on-a-web-page)
- In other browser-based text editors like Quill.js, Quip, and Draft.js, they use the contenteditable attribute to enable editing
  - But in Monaco there is not one `contenteditable` attribute
- Turns out Monaco is pulling a sneaky trick. There’s an invisible `<textarea>` element on the page which is what you’re actually typing into
  - There is also CSS attached to make the box 0px x 0px and have everything completely transparent.
  - Monaco gets all of your keystrokes from there and renders the nice HTML you actually see.
