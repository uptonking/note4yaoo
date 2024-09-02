---
title: lib-notb-jupyter-examples
tags: [examples, jupyter]
created: 2023-04-15T08:18:59.952Z
modified: 2024-06-30T03:20:21.444Z
---

# lib-notb-jupyter-examples

# guide

# popular
- https://github.com/markusschanta/awesome-jupyter
  - A curated list of awesome Jupyter projects, libraries and resources

- https://github.com/jupyterhub/jupyterhub /BSD(Revised)/202406/python
  - https://jupyterhub.readthedocs.io/
  - Multi-user server for Jupyter notebooks
  - Project Jupyter created JupyterHub to support many users
  - multi-user Hub (tornado process)
  - Hub handles login and spawns single-user servers on demand
  - With JupyterHub you can create a multi-user Hub that spawns, manages, and proxies multiple instances of the single-user Jupyter notebook server.
  - https://github.com/jupyterhub/binderhub /BSD/202406/python
    - https://binderhub.readthedocs.io/
    - https://mybinder.org/
    - Turn a Git repo into a collection of interactive notebooks
    - BinderHub is built with Python, kubernetes, tornado, npm, webpack, and sphinx.
    - A JupyterHub server will host your repository's contents. We offer you a reusable link and badge to your live repository that you can easily share with others.

