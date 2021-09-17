---
title: thread-data-analysis-processing
tags: [compute, data-analysis, data-processing, thread]
created: '2021-03-09T08:37:07.404Z'
modified: '2021-05-13T16:12:47.773Z'
---

# thread-data-analysis-processing

# pieces

- ## 

- ## 

- ## 

- ## 

- ## Did you ever want to learn how to read ROC curves?
- https://twitter.com/haltakov/status/1438206936680386560
  - ROC stands for Receiver Operating Characteristic but just forget about it. 
  - Think about these curves as True Positive Rate vs. False Positive Rate plots.
  - The ROC curve visualizes the trade-offs that a binary classifier makes between True Positives and False Positives.

- ## Javascript is poised to displace R and Python (really!) as the indispensable language of data programming, touching on WebGPU/WebGL, @observablehq , and @ApacheArrow .
- https://twitter.com/benmschmidt/status/1368988766174666753
  - Computers have gotten much, much faster in the last couple decades, but our languages for data analysis have failed to keep up. (+)
  - New data formats are making the differences between Python, R, and Javascript less important.
  - Javascript, the quintessential front-end language, is increasingly becoming the back-end for data work in Python and R.
  - [Javascript and the next decade of data programming](http://benschmidt.org/post/2020-01-15/2020-01-15-webgpu/)
- this trajectory is no surprise for anybody who went from web development into "data" - possibly by way of visualization and D3's awesomeness.
  - what makes R so handy however are the thousands of readymade math/stats/ml snippets
- This seems optimistic? Getting any sort of non-toy machine learning to run, let alone train, in javascript is still really annoying. We barely have usable numpy. Maybe some day, but there is a ton of infrastructure needed.
  - Or pessimistic, depending on your POV. The dominance of python in the neural network space is an important counter-trend. It makes me use more Python than I'd like, and it forces people into the cloud. But neural networks aren't critical in every domain. (Geocomputing, say.) And+
  - Widespread WebGPU will be a completely fresh start for javascript in that domain. I haven't read the spec to know if it will really work. But consider the bonkers stuff people do working against the current in webGL wouldn't bet against it.
