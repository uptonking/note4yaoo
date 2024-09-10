---
title: toc-lib-notebook-style-cell
tags: [cell, lib, notebook, toc]
created: 2021-05-13T16:07:05.876Z
modified: 2021-05-13T16:08:15.067Z
---

# toc-lib-notebook-style-cell

# guide

# js-notebook
- starboard-notebook /633Star/MPLv2/202005/ts
  - https://github.com/gzuidhof/starboard-notebook
  - https://starboard.gg/
  - In-browser literal notebook runtime used in Starboard.

- Data-Forge Notebook /MIT/202401/ts
  - https://github.com/data-forge-notebook/data-forge-notebook
  - https://www.data-forge-notebook.com/
  - https://data-forge-notebook.github.io/visualization-examples/
  - a cross-platform notebook application for JavaScript and TypeScript
  - 作者 Ashley Davis，专注于数据处理与可视化
  - [Release history](https://github.com/data-forge-notebook/data-forge-notebook/wiki/Release-history)
    - v2.0.0_202401
      - now fully open source
      - Markdown cells
      - Multi-window application
      - Plugin-based visualization systems: HTML/text, ApexCharts, Leaflet
      - Notebooks are now stored in markdown files for easy of reading (without DFN) and merging code changes.

- https://github.com/githubnext/vitale /202406/ts
  - vitale is a VS Code notebook implementation for Node.js + TypeScript.
  - automatic re-execution of dependent cells
  - rendering React components
  - It uses vite for compilation and hot-reloading

- https://github.com/ottomatica/docable-notebooks
  - https://docable.cloud/ottomatica/docable-examples/script.md
  - /286Star/Apache2/202105/js
  - 依赖 turndown、express、jsdom
  - provide a literate programming environments which works great for writing and publishing interactive tutorials
  - features
    - Script cells
    - Embedded Terminals
    - File cells
    - Multi-target: local, docker, ssh
    - Embed your slides, YouTube video, and more
  - Authoring a Docable notebook is as easy as writing a Markdown file.
  - Docable's interactive cells are simply Markdown code block (```) with addition of a few json annotations
  - These code blocks are 100% compatible with GitHub's Markdown rendering and the JSON is simply ignored

- https://github.com/eventhorizn/react-ts-js-notebook
  - Building a javascript notebook (think Jupyter notebook) with React and TypeScript
  - 计划详细，实现粗糙
- https://github.com/enixam/js-notebook
  - https://javascript-notebook.netlify.app/
  - 和上面的ui相同，功能可用

- https://github.com/inkandswitch/potluck /202211/ts/inactive
  - https://potluck-sheets.vercel.app/
  - Potluck: Dynamic Documents as Personal Software

- https://github.com/jtpio/p5-notebook
  - https://p5-notebook.vercel.app/
  - A minimal Jupyter notebook UI for p5.js kernels.
  - This notebook interface is built using components from the JupyterLab computational environment.

- https://github.com/jaked/programmable-matter /202112/ts
  - A dynamic data-driven document development environment (DDDDDE)
  - Did you ever wish your document editor were more like an IDE? Your IDE more like a spreadsheet? Your spreadsheet more like a database? No?
  - Programmable Matter is a "document development environment": a rich text document editor that supports embedded code. You can use code to assemble documents from components, generate documents from structured data, and even build simple UIs.
  - Like an IDE, it provides live feedback about your code (syntax highlighting, error reporting, code suggestions) and navigation of the document and code structure.
  - Like a spreadsheet, it provides live update of results as you make changes to documents, data, and code; and in the presence of code errors, the correct parts still run.
  - Like a database, it provides means of defining structured data tables and working with them through a uniform interface.

- [interactive notebooks](https://nteract.io/)
  - We build SDKs, applications, and libraries that help you and your team make the most of interactive (particularly Jupyter) notebooks and REPLs.
  - nteract provides a client-side SDK for integrating notebook and REPL UIs into your software. 

- https://github.com/srcbookdev/srcbook /apache2/202408/ts
  - Srcbook (”source-book”) is an open-source TypeScript notebook that runs locally, powered by Node.js. 
    - It shines for rapid prototyping, code exploration, and collaborating on ideas. 
    - It’s inspired by Python’s Jupyter and Elixir’s Livebook.
  - Create, run, and share reproducible programs and ideas
  - Export to valid markdown format (.src.md)
  - Local execution with a web interface
# python-notebook
- https://github.com/jupyter/notebook
  - a web-based notebook environment for interactive computing.
  - The IPython Notebook is now known as the Jupyter Notebook.
  - [The Jupyter Notebook Introduction](https://jupyter-notebook.readthedocs.io/en/latest/notebook.html)

- https://github.com/ales-tsurko/cells
  - Live coding environment. 
  - Use SuperCollider, Python, TidalCycles, Node.js etc. in the same project.

- https://github.com/inkandswitch/livebook /201704/python
  - IPython notebook-compatible live coding experiment
# reactive-doc
- https://github.com/worrydream/Tangle /201111/js/inactive
  - https://worrydream.com/Tangle/
  - Tangle is a JavaScript library for creating reactive documents. Your readers can interactively explore possibilities, play with parameters, and see the document update immediately. Tangle is super-simple and easy to learn.
- https://github.com/rexgarland/Entangle /MIT/202302/js/inactive
  - Another attempt at writing Tangle.js documents in markdown.
# ref
- https://github.com/jsvine/notebookjs
  - Notebook.js parses raw Jupyter/IPython notebooks, and lets you render them as HTML