- https://github.com/jupyter-server/jupyverse /BSD/202406/python
  - https://jupyter-server.github.io/jupyverse
  - A Jupyter server based on FastAPI
  - A set of Asphalt components implementing a Jupyter server.
  - 202207: Jupyverse and FPS generally embrace modern Python technologies such as ASGI, and an ecosystem built around uvicorn/Starlette/FastAPI, which we see as the future of web development. In the near future, Jupyverse may take a different path than JupyterHub for a multi-user scenario.
    - JupyterHub is basically a server of servers. Each individually spawned Jupyter server is quite independent. We might scale Jupyverse differently, so that it remains the only server.
  - [Jupyverse may take a different path than JupyterHub for a multi-user scenario? _202208](https://github.com/jupyter-server/jupyverse/issues/201)
    - I mean that we will probably not scale Jupyverse by launching a server for each user, but by using other techniques such as replication.
    - I have had some practice in this area, similar to Deepnote, where splitting the kernel, file system, and RTC into individual services.
    - In this respect, jupyverse and FPS would bring a better architecture in a cloud environment (a true WEB IDE architecture), where users would be able to edit code directly without starting any compute resources 

- https://github.com/jupyter/jupyterlab
  - JupyterLab: The next generation user interface for Project Jupyter
  - notebook、editor、console、terminal
- https://github.com/jupyterlab/jupyterlab-desktop /BSD/202405/ts
  - JupyterLab desktop application, based on Electron
  - winget install jupyterlab
  - JupyterLab Desktop sets File Browser's root directory based on the launch method.
  - Sessions represent local project launches and connections to existing JupyterLab servers. Each JupyterLab UI window in the app is associated with a separate session and sessions can be restored with the same configuration later on.
  - JupyterLab Desktop currently supports user-friendly prebuilt extensions. Source extensions which require rebuilding are not supported.

- https://github.com/jupyterlite/jupyterlite /BSD/202406/python/ts
  - https://jupyterlite.rtfd.io/en/stable/try/lab
  - Wasm powered Jupyter running in the browser
  - JupyterLite is a JupyterLab distribution that runs entirely in the browser built from the ground-up using JupyterLab components and extensions
  - Although JupyterLite is currently being developed by core Jupyter developers, the project is still unofficial.
  - JupyterLite works with both JupyterLab and Jupyter Notebook.
  - Python kernel backed by Pyodide running in a Web Worker
  - JavaScript kernel running in a Web Worker
  - View hosted example Notebooks and other files, then edit, save, and download from the browser's IndexDB (or localStorage)

- https://github.com/pretzelai/pretzelai /AGPL/202408/ts/python
  - https://withpretzel.com/
  - Modern, open-source Jupyter alternative
  - 🍴 Pretzel is a fork of Jupyter with the goal to improve Jupyter's capabilities. We've added AI code generation and editing, inline tab completion, sidebar chat and error fixing to Jupyter for now with a lot more to come.
  - 依赖codemirror
  - To use your own model (OpenAI, Anthropic/Claude, Ollama or Groq), see the Configuration section
  - Inline Tab Completion
    - Wait for 1 second to trigger completions. 
    - The default Pretzel AI Server uses Mistral's Codestral but you can switch the inline completion model in Settings
  - We DO NOT store any code or data you send to the Pretzel AI Server.

- https://github.com/executablebooks/jupyter-book /BSD/202406/python
  - http://jupyterbook.org/
  - Create beautiful, publication-quality books and documents from computational content
  - write their content in markdown files or Jupyter notebooks
  - include computational elements (e.g., code cells) in either type, 
  - using a simple command, run the embedded code cells, cache the outputs and convert this content into: a web-based interactive book and a publication-quality PDF.

- https://github.com/mwouts/jupytext /MIT/202405/python
  - https://jupytext.readthedocs.io/
  - Jupyter Notebooks as Markdown Documents, Julia, Python or R scripts
  - Only the notebook inputs (and optionally, the metadata) are included. Text notebooks are well suited for version control. 
  - If your notebook is documentation-oriented, a Markdown-based format (text notebooks with a .md extension) might be more appropriate

- https://github.com/voila-dashboards/voila /202406/python
  - https://voila.readthedocs.io/
  - turns Jupyter notebooks into standalone web applications

- https://github.com/jupyter-widgets-contrib/ipysheet /MIT/202401/python/ts
  - Jupyter handsontable integration
  - Due to Handsontable licensing changes ipysheet is stuck witch the outdated Handsontable version 6.2.2 (open-source). We recommend not using ipysheet anymore. 
  - We suggest an alternative like ipydatagrid.
  - https://github.com/bloomberg/ipydatagrid

- https://github.com/paddymul/buckaroo /BSD/202402/python
  - https://buckaroo-data.readthedocs.io/en/latest/
  - Buckaroo is a modern data table for Jupyter that expedites the most common exploratory data analysis tasks
  - Buckaroo starts with a modern performant data table that displays up to 10k rows, is sortable, has value formatting, and scrolls.
  - Quickly explore dataframes, and run pandas commands via a GUI. 
  - Works inside the jupyter notebook.
  - When you run `import buckaroo` in a Jupyter notebook, Buckaroo becomes the default display method for Pandas and Polars DataFrames
# notebooks-like
- https://github.com/pennant-notebook
  - https://pennant-notebook.github.io/
  - A realtime collaborative computational notebook
  - https://github.com/pennant-notebook/pennant-engine /202402/python/js
    - the remote code execution engine for the pennant-notebook project.
  - https://github.com/pennant-notebook/server /202311/ts
    - https://github.com/marwan37/pennant-flask-server
    - the server-side code for the client app, serving the client React application and handling all API routes to DynamoDB.
    - the Node/Express webserver and DynamoDB API routes/controllers for the pennant-notebook project.
  - https://github.com/pennant-notebook/client /MIT/202403/ts
    - the React application for the pennant-notebook project.
    - Open-Source Computational Notebook Supporting Real-Time Collaboration and Flexible Code Execution in Markdown, JavaScript, and Python
    - Real-Time Collaboration: Powered by Yjs
    - CodeMirror 6 provides a rich coding environment, integrated with Yjs for collaborative editing.
    - Markdown Support: Enhanced markdown editing experience with `BlockNote`.
    - Offline Persistence: Efficient caching and offline capabilities with `y-indexeddb`.
    - Drag-and-Drop Functionality: Powered by `react-dnd`.
    - Shared Execution Context: Facilitates collaborative coding where outputs are updated in real-time, and visible to all connected users.
    - Notebook-Style Code Execution: Independently run cells or the full notebook, tailored for exploratory coding and enhanced learning.

- https://github.com/nteract/nteract /BSD/202312/ts
  - We build SDKs, applications, and libraries that help you and your team make the most of interactive (particularly Jupyter) notebooks and REPLs.
  - This extension can be installed alongside Jupyter classic and JupyterLab in your Jupyter deployments or personal Jupyter server.

- https://github.com/sagemathinc/cocalc /1.1kStar/AGPLv3+NonCommercial/202311/ts/python
  - https://cocalc.com/
  - CoCalc is web-based software that enables collaboration in research, teaching, and scientific publishing.
  - It includes Jupyter Notebooks, Sage Worksheets, a LaTeX Editor and a Linux Terminal to help people work together in real time
  - 前端依赖antd5、dnd-kit、slate-core.v.90、d3、react-redux
  - 后端依赖express-session、passport
  - 基于slate-core实现了virtualized-render
  - It is also possible to run CoCalc on your own infrastructure.

- https://github.com/srcbookdev/srcbook /apache2/202408/ts
  - interactive notebooks for JavaScript & TypeScript. They allow you to create, run and share reproduceable programs and ideas.
  - runs locally on your machine and is fully open-source
  - 依赖codemirror
  - Srcbook creates folders on your local machine and provides a web interface (also running locally) as a programming environment.
  - Srcbooks export to markdown using the `.src.md` extension
# jupyter-gis
- https://github.com/GispoCoding/geoviz-notebooks /MIT/202406/jupyter
  - Python tool for analyzing geospatial data in cities.
  - https://github.com/GispoCoding/ipygis /MIT
    - GIS utils and GIS visualization/analysis functions for Jupyter Notebook.
    - ipygis is the engine behind geoviz-notebooks

- https://github.com/OpenGeoscience/geonotebook /apache2/201901/python
  - A Jupyter notebook extension for geospatial visualization and analysis
  - GeoNotebook is an application that provides client/server environment with interactive visualization and analysis capabilities using Jupyter, GeoJS and other open source tools. Jointly developed by Kitware and NASA Ames.

- https://github.com/opengeos/leafmap /MIT/202406/python
  - https://leafmap.org/
  - A Python package for interactive mapping and geospatial analysis with minimal coding in a Jupyter environment
  - It is a spin-off( 副产品；派生物) project of the geemap Python package, which was designed specifically to work with Google Earth Engine (GEE).
  - Leafmap is designed to fill this gap for non-GEE users
  - Leafmap is built upon several open-source packages, such as `folium` and `ipyleaflet` (for creating interactive maps),  `WhiteboxTools` and whiteboxgui (for analyzing geospatial data), and `ipywidgets` (for designing interactive graphical user interface [GUI]).
  - Leafmap addresses these challenges by leveraging the bidirectional communication provided by ipyleaflet, enabling users to load and visualize geospatial datasets with just one line of code
# jupyter-web
- https://github.com/ElixirNote/elixirnote
  - a next-generation web-based user interface for Project Jupyter.

- https://github.com/jsvine/notebookjs /MIT/js
  - Render Jupyter/IPython notebooks on the fly, in the browser. 
  - Notebook.js parses raw Jupyter/IPython notebooks, and lets you render them as HTML.
  - https://github.com/jsvine/nbpreview /js
    - Render Jupyter/IPython notebooks without running a notebook server.
# jupyter-extensions
- https://github.com/yunabe/tslab
  - tslab is an interactive programming environment and REPL with Jupyter for JavaScript and TypeScript users. 
  - You can write and execute JavaScript and TypeScript interactively on browsers and save results as Jupyter notebooks.

- https://github.com/twosigma/beakerx /apache2/202101/inactive
  - http://beakerx.com/
  - BeakerX is a collection of JVM kernels and interactive widgets for plotting, tables, autotranslation, and other extensions to Jupyter Notebook and JupyterLab version 1.2.x and 2.x.
  - Version 2.x of BeakerX improves on the original solution architecture by providing independent modules that end-users can install to better tune the platform.
  - The kernel is originally derived from lappsgrid, but has been rewritten in Java and refactored and expanded.
  - https://github.com/twosigma/beakerx_base
    - BeakerX base classes and utilities

- https://github.com/bloomberg/ipydatagrid /BSD/202401/ts/python
  - Fast Datagrid widget for the Jupyter Notebook and JupyterLab
  - 依赖@lumino/datagrid、d3-scale、vega-format/expression
  - [I see some cons using Web Workers like it is done in ipysheet](https://github.com/bloomberg/ipydatagrid/issues/3)

- https://github.com/jku-vds-lab/loops /BSD/202408/python/ts
  - https://jku-vds-lab.at/publications/2024_loops/
  - extension to support iterative and exploratory data analysis in computational notebooks.
  - Loops automatically tracks the notebook's history and visualizes it next to the notebook.
  - Loops visualizes differences in code, markdown, tables, visualizations, and images

- https://github.com/jupyterlab/jupyterlab-git /BSD/202407/python/ts
  - A JupyterLab extension for version control using Git
# publish
- https://github.com/quarto-dev/quarto-cli /MIT/202407/ts
  - https://quarto.org/
  - Open-source scientific and technical publishing system built on Pandoc
  - Author using Jupyter notebooks or with plain text markdown in your favorite editor.
  - Create dynamic content with Python, R, Julia, and Observable.
  - https://github.com/quarto-dev/quarto
    - Quarto documents are authored using markdown
# examples
- https://github.com/sspaeti-com/practical-data-engineering
  - This is a practical example of a data engineering project with real-estates.
  - [Building a Data Engineering Project in 20 Minutes](https://www.ssp.sh/blog/data-engineering-project-in-twenty-minutes/)

- https://github.com/jupyter/nbgrader /BSD/202406/python
  - https://nbgrader.readthedocs.io/
  - A system for assigning and grading notebooks
  - Instructor toolbar extension for Jupyter notebooks
  - Instructor "formgrader" extension for Jupyter notebooks
# collab
- https://github.com/jupyterlab/jupyter-collaboration /BSD/202406/python
  - https://jupyterlab-realtime-collaboration.readthedocs.io/en/latest/
  - A Jupyter Server Extension Providing Support for Y Documents
  - JupyterLab Real-Time Collaboration is a Jupyter Server Extension and JupyterLab extensions providing support for Y documents and adding collaboration UI elements in JupyterLab.
- https://github.com/jupyter-server/pycrdt /MIT/202406/python/rust
  - https://davidbrochart.github.io/pycrdt
  - https://jupyter-server.github.io/pycrdt
  - CRDTs based on Yrs
  - https://github.com/jupyter-server/pycrdt-websocket /python
    - async WebSocket connector for pycrdt
# utils
- https://github.com/nteract/papermill /BSD/202404/python
  - https://papermill.readthedocs.io/en/latest/
  - Papermill is a tool for parameterizing and executing Jupyter Notebooks.
  - Papermill looks for the parameters cell and treats this cell as defaults for the parameters passed in at execution time. 
  - The two ways to execute the notebook with parameters are: (1) through the Python API and (2) through the command line interface.

- https://github.com/jupyterhub/batchspawner /BSD/202405/python
  - This is a custom spawner for Jupyterhub that is designed for installations on clusters using batch scheduling software.
  - This began as a generalization of mkgilbert's batchspawner which in turn was inspired by Andrea Zonca's blog post where he explains his implementation for a spawner that uses SSH and Torque. 
  - https://github.com/NERSC/sshspawner
    - Spawn JupyterHub single-user servers with ssh

- https://github.com/minrk/allthekernels /MIT/202208/python
  - A Jupyter kernel that multiplexes all the kernels you have installed.
# devops
- https://github.com/jupyterhub/zero-to-jupyterhub-k8s /BSD/202406/python
  - https://zero-to-jupyterhub.readthedocs.io/
  - Helm Chart & Documentation for deploying JupyterHub on Kubernetes
  - The JupyterHub Helm chart lets a user create a reproducible and maintainable deployment of JupyterHub on a Kubernetes cluster in a cloud environment
# more
