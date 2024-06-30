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
