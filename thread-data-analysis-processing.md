---
title: thread-data-analysis-processing
tags: [compute, data-analysis, data-processing, thread]
created: 2021-03-09T08:37:07.404Z
modified: 2021-05-13T16:12:47.773Z
---

# thread-data-analysis-processing

# guide

# discuss-stars
- ## 

- ## Hot take: Using dashboards for analysis is an antipattern
- https://twitter.com/ergestx/status/1761013565115322689
- If a dashboard is designed for data exploration or analysis it will eventually be dumped into Excel

- ## 🐍📈 NVIDIA just made Pandas 150x faster with zero code changes
- https://twitter.com/Sumanth_077/status/1751251621143838914
  - All you have to add is just a couple of lines of code

```Python
%load_ext cudf.pandas
import pandas as pd
```

- Pandas operates in-memory, as it loads the entire dataset into the local memory of the machine it is running on. This limits its ability to handle large datasets.
  - With cuDF’s pandas accelerator you can now bring accelerated computing to pandas workflows.

- Also their cuDF library will automatically know if you're running on GPU or CPU and speed up your processing.
# discuss
- ## 

- ## 

- ## Another important component in Time Series data is the noise.
- https://twitter.com/daansan_ml/status/1768622446037594453
  - The noise component refers to the random or irregular fluctuations that are not explained by the underlying patterns or trends in the data.

- The noise component can arise from various sources, including:
  1️⃣ Measurement errors
  2️⃣ Random shocks or events
  3️⃣ Unobserved or unmodeled factors
  4️⃣ Inherent variability

- ## Volatility can be a big problem in Time Series forecasting!
- https://twitter.com/daansan_ml/status/1736295237184897157
  - volatility(波动的，不稳定的) is a statistical measure of the dispersion of data or variance around its mean over a certain period of time.
  - In finance, it refers to how much the price changes between periods.
  - Generally, at least in finance, there are periods of high volatility followed by periods of low volatility, and vice versa.
  - High volatility makes forecasting hard. So it would be useful to model it.
  - Luckily for us, we have the ARCH model, which stands for "AutoRegressive Conditional Heteroskedasticity".
  - We can use ARCH models for predicting the variance (volatility), while we use ARIMA for the mean.

- ## When you aggregate & simplify data, you often lose the signal & context needed to make sense of what you are seeing.
- https://twitter.com/observablehq/status/1499412568330280962
  - [Stop aggregating away the signal in your data](https://stackoverflow.blog/2022/03/03/stop-aggregating-away-the-signal-in-your-data/)

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
