---
title: lib-data-community
tags: [community, data-analysis, data-processing, lib]
created: 2021-05-13T14:36:20.064Z
modified: 2021-05-13T16:11:33.402Z
---

# lib-data-community

# guide

- [Arquero Cookbook](https://observablehq.com/@uwdata/arquero-cookbook)
# data-dev

# blogs
- [THE HISTORY OF DATA SCIENCE](https://www.kausalvikash.in/blog/the-history-of-data-science/)
# discuss
- ## 

- ## 

- ## 

- ## [Comprehensive Study of Open Data Platforms | by Digvijay Mali | Analytics Vidhya | Medium _202010](https://medium.com/analytics-vidhya/comprehensive-study-of-open-data-platforms-a63d702ef0d5)
- Advantages of CKAN
  1. Better Visualization
  2. Easy maintenance
  3. It keeps things light
  4. Selective Update
  5. Integration with Google Analytics

- Socrata is a software-as-a-service platform focused on the principle of ‘data in API out’ offering a cloud-based solution for the publication and visualization of open data.

- Other Implementation Standards
  - DSpace
  - CKAN
  - Figshare
  - Zenodo
  - Dataverse

- CKAN is mainly used by governmental institutions to disclose their data, its features. 
- DSpace enables system administrators to parametrize additional metadata schemas that can be used to describe resources.
  - Curators may favor DSpace though, since it enables system administrators to parametrize additional metadata schemas that can be used to describe resources.
  - These will in turn be used to capture richer domain-specific features that may prove valuable for data reuse
- Zenodo and Figshare provide ways to assign a permanent link and a DOI, even if the actual dataset is under embargo at the time of first citation. 
  - This will require a direct contact between the data creator and the potential reuse before access can be provided. 
  - Both these platforms are aimed at the direct involvement of researchers in the publication of their data, as they streamline the upload and description processes, though they do not provide support for domain-specific metadata descriptors. 
- A very important factor to consider is also the control over where the data is stored. 
  - Some institutions may want the servers where data is stored under their control, and to directly manage their research assets. 
  - Platforms such as DSpace and CKAN, that can be installed in an institutional server instead of relying on external storage provided by contracted services are appropriate for this. 
- CKAN may have an advantage over the remaining alternatives, as several governmental institutions are already converging to this platform for data publishing.

- ## 📌 The state of data analysis _201906
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
