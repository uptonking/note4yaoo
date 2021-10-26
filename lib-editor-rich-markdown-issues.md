---
title: lib-editor-rich-markdown-issues
tags: [issues, markdown, rich-markdown-editor]
created: '2021-06-02T10:29:47.978Z'
modified: '2021-06-02T10:30:09.481Z'
---

# lib-editor-rich-markdown-issues

# issues-not-yet
- ## allow `/` to be used anywhere, not just a new line
  - https://github.com/outline/rich-markdown-editor/issues/218

- ## Disable extensions
- https://github.com/outline/rich-markdown-editor/pull/438
  - any extension can be disabled, even Doc or Text, but hey, careful what you wish for

- ## Method to customise markdown serialisation
- https://github.com/outline/rich-markdown-editor/issues/183
  - I'm currently integrating the editor into an existing site which already has a body of content
  - The existing markdown has a few conventions, such as using dashes for unordered lists and underscores for emphasis
  - Any time I open an existing document to edit in rich-text-editor, as well as any changes I make, the editor replaces those characters with asterisks.
  - What options are available for customising the editor's markdown serialisation preferences?
- There is no configuration for this and I don't plan on incorporating any I'm afraid. 
  - The editor outputs compliant Markdown and a proliferation of options would result in a more bug-prone implementation that's difficult to maintain.

- ## Support dynamic loading of languages for code blocks
- https://github.com/outline/rich-markdown-editor/issues/152
-  I think in order to support more languages we need to figure out how to dynamically load the language files into the editor, once that's in place then we can support many more languages without increasing the initial download size 

- ## Content is not rendered when using SSR 
- https://github.com/outline/rich-markdown-editor/issues/303
- Prosemirror does not support node, so to achieve this we'd have to write a renderer that emulates the output of Prosemirror – Remirror has done a good job of this, so it could be an inspiration for the work
- ## render method is not arrow function 不应该用
- https://github.com/outline/rich-markdown-editor/pull/500
  - change `render = () => {}` to `render() {}`, is able to Inheritance Inversion Editor
  - now it's ok to use `<>{super.render()}</>`
# issues
- ## 

- ## 

- ## Collapsible headings
- https://github.com/outline/rich-markdown-editor/issues/169
  - The way this should likely work is to have "collapsing" a heading add a **Prosemirror decoration** to everything between the heading and the next one of the same level or above. 
  - The decoration can add a `className` which hides the content.

- ## Floating toolbar gets covered by native toolbar on text selection in android
- https://github.com/outline/rich-markdown-editor/issues/462
- In Notion, the android app handles this beautifully by showing a toolbar attached to the top of the keyboard (or at the bottom of the page).
- I think positioning the toolbar using `position: fixed; bottom: 0` should work.

- ## Override Styles
- https://github.com/outline/rich-markdown-editor/issues/58
- I'm using Material UI components and I'd like to stick to those styles without your CSS being applied over it
- I ended up using patch-package to overwrite things, might be helpful for you too
  - I also ended up using a patch-package, this works well, but I think some API for injecting either custom components or styling information would be nice.
- Glad you found a solution. You can also inject custom components by passing a plugin into the editor that implements a `renderNode` method. You could use the existing `renderNode` implementation to base it off.
- I'd recommend taking a look at a more flexible package – this is purposefully a very opinionated editor. Some good alternatives are: TipTap and Remirror

- ## feat: Image styling based on preset classes
- https://github.com/outline/rich-markdown-editor/pull/345
- I really want this feature, as having massive images everywhere makes our pages look really bad
  - Potentially controversial: It re-uses the standard `title` part of the image tag to allow the user to define a class that controls the style of the image
  - In future this could become something easily controlled by a pop-up tool bar when you click on the image
