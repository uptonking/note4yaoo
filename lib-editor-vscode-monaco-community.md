---
title: lib-editor-vscode-monaco-community
tags: [community, editor, monaco-editor]
created: 2023-01-21T18:56:44.012Z
modified: 2023-01-21T18:57:13.106Z
---

# lib-editor-vscode-monaco-community

# guide

# discuss
- ## 

- ## 

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
