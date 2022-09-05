---
title: lib-editor-prosemirror-issues
tags: [editor, issues, prosemirror]
created: 2021-06-12T02:40:02.657Z
modified: 2021-06-12T02:40:42.535Z
---

# lib-editor-prosemirror-issues

# issues-not-yet
- 测试一下哪个优先级更高：plugins中一个plugin.nodeViews vs EditorView的props.nodeViews
# issues
- ## 

- ## 

- ## 

- ## 

- ## Tooltip inline menu fights with iOS selection menu
- https://github.com/ProseMirror/prosemirror/issues/7
- Since control over the tooltip menu is impossible for web pages, the **recommendation** here is to either not use the tooltip menu on iOS, or set its `position` option to "below" to prevent the two tooltips from overlapping.

- ## Is there any way using keymap when ‘editable’ of the view is false
- https://discuss.prosemirror.net/t/is-there-any-way-using-keymap-when-editable-of-the-view-is-false/3317
- With `editable: false` , the `contenteditable` attribute on the document node is removed, which by default makes the browser disable keyboard focus for the element. 
  - When the node isn’t focused, it doesn’t even receive keyboard events, so it’s hard to implement any keybindings for it.
  - You could use the `attributes` prop  to add a `tabIndex=0` attribute to your editor to make it focusable. 
  - But this might lead to some other key bindings also firing, and if those do change the document, `editable: false` (which works only on the DOM) level won’t stop them.

- ## How to: input-like placeholder behavior
- https://discuss.prosemirror.net/t/how-to-input-like-placeholder-behavior/705
  - text that will be viewable when textContent === '' and automatically appears / is removed when that changes. 
- 可以借助 decorations
- if you click on the decoration it does focus the editor, but the cursor is hidden, is there a way to fix this?
  - That’s a browser issue, I guess – cursor drawing around uneditable elements is quite buggy. You could try wrapping the placeholder in an absolutely positioned element, that sometimes works around this bug.
- In principle the way ProseMirror plugins works should make it impossible to have accidental extra reflows – the `decorations` prop is called when the view is updated, so any decorations it returns are immediately drawn.
- Coming in with a different angle, If you use a nodeview you can render a class manually and ignore the mutation. That way if you have `!node.content.size` you can set the class on, or off. Removes need for decorations and whatnot. Thats if you just have some `p` elements that you want to have placeholders for, you can just use CSS with a placeholder class

- ##  `.toDOM` can also return a string or a DOM node, which are simply used as-is. Is it possible to define holes even when toDOM returns a DOM node?
- https://stackoverflow.com/questions/59769774
  - .toDOM method of a schema usually returns a nested array that describes how to render the node to DOM, similar to a "virtual dom" data structure. 
  - This data structure can also contain what ProseMirror calls a "hole", represented by `0` . 
  - This hole is where ProseMirror will insert the content of the node, such as text or other nodes.
- Is it possible to define holes even when toDOM returns a DOM node?
  - No. Defining a hole makes sense only when there are multiple children DOM elements inside the DOM representation of a given ProseMirror Node. 
  - Defining a hole tells PM where to insert the next child PM Node.

```JS
imageAlt: {
  toDOM: () => ['div', ['h2', 'Alt'],
    ['div', 0]
  ],
  content: 'inline*',
  defining: true,
  isolating: true
}

// This means that imageAlt will render like this:

<div>
    <h2>Alt</h2>
    <div>Content Goes Here</div>
</div>
```

- Children PM Nodes would have been inserted under either `h2` or `div`; so we explicitly pointed `h2` to contain the child PM Node.
- But in the case where `toDOM()` returns a `dom.Node` but not an array, that means there is only one option, hence there is no need to define a hole. 
  - A `dom.Node` is always 1 level deep and any child ProseMirror Node will be the direct child.

- ## Customizing Schema for Table
- https://discuss.prosemirror.net/t/customizing-schema-for-table/1991
  - I want to change how the table node is rendered. 
  - For example: I want the `table` element to have a class of `table` .
- I guess you’re still including the `columnResizing` addon? **That will define a node view for tables which will override your `toDOM` method**.
  - The tables module builds on a bunch of assumptions about the kind of tables it is representing, and I wouldn’t be surprised if some of its features, like column widths, stop working when you change its DOM representation, 
  - but in principle if you disable those features you should be able to do what you want here.
- I fixed this by creating a class that extends the `TableView` , seems a little bit hacky but it works.
  - and then pass the new class as the View to the the `ColumnResizing` plugin

- ## prosemirror and mermaid
- https://gitter.im/ProseMirror/prosemirror?at=59c2cbef614889d47520666a
- There are some filters for tools like pandoc that can also render them to different image formats, and the images can be embedded into transformed document formats (like PDF/DocX). 
  - Mermaid itself is a combination of a set of DSLs for different diagram types and and engine that renders the diagrams with D3.js to a SVG canvas. 
  - There's also a Markdown-previewer extension for Visual Studio Code that lets you preview the rendered markdown + diagrams on the fly, 
- Now, to my question; I've looked at the Prosemirror example where there's an option to switch between WYSIWYG and markdown. 
  - Now, is it doable to create a plugin for Prosemirror that could inline HTML canvas'es inside a contenteditable element? 
  - My goal would be that the dev could create/edit the diagrams in plain mermaid-DSL embeded in fenced code sections in Markdown, and switch over to WYSIWYG and see the diagrams inlined (but readonly).
- so it is technically feasible to have a canvas element floating inside a contenteditable element?
  - I can’t think of any reason why not.

- ## How to create a nodetype consist of an image and text with inline editing experience?
- https://discuss.prosemirror.net/t/how-to-create-a-nodetype-consist-of-an-image-and-text-with-inline-editing-experience/1326
- ProseMirror needs to be able to ‘fix’ documents to conform to the schema, for example if editing somehow yields an image wrapper node with only a paragraph inside of it, it must generate an image to satisfy the schema constraint. 
  - But because images contain attributes without a default value, it can’t.
  - One solution would be to model the node as a captioned image instead of a wrapper, with its own image src (an possibly alt etc) attribute, and inline* content, rendering as something like ["div", ["img", {....}], ["p", 0]]. 
  - That way, the node can’t get in a state where the image is missing, since it’s not part of its editable content.
  - Alternatively, use 'image? p' as content expression, so that the image isn’t required and doesn’t ever need to be generated.

- ## ProseMirror for editing page layout
- https://discuss.prosemirror.net/t/prosemirror-for-editing-page-layout/1045
  - I’m thinking about using ProseMirror for editing the layout of a blog post or similar. 
- This is probably possible — ProseMirror isn’t really written for showing content precisely as it will appear in some final output, since we take the approach that during editing you’re more interested in semantic information than in layout, but I expect it’s flexible enough to get something like this working.
- I guess dragging blocks into the editor could be made to trigger structural changes to the document. So yes, I think this’ll work well with ProseMirror. Embedding things that aren’t editable is definitely supported.
  - Depending on what your HTML looks like, contentEditable may misbehave for some complex things like having things positioned in fancy ways. You’ll have to experiment and see.

- ## Multi-column layouts
- https://discuss.prosemirror.net/t/multi-column-layouts/44
- if it is possible to have multi-column/grid layouts (not tables!) inside a contenteditable. All of them told me: nope, very messy with contenteditable.
- ProseMirror’s approach is to mostly limit the editing view to a semantic representation of the document, and leave the presentation to other parts of the pipeline.
- Using the `column-count` CSS property on the editor view works just fine.
  - 此属性大约100%的浏览器支持
  - 但给的示例大多是用来自动拆分文本，不清楚对图文混排的支持
