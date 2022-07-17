---
title: lib-data-community
tags: [community, data-analysis, data-processing, lib]
created: 2021-05-13T14:36:20.064Z
modified: 2021-05-13T16:11:33.402Z
---

# lib-data-community

# guide

- [Arquero Cookbook](https://observablehq.com/@uwdata/arquero-cookbook)
# discuss
- ## 

- ## The state of data analysis
- https://www.reddit.com/r/javascript/comments/bvqy9l/the_state_of_data_analysis/
- ### Python and R are awesome for data science
- The pandas package for Python offers a data structure called DataFrame that provides a comprehensive API for manipulating data. 
- numpy: a powerful N-dimensional array object
- scipy - statistics, linear algebra, numerical integration and optimisation
- matplotlib, plotly, bokeh etc. - data visualisation
- scikit-learn - machine learning
- R is another programming language that's popular for data science. 
  - However, unlike Python, R is focused on statistical analysis. 
  - Python is a general purpose language that's good at other things besides data science.
- Jupyter notebooks have also played a huge role in making both Python and R more accessible to data scientists.
- ### JavaScript is the chosen one for web
- D3.js: for binding data to DOM elements and apply data-driven transformations.
  - plotly.js - a high-level declarative charting library.
- JavaScript doesn't have much to offer in terms of data analytics. There are a few packages that do try to mimic pandas for Python:
  - dataframe-js
  - data-forge
  - apache-arrow

    - a standardized language-independent columnar memory format for flat and hierarchical data, 
    - organized for efficient analytic operations on modern hardware.

  - @stdlib/stdlib

    - a standard library for JavaScript and Node.js, with an emphasis on numerical and scientific computing applications. 

- Because of this one shortcoming of JavaScript, i.e. poor support for data analytics, most web applications tend to handle the bulk of the data crunching in the back-end server. 
- This means that the front-end would have to request the data over the internet via HTTP. 
- The disadvantages of this approach are:
  - Computational load on the back-end.
  - Performance/User Experience penalty due to the need to make HTTP requests for 'analysed' data.
  - Cross-platform development burden.
  - More importantly, the vast majority of data scientists who are not familiar with web development do not have a way of easily sharing their contributions with the world (or to their target audience) in the form of a webpage.

- I think part of the motivation for the Dash library, has been that it's so hard to make 'web-based analytics applications' using just JavaScript.

- https://www.reddit.com/r/datascience/comments/bw0d5b/the_state_of_data_analysis/
- Having a data structure for efficiently storing data is not really the critical part for data analysis. It is a technical prerequisite.
  - More importantly: Do we have access to distribution functions such as normal or binomial PDF/CDF? 
  - Are there functions/interfaces to run statistical analysis, incl. tests, linear modelling, generalised linear modelling, ...? 
  - Not sure, but afaik JavaScript‘s abilities are very limited in this regard while both python and R provide a wide range of packages and libraries which are actively maintained by a large community for quite some time. 
  - Are there any such packages available for JavaScript?
- The `stdlib` library does provide access to various mathematical tools including probability distribution functions.
- js isn't going away - it's just most analysts don't really need it with the ubiquity of bi tools
# ref
- [THE HISTORY OF DATA SCIENCE](https://www.kausalvikash.in/blog/the-history-of-data-science/)
