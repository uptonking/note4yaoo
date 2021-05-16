---
title: lib-notebook-observablehq-alternatives
tags: [alternatives, notebook, observablehq]
created: '2021-05-13T04:01:17.658Z'
modified: '2021-05-14T14:46:37.026Z'
---

# lib-notebook-observablehq-alternatives

# guide

- notebooks
  - jupyter

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

## [Jupyter Notebook](https://jupyter.org/)

- provides a web-based application suitable for capturing the whole computation process: developing, documenting, and executing code, as well as communicating the results.
- The Jupyter notebook combines two components:
  - A web application: 
    - In-browser editing for code, with automatic syntax highlighting
    - In-browser editing for rich text using the Markdown markup language
    - The ability to execute code from the browser
    - Displaying the result of computation using rich media representations, such as HTML, LaTeX, PNG, SVG, etc
    - The ability to easily include mathematical notation within markdown cells using LaTeX, and rendered natively by MathJax.
  - Notebook documents: 
    - contains the inputs and outputs of a interactive session as well as additional text that accompanies the code but is not meant for execution.
    - These documents are internally JSON files and are saved with the .ipynb extension. 

### BeakerX

- BeakerX is a collection of kernels and extensions to the Jupyter interactive computing environment. 
- It provides JVM support, Spark cluster support, polyglot programming, interactive plots, tables, forms, publishing, and more. 

- ref
  - [The Jupyter Notebook Introduction](https://jupyter-notebook.readthedocs.io/en/latest/notebook.html)
  - http://beakerx.com/documentation

## more-notebook

- https://github.com/iodide-project/iodide
  - Literate scientific computing and communication for the web
  - Iodide is no longer under development
  - Note that the pyodide project (python-on-webassembly) continues and is unaffected by this change.
  - For another take on interactive, client-side notebooks, you may also be interested in the Starboard Notebook which provides some of the same capabilities as Iodide and is in active development.

- https://github.com/calculist/calculist-web
  - https://github.com/calculist/calculist
  - https://calculist.io/
  - the open source thinking tool for problem solvers
  - Write down your thoughts, ideas, and data in the form of lists.

- https://github.com/polynote/polynote
  - an experimental polyglot notebook environment. 
  - Currently, it supports Scala and Python (with or without Spark), SQL, and Vega.
  - Current notebook solutions, like Jupyter and Zeppelin, are lacking in some fundamental features: 
    - Code editing
    - Text editing
    - Multi-language support
    - Runtime insight: shows what kernel is doing; variables tables; highlight exceptions

- https://github.com/spark-notebook/spark-notebook
  - an interactive web-based editor that can combine Scala code, SQL queries, Markup and JavaScript in a collaborative manner to explore, analyse and learn from massive data sets.

- https://github.com/fonsp/Pluto.jl
  - Simple reactive notebooks for Julia

# observable-extensions

- https://github.com/asg017/unofficial-observablehq-compiler
  - An unofficial compiler for Observable notebooks (glue between the Observable parser and runtime)
  - This compiler will compile "observable syntax" into "javascript syntax". 
