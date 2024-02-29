---
title: toc-lib-dataframe
tags: [data-processing, dataframe, lib]
created: 2020-12-07T09:59:23.769Z
modified: 2021-05-13T16:14:41.762Z
---

# toc-lib-dataframe

# guide

- [How do pandas DataFrames work?](https://leontrolski.github.io/fake-data-frame.html)
# data-notebook
- https://github.com/jupyter/jupyter
  - /11.4kStar/BSD/202012/python
  - https://github.com/jupyter/notebook
    - Jupyter notebook is a web-based notebook environment for interactive computing.
- https://github.com/CartoDB/cartoframes
  - A Python package for integrating CARTO maps, analysis, and data services into data science workflows.
  - Python data analysis workflows often rely on the de facto standards pandas and Jupyter notebooks.
  - CARTOframes give the ability to communicate reproducible analysis while providing t
  - he ability to gain from CARTO's services like hosted, dynamic or static maps and Data Observatory augmentation.
# python
- https://github.com/pandas-dev/pandas
  - /27.5kStar/BSD/202011
  - 依赖 NumPy, python-dateutil, pytz
  - powerful Python data analysis toolkit
  - providing labeled data structures similar to R data.frame objects, statistical functions, and much more
  - ref
    - https://github.com/adamerose/PandasGUI
- https://github.com/numpy/numpy
  - /15.7kStar/BSD/202012
  - NumPy is the fundamental package needed for scientific computing with Python.

- https://github.com/modin-project/modin
  - Speed up your Pandas workflows by changing a single line of code

- https://github.com/wesm/feather /202102/inactive
  - Feather: fast, interoperable binary data frame storage for Python, R, and more powered by Apache Arrow
# rust
- polars /12.3kStar/MIT/202301/rust/NoDeps
  - https://github.com/pola-rs/polars
  - https://pola.rs/
  - Polars is a blazingly fast DataFrames library implemented in Rust using Apache Arrow Columnar Format as the memory model.
  - multi-threaded, hybrid-streaming DataFrame library in Rust | Python | Node.js
  - If you have data that does not fit into memory, polars lazy is able to process your query (or parts of your query) in a streaming fashion
  - In the TPCH benchmarks polars is orders of magnitudes faster than pandas, dask, modin and vaex on full queries (including IO).

- https://github.com/Eventual-Inc/Daft /apache2/202402/rust/python
  - https://getdaft.io/
  - Daft is a distributed query engine for large-scale data processing in Python and is implemented in Rust.
  - Seamless Interchange: Built on the Apache Arrow In-Memory Format
  - Familiar interactive API: Lazy Python Dataframe for rapid and interactive iteration
  - Full integration with data catalogs such as Apache Iceberg
  - Built for the cloud: Record-setting I/O performance for integrations with S3 cloud storage
# java
- https://github.com/jtablesaw/tablesaw
  - /2.4kStar/Apache2/202011
  - It includes a dataframe and a visualization library, as well as utilities for loading, transforming, filtering, and summarizing data.
- https://github.com/haifengl/smile
  - Statistical Machine Intelligence & Learning Engine
# cpp
- https://github.com/hosseinmoein/DataFrame
  - /730Star/BSD/202012
  - a C++ statistical library that provides an interface similar to Pandas package in Python.
  - A DataFrame can have one index column and many data columns of any built-in or user-defined type.
  - DataFrame for statistical, Financial, and ML analysis in modern C++ using native types, continuous memory storage, and no pointers are involved
- https://github.com/rapidsai/cudf
  - GPU DataFrame Library
