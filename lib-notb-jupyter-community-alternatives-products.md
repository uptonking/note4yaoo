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

# discuss-marimo
- ## 

- ## 

- ## 

- ## [marimo: Representing Python notebooks as dataflow graphs | Hacker News _202508](https://news.ycombinator.com/item?id=44801392)
- One thing which I don't like about reactive notebooks is that you have to be much more mindful of expensive and long running calculations. 
  - There are feature to help, like adding a run button, but often I end up just disabling auto-run which does reduce the value of the reactive flow. 
  - For those use cases I don't find myself using marimo over Jupyter.
- for my own personal work, I find that there are many reasons to use marimo even when autorun is disabled — you still get guarantees on state, rich dataframe views, reusable functions, the Python file format, and more.
- Marimo is just a `.py` file.

- I don't like this reproducibility crisis story either. Notebooks are for exploration. It is okay if they are messy. 
  - If the tool I am using doesn't get in the way of my process but instead makes it fast enough then it is already doing its job. 
  - Once you are done it is up to you to let it die, make sure it is something you can go back and iterate on it, or package it and make it usable elsewhere.

- From the blog, you will see that reactive execution not only minimizes hidden state, it also enables rapid data exploration (far more rapid than a traditional notebook), reuse as data apps, reuse as scripts, a far more intelligent module autoreloader, and much more.
  - marimo is not just another Jupyter extension, it's a new kind of notebook. 

- > You have to be very disciplined to make a Jupyter notebook that is actually reproducible
  - This seems not necessarily very hard to me? All you have to do is keep yourself honest by actually trying to reproduce the results of the notebook when you're done

- Marimo seems really solid if you like tools like Streamlit or Observable
  - It certainly has some of the “widget feelings” from streamlit but the real killer feature is that you’re still always in a notebook. You can still explore with these widgets, which is a stellar experience.

- Even with data flow extension (also like ipyflow) I am still struggling with the execution model of notebooks in general. I often still see people defining functions and classes in notebooks to somehow handle prototyping loops.
  - I would love to see DAGs like in SSA form of compilers, that also supports loop operators. However, IMHO also the notebook interface needs to adjust for that (cell indentation ?). 
  - However, the strength of notebooks rather shows in document authoring like quarto, which IMHO mostly contradicts more complex controll flow.

- ## [marimo: Lessons learned reinventing the Python notebook | Hacker News _202403](https://news.ycombinator.com/item?id=40327543)
- I question the choice of Python as the format. Agreed that Json is terrible. But Python will have similar problems. And a notebook is a marked up document. Using a markup language is a natural choice. Delimit areas of particular syntax and you are off to the races. (Yes, I am fond of org mode.)
- We're adding support markdown with fenced code blocks, which maybe gets you closer to "delimiting areas of particular syntax"
  - Python is nice because it enables composition and reuse as vanilla scripts. But there are definitely tradeoffs.

- Yes, fenced blocks is what I meant. Recreating parts of xml and cdata seems the common end goal. I think we have enough modern processing that you can do looser grammars.
  - Composition is an odd goal to me. Most notebook usage is exploratory. As such, taking effort to reuse notebooks feels counter to the benefits of doing it again that you can get.

- How about lessons learned from other reactive notebook environments that have been around for a while? If you are 'reinventing' something, I wonder why no mentions are made of the paths that have been laid before (Observable, Quarto, Enso, etc.).
  - Pluto.jl is our biggest inspiration. We also took some inspiration from streamlit, and of course a lot of inspiration from the IPython kernel and Jupyter. We didn't look closely at Observable (though Fons cites Observable as his biggest inspiration), and didn't look at Quarto or Enso at all.

- as a daily jupyter user, i like this .py DAG approach a lot - more so for visualizing complex workflows than addressing a potentially corrupt hidden state.

- having spent a lot of time with airflow recently, it's designed for scheduling recurring jobs, not *batch processing.* meanwhile dagster is not meant for computationally intensive/ long-running jobs and the dataset-centric approach is offputting

- In principle every notebook is a DAG, since the cells are evaluated in a certain order. You could even infer the DAG from Jupyter notebooks, at least when the execution number is stored (the In[...] part).

- I am skeptical about the power of static analysis with a language like Python. Many times, the hidden state in Jupyter lives in another module, or somewhere deep in an object hierarchy. If you’re going to reinvent the Python notebook for reproducibility, I wonder why not go further, and fully snapshot the program state?

- the only ergonomic solution to me is to maintain a converted script of notebooks and using it for diff tracking, productionizing, etc. through a simple abstraction.
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
- 🆚️ How does it compare with Observable?
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
