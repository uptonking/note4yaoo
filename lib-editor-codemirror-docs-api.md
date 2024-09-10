---
title: lib-editor-codemirror-docs-api
tags: [api, codemirror, docs]
created: 2024-09-10T00:42:58.735Z
modified: 2024-09-10T00:43:36.318Z
---

# lib-editor-codemirror-docs-api

# guide

# overview

# api-view

- deco-mark
  - Syntax highlighting
  - add some attributes or wrapping DOM element 
- deco-widget
  - insert a DOM element in editor: inline elements or blocks
  - block-level decorations should not have vertical margins, and if you dynamically change their height, you should make sure to call requestMeasure, so that the editor can update its information about its vertical layout.
- deco-replacing 可以修改多行
  - code folding or replacing an element in the text with something else
  - possible to display a widget instead of the replaced text
- deco-line 修改一行
  - influence the attributes of the DOM element that wraps the line
- Decorations that significantly change the vertical layout of the editor, for example by replacing line breaks or inserting block widgets, must be provided directly, since indirect decorations are only retrieved after the viewport has been computed.
  - Indirect decorations are appropriate for things like syntax highlighting or search match highlighting, where you might want to just render the decorations inside the viewport or the current visible ranges

- widget side
  - When this is positive, the widget will be drawn after the cursor if the cursor is on the same position. Otherwise, it'll be drawn before it. 
  - When multiple widgets sit at the same position, their side values will determine their ordering—those with a lower value come first. 
  - Defaults to 0. May not be more than 10000 or less than -10000
- widget inlineOrder
  - By default, to avoid unintended mixing of block and inline widgets, 👉 block widgets with a positive side are always drawn after all inline widgets at that position, and those with a non-positive side before inline widgets. 
  - Setting this option to true for a block widget will turn this off and cause it to be rendered between the inline widgets, ordered by side.

- if you dynamically change their height, you should make sure to call requestMeasure, so that the editor can update its information about its vertical layout.

- 
- 
- 
- 
- 
- 
- 

# api
- 🧩 Annotations are tagged values that are used to add metadata to transactions in an extensible way. 
  - They should be used to model things that **effect the entire transaction** (such as its time stamp or information about its origin). 
  - For effects that happen alongside the other changes made by the transaction, state effects are more appropriate.
- 🧩 State effects can be used to represent additional effects associated with a transaction. 
  - They are often useful to model changes to custom state fields, when those changes aren't implicit in document or selection changes.

- 
- 
- 
- 
- 
- 

# more
