---
title: lib-notebook-jupyter-community
tags: [community, jupyter]
created: 2023-01-23T15:57:21.902Z
modified: 2023-01-23T15:57:32.786Z
---

# lib-notebook-jupyter-community

# guide

# discuss-stars
- ## 

- ## [proposals: Markdown based notebooks_202303](https://github.com/jupyter/enhancement-proposals/pull/103)

# discuss
- ## 

- ## 

- ## 

- ## 
# discuss-alternatives-notebook
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
# discuss-news
- ## 

- ## 

- ## 

- ## 

- ## We bring a modern #SQL experience to #Jupyter! 
- https://twitter.com/ploomber/status/1617522816441778177
- [JupySQL: Better SQL in Jupyter](https://ploomber.io/blog/jupysql/)
  - we forked ipython-sql and are actively developing it to bring a modern SQL experience to Jupyter!
