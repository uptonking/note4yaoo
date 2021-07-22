---
title: lib-notebook-observablehq-latest-changelog
tags: [changelog, observablehq]
created: '2021-05-14T14:52:22.020Z'
modified: '2021-05-14T14:52:48.486Z'
---

# lib-notebook-observablehq-latest-changelog

# guide

# blogging

## Introducing Observable for Enterprise_202107

- Observable now offers a new Enterprise Tier with additional support, security, and access control priced at $40/month/editor.
- Features include:
  - Access control by authentication domain
  - Control notebook publishing permissions
  - Customer Success Manager
  - Onboarding help and annual training
  - Early access to new product features
  - 4 hour response times for email support response

## [SQLite_20210527](https://observablehq.com/@observablehq/sqlite)

- Observable has built-in support for SQLite
  - Observable’s SQLite client uses sql.js
  - https://github.com/sql-js/sql.js

## [Introducing Observable Templates!_20210525](https://observablehq.com/@observablehq/introducing-observable-templates)

- Templates provide pre-packaged artifacts for common data-related workflows.
  - Building an accurate user retention dashboard can take days, if not weeks. 
  - With our User Retention Template, all you need to do is upload your data
- With Templates the data, visualizations, and text, all live together. 

## [Cell Modes_20210514](https://observablehq.com/@observablehq/cell-modes)

- Previously, writing an Observable notebook was optimized for JavaScript. 
  - there was a little extra work for non-JavaScript cells -- for example, you had to manage the opening and closing backticks for a Markdown cell.
- Now, you can choose the mode in which you want to edit a cell. 
  - The mode of a cell affects the way the cell is parsed and evaluated (treating the contents of the cell as if it were wrapped in the appropriate tagged template), as well as the editing options displayed in the editor.
- The mode defaults to JavaScript for newly created cells, but newly split cells will keep the mode of the original cell.

## [Introducing Observable Plot_20210504](https://observablehq.com/@observablehq/introducing-observable-plot)

- **Plot’s aim is speed and convenience**. 
  - Our hope is you’ll spend less time reading the docs, searching for snippets, and debugging — and more time asking questions of data.
  - With faster iteration, you can see more of your data and find more insights.
  - Plot not only has intuitive syntax but makes it incredibly easy to iterate through different chart types and faceting methods

## [Working with Observable Collaboration_20210311](https://observablehq.com/@observablehq/working-with-observable-collaboration)

- We call our improved (but still experimental) editor “Next”, and our current (stable) editor “Classic”. 
- The following features are only partially supported:
  - [ ] You can create, view, resolve and delete comments, but you cannot lock comments.
  - [ ] Files can be accessed by notebooks, and you can upload files using the Cmd+Shift+U keyboard shortcut. The files pane is only partially implemented.
  - [ ] Suggest and compare are not yet supported.
  - [ ] Visual dataflow is not yet supported.
  - [ ] You can view a notebook at a specific version by appending @version to the URL, but the history pane is not yet implemented.

- To go back to Classic temporarily without permanently disabling experimental features, click the `Switch to Classic` action
  - In theory, there shouldn’t be any issues with collaborators editing a notebook in Next and Classic simultaneously
  - You can disable automatic redirects to Next ui by adding `?ui=classic` to the URL.

## more features

- [Announcing cell shortcuts_201906](https://observablehq.com/@observablehq/cell-shortcuts)
  - We’ve added new bindings to our our keyboard shortcuts: something that mirrors vim’s ‘Normal Mode’, or Jupyter’s ‘Command Mode’.
- [Suggestions](https://observablehq.com/@observablehq/suggestions-and-comments)
  - You propose code changes to the author of the notebook.
  - 类似git的diff view
# changelog
- 2021-05-13
  - We're excited to announce Cell Modes!
  - You can choose the mode you want to edit - Javascript, Markdown, HTML and TeX.
  - when editing a cell in Markdown mode, you can simply write plain Markdown and get the output that you want. 
  - No more managing the opening and closing backticks of the Markdown tagged template literal, no more need to escape backticks!
