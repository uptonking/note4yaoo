---
title: lib-editor-typewriter-dev
tags: [text-editor, typewriter]
created: 2023-02-09T12:24:05.159Z
modified: 2023-02-09T12:24:23.549Z
---

# lib-editor-typewriter-dev

# guide

- features
  - collab
  - virtual render

- 技术要点
  - 模型层TextDocument将Delta中的op数组按换行符拆分为blocks/lines数组
  - virtual-render只渲染指定区域内的元素
  - 默认render使用的是virtual dom
  - 选区同步基于浏览器的事件
  - 协作基于 json-patch + 简化版ot

- 渲染长文档的思路
  - virtualized render
    - 参考 ajaxorg/ace、codemirror、typewriter
    - 虚拟渲染能提高安全性?
  - defer render, 懒加载，viewport内才加载，按需请求再加载
    - 持久化分页后的数据，便可以按固定高度实现virtual render

- virtualized render cons
  - 影响浏览器自带的功能，如页面内查找
  - 锚点自动滚动，如生成标题目录toc，评论

- typewriter的delta结构就是一系列op集合和操作，非常类似经典OT算法
# dev
- typewriter /308Star/MIT/202301/ts
  - https://github.com/typewriter-editor/typewriter
  - A rich text editor based off of Quill.js and Ultradom, and using Svelte for UI.
  - 依赖 svelte、popperjs2、typewriter/delta
  - Built on the same data model as Quill.js, the Delta format, and using a tiny virtual DOM, Superfine, Typewriter aims to make custom rich text editors faster, easier, and more powerful
# changelog

## [prepare for 1.0 release_20210120](https://github.com/typewriter-editor/typewriter/pull/56)

- It's time to get Typewriter ready for a 1.0 release after a few years of indecisiveness on direction. This represents a major overhaul of the library after much learning.

- We are pivoting away from a monorepo with multiple packages back to a single package. 
  - This simplifies usage, the codebase, and deployment. 
  - We will have one npm package as before at `typewriter-editor` and `@typewriter/*` will be deprecated.
- As part of simplifying into 1 package, we've replaced `Paper` with the new `Typeset` interface which is similar and better named for what it represents. It combines the type definitions with their rendering and display information to simplify creation of new types for users.

- Instead of moving to a new Delta format or changing how newlines work in the existing Delta format, we are adding a new data format that builds on top of Delta and can be converted to and from Delta `TextDocument`. 
  - It just breaks Delta into lines and adds the selection information to the document. 
  - Deltas are still used in changes and for collaborative editing.

- To support atomic changes, we've added a `TextChange` class to encapsulate a single atomic change which could be a single character typed (along with the new selection) or a Replace-All operation on the document. This simplifies the events and history module.

- Since changes include selection info, we've simplified the events to a `changing` event (before a change is made and which can be canceled with `event.preventDefault()`) and a `change` event which is dispatched after the change is made. 
  - There is also a `changed` event which is dispatched after change to allow some things to respond after everything else has, though I don't anticipate this is needed by most.

- 👉🏻 We have moved user input, copy, paste, selection, rendering, and decorations, all into modules. `View` is no more. 
  - It turns out, very little is needed in the core editor and doing this allows these pieces to be replaced with custom implementations, such as replacing rendering with virtual rendering.

- A new keyboard module resolves Keyboard module? by both adding shortcut strings to the keydown event and handling basic editor input such as Enter & Delete.

- 👉🏻 We've moved back to using the browser `MutationObserver` for handling user input with a fallback to the `input` event for Firefox. 
  - This gives us the best support for text composition and the buggy Android GBoard keyboard which is default on most Android devices. 
  - But this is all handled in the input module which can be replaced as needed.

- 👉🏻 We've given up the dream of using Svelte to render the contents of the text editor, sticking with a small virtual DOM. 
  - This is part of the editor's core feature since Typesets include a function for rendering to the vDOM. 
  - The rendering module can be replaced, but it is assumed that all rendering will be done with the vDOM provided.

- And finally, we've embraced Svelte as the supported way to create UI for the editor and provided several renderless components which make it dead simple to add toolbars, hover menus, and inline menus. Recreating the Medium editor (which seems to be the thing to do) with the provided tools is very simple.
# docs

## overview

- Built on the same data model as Quill.js, the Delta format, and using a tiny virtual DOM, Superfine, Typewriter aims to make custom rich text editors faster, easier, and more powerful. 

- Need something out-of-the-box? Typewriter is not for you. 
  - Typewriter provides the tools to easily create your own custom editor. 

- Typewriter was built for Dabble, an in-browser app for novelists to write their stories (think Google Docs but just for Novels).
- Dabble required the ability to 
  - customize the editor to look and work a certain way, 
  - great performance on large documents, 
  - a mechanism for decorating the display without altering the underlying data (for find-and-replace and collaboration), 
  - and conceptual simplicity so Dabble could be customized without brain meltdown. 
