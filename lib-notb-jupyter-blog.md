---
title: lib-notb-jupyter-blog
tags: [blog, jupyter, notebook]
created: 2024-06-30T03:58:41.260Z
modified: 2024-06-30T03:59:03.615Z
---

# lib-notb-jupyter-blog

# guide

# blogs

## 🆚 [JupyterLab vs Notebook: A Comprehensive Comparison – Kanaries _202308](https://docs.kanaries.net/topics/Python/jupyterlab-vs-notebook)

- Jupyter Notebook has a simpler, more lightweight interface. It is primarily a single-document interface
- JupyterLab, however, offers a more versatile and feature-rich interface. It is a multi-document, multi-tasking interface that allows users to work with several notebooks or files simultaneously, view their data in a variety of ways, and even integrate their work with third-party extensions. 
- In addition to all the features offered by Jupyter Notebook, JupyterLab allows you to open multiple notebooks or files side-by-side in the work area, organize your workspace with drag-and-drop functionality, and use tools like a file browser, command palette, markdown preview, and more. It also supports real-time collaboration, making it a great tool for team projects.
- In addition to the notebook file format (.ipynb), JupyterLab also supports other file formats like markdown (.md), JavaScript (.js), JSON (.json), HTML (.html), CSS (.css), and more. This makes JupyterLab a more versatile tool for working with different types of files and projects.
# blogs-collab

## 📔 [How we made Jupyter Notebooks collaborative with Yjs _202106](https://blog.jupyter.org/how-we-made-jupyter-notebooks-collaborative-with-yjs-b8dff6a9d8af)

- the first collaborative Jupyter Notebook implementation, Colaboratory (or Colab), was created by Google engineers. They rewrote the UI for Jupyter Notebooks and gave it a collaborative notebook model via Google’s Realtime API, which was deprecated in 2017. 
- In 2013 William Stein launched CoCalc, a Jupyter notebook service with collaborative editing support right from the beginning. Like Colaboratory, CoCalc wrote a new UI for Jupyter Notebooks, while reusing other parts of the Jupyter architecture. They made different choices and implemented a custom solution for conflict resolution
- In 2017, Chris Colbert started the ambitious endeavor to build high-performance CRDT data structures that can be used as an observable data model.
- In 2019, Vidar Tonaas Fauske, Ian Rose, and Saul Shanabrook started work to integrate the Lumino CRDT into JupyterLab. Their work lived for a time in JupyterLab#6871 and has later been moved to a separate repository JupyterLab/rtc.
- While the Lumino CRDT is pretty awesome, in 2020 Brian Granger created a Lumino CRDT performance benchmark that revealed critical performance and algorithm issues (such as the so-called interleaving anomoly). In the process, Brian discovered my CRDT implementation Yjs and the two of us began to discuss CRDT implementations and Yjs in particular.
- After many discussions with Eric, we finally came up with a compromise that I’m now really excited about. Yjs and ModelDB only provide raw data structures to build collaborative applications. Our plan was to build a notebook model with an easy-to-use API to manipulate, observe, and synchronize changes on the notebook.
# blogs-vendors

## [Overview of JupyterHub Ecosystem _202307](https://engineeringblog.yelp.com/2023/07/overview-of-jupyterhub-ecosystem.html)

- At Yelp, Apache Spark and JupyterHub are heavily used for batch processing and interactive use-cases, such as in building feature models, conducting ad-hoc data analysis, sharing templates, making on-boarding materials, creating visualizations, and producing sales reports.
- Our initial deployments of Jupyter at Yelp were iPython notebooks managed at an individual level. Later on when Jupyterlab was released (2018), our notebook ecosystem was extended to Jupyter Servers running on dev boxes
- In this blog post, we will discuss the evolution of our Jupyterhub ecosystem which is now managed by a single team and presents an easy to use, scalable, robust, and monitored system for all engineers at Yelp.

- The Yelp JupyterHub ecosystem encompasses JupyterHub, our internal notebook archiving service Folium, Papermill, Spark on PaaSTA, and a Spark Job Scheduling Service (e.g. Mesos or Kubernetes).

- Over the years, we have scaled our usage of the JupyterHub ecosystem to several teams owning thousands of batches. 
  - As of today, over 100 service owners own more than 1200 batches and hundreds of Jupyter and Folium notebooks are executed daily.

- At Yelp, our team is committed to continuous evolution of the JupyterHub ecosystem
# more
