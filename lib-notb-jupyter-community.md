---
title: lib-notb-jupyter-community
tags: [community, jupyter]
created: 2023-01-23T15:57:21.902Z
modified: 2024-06-30T03:20:13.304Z
---

# lib-notb-jupyter-community

# guide

# discuss-news
- ## 

- ## 

- ## 

- ## I just released Jupyter Shared Drive _20240824
- https://x.com/davidbrochart/status/1827087377086513330
  - This is a new way of collaborating in real-time in JupyterLab. Unlike Jupyter Collaboration, it is separate from your local files. See it as a scratch disk where you temporarily share files with colleagues.
  - pip install jupyter-shared-drive
  - The shared files don't live in a central place, but in each browser. This is a distributed architecture, think of it as a peer-to-peer application like BitTorrent. 
  - And since it's based on WebRTC, it will also work in JupyterLite! A signaling server is needed for connecting users.

- ## We bring a modern #SQL experience to #Jupyter! 
- https://twitter.com/ploomber/status/1617522816441778177
- [JupySQL: Better SQL in Jupyter](https://ploomber.io/blog/jupysql/)
  - we forked ipython-sql and are actively developing it to bring a modern SQL experience to Jupyter!

# discuss-roadmap/proposals
- ## 

- ## [proposals: Markdown based notebooks_202303](https://github.com/jupyter/enhancement-proposals/pull/103)

# discuss-version-history ⏳
- ## 

- ## 

- ## 

- ## 🤔 [Why Jupyter is data scientists’ computational notebook of choice | Hacker News _201810](https://news.ycombinator.com/item?id=18336202)
- Version control for Jupyter notebooks was one of the biggest complaint I had. Specifically, diff and merge with the JSON files (.ipynb) is ugly.
  - I built ReviewNb to solve one of those problems (diff). 
  - Note that, there is nbdime which works well for local diff/merge. 
  - The idea for ReviewNb is to have much tighter integration with GitHub etc.

- I have used jupytext (https://github.com/mwouts/jupytext) for this and it seems to work great - it outputs a separate .py file which is easily diff-able.

- The hard part is that introducing a tool like git (which requires you to choose moments to take a snapshot of the file, and then add some commit message) breaks the flow of interactive experimentation that notebooks are so good for.
  - And then we need to find a way to make those commits useful, because the time ordering of commits could be different from the time order in which cells were run! That is what is crucial to making computations reproducible — viewers should be able to replay the history of how a notebook result came to be.
  - I wonder whether there is a solution along the lines of auto-committing each cell before it’s executed and the results just after the cell is executed. Otherwise a user has to do too much manual organizing, which is a problem the notebook should ideally solve. When a user is happy with the experiments and the provenance of their results, they should be able to use an interactive rebase to create a cleaner version to share/archive.

- I'm not a Jupyter user, but I solve the reproducibility problem with Make.
  - As a project moves from exploration toward production, the entire thing is wrapped into a Makefile that can flow from raw data to publication in a single call to make.
- To have reproducible prototypes, I use Make to wrap the whole workflow in docker. 

- RStudio’s Markdown notebooks do not suffer from this and save a separate output file that can be gitignored.
- And they pay for this on other accounts:
  - No inline rendering of markdown.
  - Opening an . Rmd file is a lottery to see if rendered graphs and tables still exists.
  - Tables render completely differently in editor, HTML and pdf

- RMarkdown and Knitr are dramatic improvements in terms of final outputs and VC relative to notebooks.

- I think they fundamentally json is just the wrong format for these files. 
  - In json the code has to be escaped into strings, and json is really finicky about syntax (e.g. no trailing commas). So it doesn't work well.
- The closest I have seen anything come in this regard is Quokka however it's not quite all the way there.

- The closest thing I've seen to what you described would be... Emacs. It actually uses the "metadata in file-specific comments" paradigm. You can put file-local values for Emacs variables in comments at the top or bottom of your file

- You don't use Jupyter notebooks in production; they are super useful for pitching ideas to clients/bosses and doing some early prototyping. I feel sorry for anyone that has to work with "pure data scientists" that have no clue about software engineering practices...
- FWIW, Netflix uses Jupyter notebooks in production, using nteract UI

- "Production notebooks" should not be a thing... Unless prefaced by a bold RUN ALL.

- If you are interested in workbooks which are collaborative and versioned, take a look at http://datalore.io/
  - Version control is transparent and integrated and it's possible to work with workbooks collaboratively.

- Diffing JSON as text must be painful. Diffing JSON as data should be somewhat simple.
- Not merge, but jq can diff, and it can also do a consistent dump (jq -cS) for you.

- Powershell has Compare-Object, which will diff . NET objects. It has the convenient alias "diff". JSON can be converted to . NET objects by ConvertFrom-JSON. So you can import 2 JSON files and diff them in Powershell.
# discuss
- ## 

- ## 

- ## 

- ## 