- Some of the editors available provided some of these things, but none provided all. 
  - And none provided the performance needed for working smoothly with documents 10k+ words long on low-powered Chromebooks and mobile devices.

## [Why Typewriter?](https://github.com/typewriter-editor/typewriter)

- A new class of rich text editors for the web has emerged in recent years backed by their own data model and using `ContentEditable` as an input mechanism. 
  - These editors provide consistent display across every browser, bypass many of the bugs inherent with ContentEditable, give the ability to create your own custom editor with the building blocks provided, and allow realtime updates with collaborators (using operational transforms or CRDTs).

- Some of these editors are dependent on a large framework such as Vue or React. 
  - These are good choices if you are already paying the cost of the framework overhead. 
  - If you are not, they add a lot of code size for your editor. 
  - Examples of these are React’s Draft.js and Slate.

- Some of these editors—such as ProseMirror and CKEditor5—use a **hierarchical data model** similar to HTML. 
  - This gives complete control over what is allowed in the editor but comes with a high complexity cost. 
  - It is more difficult to conceptualize a hierarchical document that can be any depth than it is a plain text document, a flat list of characters. 
  - Because of this, it can also be more difficult to customize editors using a hierarchical data model because the API is more complex, but ultimately it is more flexible and powerful.

- Other editors such as Quill.js and Medium's editor use a **linear data model** which is much easier to reason about and simpler to work with. 
  - These editors do not allow as much flexibility over the output as their hierarchical cousins, but many (perhaps most) types of content can be represented linearly, and you don’t need a PhD in the editor to customize it.

- Typewriter pulls bits from all these editors and takes the best of each of them.
- 👉🏻 Typewriter goes with the linear approach, building off the same data model as Quill.js, the [Delta](https://github.com/quilljs/delta) format.
  - Typewriter modifies Delta to provide better memory usage with an immutable approach and adds a layer on top `TextDocument`, which splits a `Delta` document into lines to add even more memory benefits for large documents. 
  - This model is more similar to the Medium editor (which is line-based) and provides greater runtime performance, especially on larger documents. 
  - It also paves the way for document virtualization which allows documents with hundreds of thousands of words to render as quickly as a hundred word document and gives responsive typing.

- Typewriter avoids large frameworks by using a tiny virtual DOM for rendering its own content

- Typewriter adds Decorations like ProseMirror which support changes to how the document is displayed without changing the document. 
  - It does this in a performant manner. 
  - This is used for features like highlighting find-replace words or inserting a collaborator's cursor.

- 👉🏻 The Current State of Typewriter
  - Typewriter has recently undergone a huge rewrite, moving from using just the `Delta` format to its new `TextDocument` model for enhanced performance in decorations and rendering and opening the way for even more performance with virtualized rendering. 
  - Many smaller things learned from the previous iterations have been incorporated. There are still bugs and may be some API changes, but those should decrease as Typewriter settles into its new trajectory.
  - Virtualized rendering is buggy and not ready for production.

## guide

- To stay conceptually simple, Typewriter uses a list-like internal data format based off the Delta format rather than a hierarchical data model.
- Typewriter also uses immutable data to keep code simpler and increase performance.

- Text Document represents the contents and user selection of Typewriter in memory. The TextDocument and TextChange APIs can be used in headless environments (i.e. Node.js).
- Editor is the core of Typewriter. It manages the contents, dispatches change events, and provides modules which render the contents to the DOM, handle keyboard shortcuts, add undo/redo, and more.

- Typeset holds the rules for what types of content is allowed in the editor and how that content is mapped to HTML and back again.

- an index in Typewriter represents the location between characters, not a character itself, so an index of 0 points to the location before the first character. 
  - It is the location where the text cursor would appear.

- range—a tuple of indexes (an array with two indexes) with the start and end of the section.
  - Any time we talk about ranges with Typewriter we are talking about an array with two numbers. 
  - The Editor's `selection` property is a range.
- Ranges don't have to be in document order. 
  - [ 0, 5 ] is equivalent to [ 5, 0 ] for most editing operations. 
  - The Editor will "normalize" ranges when it needs to, placing the lower index before the higher, when it runs change operations that need it.

- Typewriter uses the Delta format, borrowed from Quill.js, and builds on top of it to create its TextDocument.
- Typewriter ships with its own version of Delta that has been slightly modified for better performance for Typewriter's immutable use and to support deep merging of attributes for comment support. 

- A Delta can represent a whole document and can represent changes to a document. 
- Deltas are a representation of the document which separates structure from appearance and can be stored as JSON.
- Deltas are human readable and can be deterministically converted to and from HTML representations using Typesets
- TextDocument can be converted to and from Delta

- When parsing HTML (such as on a Paste operation) Typewriter will throw out any elements that don't match a Typeset Type. This keeps your data clean.

- Empty blocks are always filled with a `<br>` element to keep them open, otherwise they collapse and the user can't click into them to enter any text.
