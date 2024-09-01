---
title: lib-notb-jupyter-community-alternatives-products
tags: [alternatives, jupyter, pm]
created: 2024-06-30T03:32:21.694Z
modified: 2024-06-30T03:32:45.893Z
---

# lib-notb-jupyter-community-alternatives-products

# guide

# pm-jupyter
- [Deepnote: Analytics and data science notebook for teams.](https://deepnote.com/)

- [DataLab](https://www.datacamp.com/datalab)
  - an AI-enabled data notebook to allow anyone to go from data to insight regardless of technical skill. 
# discuss-stars
- ## 

- ## 

- ## 

- ## [What is the difference between Jupyter Notebook and JupyterLab? - Stack Overflow](https://stackoverflow.com/questions/50982686/what-is-the-difference-between-jupyter-notebook-and-jupyterlab)
- At this time (mid 2019), with JupyterLab 1.0 release, as a user, I think we should adopt JupyterLab for daily use
  - JupyterLab will eventually replace the classic Jupyter Notebook
  - in the old days, there is just one Jupyter Notebook, and now with JupyterLab (and in the future), Notebook is just one of the core applications in JupyterLab (along with others like code Console, command-line Terminal, and a Text Editor).

- Update regarding Jupyter Notebook (Aug 2023)
  - Several posts have mentioned that JupyterLab will eventually replace Jupyter Notebook (for good reason, Project Jupyter told us so). 
  - However, this is no longer quite the case. 
  - Jupyter Notebook v7 is the next fully supported version of Jupyter Notebook. It is based on RetroLab (formerly JupyterLab classic), which means it shares the same internals as Jupyter Lab, but aims to preserve the classic Jupyter Notebook experience.
  - Notebook v7 will continue to provide the document-centric experience preferred by many users, where each individual notebook opens in a separate browser tab and the visible tools and menus are focused on the open document. 
- Highlighted features in Notebook v7: 
  - debugger, real time collaboration, table of contents rendering, theming and dark mode, internationalization, accessibility improvements, support for many JupyterLab extensions, and compact view on mobile devices

- ## vote: if you do exploratory data analysis or build machine learning models, what tool do you reach for first?
  - local, Jupyter notebook
  - local, data science ide(spyder, rstudio, jupyterlab, matlab)
  - hosted, colab
  - pycharm, vscode
- JupyterLab has made some really nice improvements lately – would definitely feel comfortable calling it an IDE, and certainly feel that it is differentiated compared to Jupyter notebooks.
- I think Jupyter Lab is in the same category as RStudio etc, though i don't think I'd call it an IDE, maybe an IDSE (integrated data science environment). I think it's worth emphasizing the order of priorities to be DS first, developing second
- why do so many people still use notebooks and not Jupyter Lab?
  - [Benefits of the classic UI and use cases for classic over JupyterLab](https://discourse.jupyter.org/t/benefits-of-the-classic-ui-and-use-cases-for-classic-over-jupyterlab-was-why-is-tim-not-moving-to-lab/2419)
  - The goal of the jupyterlab-classic project is to look as close to the classic notebook UI as possible, while leveraging the efforts put in the development of JupyterLab itself and its extension system

# discuss
- ## 

- ## 

- ## 

- ## 

- ## 有没有除了 colab 之外也可以在线运行 jupyper notebook 的服务，发现了 jetbrains 家的 datalore 
- https://x.com/lewangdev/status/1642551706486489088
  - 相较于 colab 和 jupyter，别人家是 notebook，他家的是 IDE，连代码自动补全，重构等常用功能都有，个人和4人以下小团队可以免费使用，而且不用翻墙
- 120小时，每次运行小脚本是不是只算几秒钟？
  - 对，运行有时间统计的，这个 notebook 全部执行完，估计只用几十秒的时间

- datalore 免费版没有 GPU，但是跑下 Python 脚本还是挺好的

- ## I think notebook-like UIs are the best medium for generative AI rn. 
- https://x.com/sh_reya/status/1801626846364058110
  - Notebooks are rich in context & context-aware by design, familiar, and inherently exploratory
- One very cool piece of AI-UI that departs a bit from the notebook paradigm is Infinite Tech: https://infinite.tech
  - Kind of like a mutable notebook grid, where you can connect different cells/panels to different agents/datasets and setup an agent system geometrically.
- Built an open-source Jupyter Notebook that brings the power of @OpenAI's code interpreter into your local Python development environment.

- ## 👣 jupyter notebook/livebook but focused entirely on SQL - who is gonna build this
- https://x.com/thdxr/status/1798422000320602496
- Databricks does this. Downside is that you have to setup databricks. But if you’re anyways using it -> no extra friction

- jupyter notebook is language agnostic but you would need a kernel for SQL
- Jupyter already works pretty well w/ jupysql

- What’s your exact use case? I have a Jupyter template set-up to ingest from S3 or local paths, and use DuckDB to write sql for querying. I could likely customize it to fit your use case more specifically(data source, query interface, etc).

- I used to type SQL in jupyter cells. a package called jupysql may be exactly what you're looking for

- I think @YousefED is pretty close already with http://typecell.org, though it does a lot more than sql I guess

- isn't this just metabase? or tableau

- try deepnote

- JetBrains DataSpell?

- Feel like DBeaver is pretty close to this already. I use it to run, test, and store SQL queries.

- ## 📖 [Show HN: Srcbook – A TypeScript notebook for rapid prototyping | Hacker News _202408](https://news.ycombinator.com/item?id=41291700)
  - We built this because we needed a Jupyter-like environment for TypeScript

- how do you run the code? is it securely sandboxed?
  - The code runs locally on your machine. 
  - Right now the architecture is that each Srcbook has 2 representations:
  - a markdown encoding that we use when you export. Easier to share, serialize, etc...
  - on disk, Srcbooks are actually directories under ~/.srcbook/srcbooks. The files and code is all there, and runs with your local node executable. You therefore need to be careful to not run any arbitrary srcbook you download, but there is no code ever leaving your machine

- Observable is a great notebook env for dataviz, but the bespoke js + observability patterns can feel obtuse for non-dataviz stuff.
  - Likewise, the Jupyter js kernels feel second-class and require python dependencies.
- How does it compare with Observable?
  - Observable is highly specialized in data visualizations (graphs, plots, etc...) and runs in the browser.
  - Srcbook is built for different use cases: we focus on a backend runtime (node) and want to solve for non-data-visualizations workflows. Use cases like prototyping with a third party npm library, running a script to test your app's behavior, or building an AI agent.
  - Compared to Observable, it's apache-2 licensed and it's self-hostable. The d3, p5 and database access you have to add yourself. With Observable user, workspace, diagramming and template management is built-in.

- I think this is more like Google Colab, where the UI renders in the browser, but offloads computation to a kernel running elsewhere.
  - As I recall, Observable uses the browser's JS runtime for computation.

- Love that this is local. I've messed around trying to get Node on Jupyter with custom kernels, but never got close to a working setup with TypeScript.
  - Two features would be huge:
  1. Web cells for intermixing UI components alongside NodeJS cells. Would be cool if there was a bridge API to call code in the Node cells as well.
  2. VSCode extension to render this all in there directly.

- This is a cool idea! I often end up just using replit to play with a library, something more like Livebook makes a lot of sense. I like that you're using markdown too, makes these files much more useful than Jupyter ones.
  - The Markdown is a really neat idea borrowed from Livebook. It allows for really good diffing if you want to version control them, and makes reviewing diffs easier. As a bonus a lot of things can read markdown and render it nicely for you.

- I wish there was also a "browser" cell, so that the execution wouldn’t be happening in the node.

- how do you plan to monetize this?
  - The plan is to have a cloud offering which runs Srcbooks as infrastructure. There are a couple of directions are considering, but essentially they boil down to helping you build an app quickly and iteratively, then serve it in production.

- why this is advantageous over just dumping a bunch of HTML files into a folder
  - Presumably this runs in node, rather than the browser, which might have implications for your dependencies (I know esm.sh shims node core dependencies and does fancy transpilation stuff, but why deal with that if you can just run direct on node).
