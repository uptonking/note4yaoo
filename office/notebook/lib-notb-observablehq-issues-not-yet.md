---
title: lib-notb-observablehq-issues-not-yet
tags: [issues, not-yet, observablehq]
created: 2021-05-22T19:54:41.082Z
modified: 2024-06-30T03:22:16.903Z
---

# lib-notb-observablehq-issues-not-yet

# issues-not-yet

- ## In defense of static imports
- https://talk.observablehq.com/t/in-defense-of-static-imports
- Since everything in Observable is inherently dynamic, there’s not really a need for static ES imports—though, we might add support in the future.
- I’d like to disagree with this.
  - If the library exposes itself through a `default` export, you’re forced to write
  - `delatin = (await import('https://unpkg.com/delatin')).default` ; 
  - With static imports of Observable cells, you can import multiple utility functions at once:
  - `import {slider, button} from '@jashkenas/inputs'` ; 
  - With dynamic imports, you’re forced to namespace them:
  - `inputs = import('https://unpkg.com/foobar')` ; 
  - Inconsistency. It would be easier for beginners if they didn’t have to remember that you can only use static imports for cells, and dynamic imports for external modules
- we are hoping to add support for cell destructuring in the near future.
  - Putting that aside, the problem currently is that we need some way to disambiguate between imports of notebooks and imports of ES modules.
  - if we want to go all-in on ES imports, we’re going to need browser support for import maps and possibly some Observable support for configuring import maps.
  - https://github.com/WICG/import-maps
  - https://caniuse.com/import-maps
  - The challenge with ES imports currently is that all (nested) imports must be relative or absolute paths, not bare identifiers. 
  - This makes it difficult to use cross-package imports, such as d3-scale importing d3-interpolate. 
  - `require` does not have this issue because the require function does the resolution, giving us a hook to control the behavior at runtime.

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

- ## Import/require works then doesn’t
- https://talk.observablehq.com/t/import-require-works-then-doesnt/4439
- The `require` function that is available in Observable is actually `d3-require`, which only supports AMD style modules.
  - The default CDN used by d3-require is jsdeliver.com
