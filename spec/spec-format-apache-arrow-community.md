---
title: spec-format-apache-arrow-community
tags: [apache-arrow, community]
created: '2021-07-24T08:16:02.068Z'
modified: '2021-07-24T08:16:41.076Z'
---

# spec-format-apache-arrow-community

# pieces

- ## 

- ## 

- ## 

- ## 

- ## Streamlit is now more performant thanks to @ApacheArrow !
- https://twitter.com/streamlit/status/1418637045468000256
  - Using Arrow for data serialization helped us delete over 1, 000 lines of code 
- In general, the performance improvements come from reduced data serialization time (i.e. sending data from Python to the browser).
  - But pandas itself is also becoming faster due to Apache Arrow, so having both pandas and Streamlit using the same format should yield improvements
  - The app creator still needs to think about their workflow, use caching as appropriate, etc. **Apache Arrow can't fix algorithmic complexity of complex transformations**
