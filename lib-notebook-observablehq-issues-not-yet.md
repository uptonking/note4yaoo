---
title: lib-notebook-observablehq-issues-not-yet
tags: [not-yet, observablehq]
created: '2021-05-22T19:54:41.082Z'
modified: '2021-05-22T19:55:00.238Z'
---

# lib-notebook-observablehq-issues-not-yet

# issues-not-yet

- ## View-only mode?

- 未解决的问题
  - 隐藏了代码编辑器后，cell name仍然会被渲染出来

- https://talk.observablehq.com/t/view-only-mode/447
- To keep the original data private, I recommend aggregating your data in a separate private notebook (which you don’t publish; or, do the aggregation outside of Observable), and then only make the aggregate data public. 
  - Since the aggregate data contains the same information as your visualization, this approach would not expose any new information—the data and the visualization are informationally equivalent.
- There currently isn’t any way to hide the code from readers — aside from resorting to dirty tricks, like stuffing all of it into viewof cells that run code as a side effect and return a Markdown paragraph as the view.
  - I’d certainly be interested to hear more about the workflow that you’re looking for, with this example. Just a per-cell toggle that makes some cells invisible to everyone besides the author? Something more sophisticated?
- I have admired how R Markdown has made the code less conspicuous
  - One option would be to make that less conspicious, or to allow a setting that would hide the output. 
  - Another option I can think of would be an alternative URL like /html/ or /read-only/ or whatever at the end of a published page’s URI that, like Google Sheets, would offer a stripped down version of the page without any of the editing features.
- I’ve been referring to these as “inspector cells”. 
  - An inspector cell is any cell that doesn’t return DOM. 
  - When a cell returns some non-DOM value such as a number, string, object or function, this is displayed by Observable’s built-in inspector (much like a browser’s developer tools).
  - There’s no way to hide a cell entirely, and that’s mostly deliberate: we want the code to be accessible to readers so they can read it, learn from it, and even tinker with it. We are view-source at heart.
  - What I do for these cells is put them at the end under an Appendix h2 header.
  - A more extreme approach would be to hide the inspector entirely via CSS:
  - html`<style>. O--inspect { visibility: hidden; }</style>`.
  - But, note that the cell names would still be visible in the left margin, so that might be a little weird.
  - Another approach is to use `viewof` to override the default inspector and instead show arbitrary DOM.
  - Perhaps the cleanest approach is to use `import`s. 
    - If you break your notebook into two notebooks—one explanatory, mostly Markdown and narrative; the other implementing the chart (possibly exploratory)—
    - then you can import the chart into your explanatory notebook without needing to also show those implementation cells. 
    - The import statement would be visible, however, so you can’t hide the code entirely!
- In the future, we might formalize the concept of an “appendix” (or perhaps an “implementation section”), and allow that section to be collapsed by default. 
  - Or we might go so far as to make notebooks hierarchical, and allow you to embed notebooks within notebooks…
