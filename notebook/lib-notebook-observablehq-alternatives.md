---
title: lib-notebook-observablehq-alternatives
tags: [alternatives, notebook, observablehq]
created: 2021-05-13T04:01:17.658Z
modified: 2021-05-14T14:46:37.026Z
---

# lib-notebook-observablehq-alternatives

# guide

- notebooks
  - [jupyter](https://jupyter.org/) helps to develop open-source software, open-standards, and services for interactive computing across dozens of programming languages.
  - [Dash](https://plotly.com/dash/) is the new standard for AI & data science apps.
# observable notebook alternatives

## GRID

- https://grid.is/
  - GRID is a web-based tool that empowers you to create stunning charts, reports, and interactive visualizations using your own #spreadsheet data 
  - GRID enables you to leverage your existing spreadsheet skills to build smart, interactive calculators, reports and scenario analyses.

## Data-Forge Notebook

- https://www.data-forge-notebook.com/#/
  - https://data-forge-notebook.github.io/visualization-examples/
  - 作者 Ashley Davis，专注于数据处理与可视化
- https://github.com/data-forge/data-forge-ts
  - http://www.data-forge-js.com/
  - /988Star/MIT/202102/ts
  - 依赖 json5、easy-table、dayjs、numeral、typy、papaparse
  - The JavaScript data transformation and analysis toolkit inspired by Pandas and LINQ.
- https://github.com/data-forge-notebook/plot
  - https://data-forge-notebook.github.io/plot/docs/plot
  - It is an abstraction layer over JavaScript visualization libraries. 
  - Currently supporting Apex Charts, but intending to support more in the future.
  - Plot can be used from Node.js, from the browser and is specially designed to integrate with Data-Forge Notebook.
- https://github.com/data-forge-notebook/datakit
  - https://data-forge-notebook.github.io/datakit/
  - Simple toolkit for reading and writing data CSV and JSON files
  - Consider using data-forge-ts for data transformation, analysis and visualization
- https://github.com/data-forge-notebook/editor-core
  - The core repository for Data-Forge Notebook's editor. Reused in the Electron and Online builds.

## jupyter-notebook-extensions

- JupyterLite
  - https://github.com/jupyterlite/jupyterlite
  - https://jupyterlite.rtfd.io/en/latest/try/lab
  - A full JupyterLab distribution running in the browser
  - Wasm powered Jupyter running in the browser
  - JupyterLite works out of the box with NumPy, SciPy and Matplotlib, you can also run them in your browser without any backend (helping reduce the load of Binder)

- Jupyter Book
  - https://github.com/executablebooks/jupyter-book
  - http://jupyterbook.org/
  - Build publication-quality books and documents from computational content.
  - write their content in markdown files or Jupyter notebooks
  - include computational elements (e.g., code cells) in either type
  - include rich syntax such as citations, cross-references, and numbered equations
  - using a simple command, run the embedded code cells, cache the outputs and convert this content into: a web-based interactive book and a publication-quality PDF.

- https://github.com/MarcSkovMadsen/panel-highcharts
  - panel-highcharts package makes it easy to use Highcharts from Python for exploratory analysis in a Jupyter Notebook or as a HoloViz Panel Web App.

- https://github.com/executablebooks/thebe
  - https://thebe.readthedocs.io/
  - /217Star/BSD/202104/js
  - turn static HTML pages into live documents
- https://github.com/ines/juniper
  - https://ines.github.io/juniper/
  - /194Star/MIT/201904/js
  - Edit and execute code snippets in the browser using Jupyter kernels
  - Juniper is a lightweight JavaScript library for adding interactive, editable and runnable code snippets to any website. 
  - It uses JupyterLab components and Binder, inspired by Min RK's Thebelab

- https://github.com/ElixirNote/elixirnote
  - https://elixirnote.github.io/elixir-web/
  - An extensible environment for interactive and reproducible computing, based on the Jupyter Notebook and Ecosystem.

- https://github.com/datalayer/jupyter-react
  - https://datalayer.tech/
  - React.js components to create a data product compatible with the Jupyter ecosystem .

## js-based-notebook

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
  - Docable's interactive cells are simply Markdown code block (```) with addition of a few json annotations
  - These code blocks are 100% compatible with GitHub's Markdown rendering and the JSON is simply ignored

- https://github.com/stencila/stencila
  - https://stenci.la/
  - a platform for authoring, collaborating on, and publishing executable documents.

## more-notebook

- https://github.com/airbnb/knowledge-repo
  - Knowledge Repo project is focused on facilitating the sharing of knowledge between data scientists and other technical roles using data formats and tools that make sense in these professions.
  - It provides various data stores (and utilities to manage them) for "knowledge posts", with a particular focus on notebooks (R Markdown and Jupyter/IPython Notebook) to better promote reproducible research.

- https://github.com/iodide-project/iodide
  - Iodide is no longer under development
  - Literate scientific computing and communication for the web
  - Note that the pyodide project (python-on-webassembly) continues and is unaffected by this change.
  - For another take on interactive, client-side notebooks, you may also be interested in the Starboard Notebook which provides some of the same capabilities as Iodide and is in active development.

- https://github.com/polynote/polynote
  - /ByNetflix
  - an experimental polyglot notebook environment. 
  - Currently, it supports Scala and Python (with or without Spark), SQL, and Vega.
  - Current notebook solutions, like Jupyter and Zeppelin, are lacking in some fundamental features:
    - Code editing
    - Text editing
    - Multi-language support
    - Runtime insight: shows what kernel is doing; variables tables; highlight exceptions

- https://github.com/idyll-lang/idyll
  - 完全基于js
  - Create explorable explanations and interactive essays.
  - Idyll is supported by the Interactive Data Lab at the University of Washington

- https://github.com/calculist/calculist-web
  - https://github.com/calculist/calculist
  - https://calculist.io/
  - the open source thinking tool for problem solvers
  - Write down your thoughts, ideas, and data in the form of lists.

- https://github.com/spark-notebook/spark-notebook
  - an interactive web-based editor that can combine Scala code, SQL queries, Markup and JavaScript in a collaborative manner to explore, analyse and learn from massive data sets.

- https://github.com/fonsp/Pluto.jl
  - Simple reactive notebooks for Julia

- https://github.com/Jermolene/TiddlyWiki5
  - https://tiddlywiki.com/
  - TiddlyWiki, a non-linear personal web notebook that anyone can use and keep forever, independently of any corporation.
  - TiddlyWiki is a complete interactive wiki in JavaScript. 
    - It can be used as a single HTML file in the browser or as a powerful Node.js application. 
    - It is highly customisable: the entire user interface is itself implemented in hackable WikiText.

- https://github.com/sutter-dave/apogeejs-admin
  - a javascript programming environment for iterative programming.
  - inspired by the spreadsheet and notebooks.

- [Idyll markup](https://idyll-lang.org/docs/syntax)
  - The main extensions are reactive variables, and components. 
  - Together these two elements can be used to create dynamic, interactive articles.

- https://github.com/quarto-dev/quarto-cli
  - Quarto is an open-source scientific and technical publishing system built on Pandoc. 
  - Quarto documents are authored using markdown
  - Support for embedding output from Python, R, and Julia via integration with Jupyter and Knitr .
# data-platform
- https://github.com/owid/owid-grapher
  - https://ourworldindata.org/owid-grapher
  - A platform for creating interactive data visualizations
  - This is the project we use at Our World in Data to create embeddable visualizations
