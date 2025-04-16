---
title: toc-lib-dataframe
tags: [data-processing, dataframe, lib]
created: 2020-12-07T09:59:23.769Z
modified: 2021-05-13T16:14:41.762Z
---

# toc-lib-dataframe

# guide

- tips
  - 数据处理的流行方向是基于arrow实现dataframe ???

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
- polars /12.3kStar/MIT/202403/rust/NoDeps
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
- https://github.com/haifengl/smile /6.2kStar/GPLv3/202503/java
  - https://haifengl.github.io/
  - Smile is a fast and comprehensive machine learning framework in Java
  - Smile covers every aspect of machine learning, including deep learning, large language models, classification, regression, clustering...
  - GenAI: Native Java implementation of Llama 3.1, tiktoken tokenizer, high performance LLM inference server with OpenAI-compatible APIs and SSE-based chat streaming
  - Deep Learning: Deep learning with CPU and GPU. EfficientNet model for image classification.
  - Smile comes with interactive shells for Java, Scala and Kotlin. 
  - This library also support data visualization in declarative approach. The specification is based on Vega-Lite.
  - [DataFrame为什么提供那么多功能类似的接口 _202407](https://github.com/haifengl/smile/issues/783)
    - Apply is a helper function for scala so that you can do df(“column name”), which is same as df.column(“column name”) in Java. 
    - Because Java is strong typed, we have to use getXXX to distinguish the return type when get a field value.

- https://github.com/dflib/dflib /apache2/202504/java
  - https://dflib.org/
  - In-memory Java DataFrame library
  - a lightweight pure Java implementation of a common DataFrame data structure.
  - DFLib provides integration with Apache Echarts to visualize DataFrame data. 
  - While DFLib works in any Java application, it has a special intergation with Jupyter Notebook, a browser-based interactive environment

- https://github.com/jtablesaw/tablesaw /3.6kStar/apache2/202504/java
  - https://jtablesaw.github.io/tablesaw/
  - a dataframe and visualization library that supports loading, cleaning, transforming, filtering, and summarizing data
  - Tablesaw also supports descriptive statistics and can be used to prepare data for working with machine learning libraries like Smile, Tribuo, H20.ai, DL4J.
  - 项目未持续发展的原因是没有结合machine learning的需求
  - Import data from RDBMS, Excel, CSV, TSV, JSON, HTML, or Fixed Width text files, whether they are local or remote (http, S3, etc.)
  - Export data to CSV, JSON, HTML or Fixed Width files.
  - Combine tables by appending or joining
  - Add and remove columns or rows
  - Sort, Group, Filter, Edit, Transpose, etc.
  - Map/Reduce operations
  - Handle missing values
  - Descriptive stats: mean, min, max, median, sum, product, standard deviation, variance, percentiles, geometric mean, skewness, kurtosis, etc.
  - data visualization by providing a wrapper for the `Plot.ly` JavaScript plotting library
  - We recommend trying Tablesaw inside Jupyter notebooks, which lets you experiment with Tablesaw in a more interactive manner. Get started by installing BeakerX
  - [Is there any plan to release a new version since the lasted version had past two years _202406](https://github.com/jtablesaw/tablesaw/issues/1251)
    - 👷: The project should be considered deprecated. If anyone wants to fork it, that's fine with me.
  - [Stepping back from Tablesaw _202309](https://github.com/jtablesaw/tablesaw/discussions/1233)
    - I've reassessed how I spend my time, and find I'm no longer sufficiently interested in the project to devote time to it. 
  - [Discussion: Apache Arrow](https://github.com/jtablesaw/tablesaw/issues/288)
    - Re-opening to add arrow support and get rid of saw support, assuming Arrow io is at least as fast.
    - 202204: Baseline support is added. It may be desirable/necessary to modify the interface to fit better with existing reader/writer framework
  - [Is it possible to fetch a preview of a dataset from a cloud source? · jtablesaw/tablesaw · Discussion _202107](https://github.com/jtablesaw/tablesaw/discussions/960)
    - For remote access we use a Stream-based API and, AFAIK, there is no way to retrieve a preview.
  - [How much data can tablesaw store at most?  ](https://github.com/jtablesaw/tablesaw/issues/290)
    - The memory usage of different methods is often highly dependent on the number of columns, their types, and the cardinality of the values.
  - [Using stream().parallel()](https://github.com/jtablesaw/tablesaw/issues/841)
    - 202106: Tablesaw is not thread safe, by design. To make it thread safe would be much harder and probably quite a bit slower. It is really designed for a single user doing data analysis.
  - [Is "Table" Thread safe ? _202101](https://github.com/jtablesaw/tablesaw/issues/858)
    - Table was designed for data analysts rather than as a server component so no attempt was made to make it thread safe.
    - That said, most methods (not all) return a new table as the result so it might be possible to use it for some limited applications.
  - [Feature: Streaming imports from CSV to .saw _201606](https://github.com/jtablesaw/tablesaw/issues/4)
    - Write an importer that simply streams data from CSV direct to .saw output, so that interactive use of the data can proceed quickly
  - [Tablesaw version 1.0 _202110](https://github.com/jtablesaw/tablesaw/discussions/1013)
  - [Version 1.0 (Moving Tablesaw to Java 11) _202203](https://github.com/jtablesaw/tablesaw/discussions/1075)
    - Update the language level to Java 11 (or higher)
    - For Tablesaw to be included in projects that use the Java module system, as real modules, we need to be on Java 9.0 or later as the language level. The current fallback is to put Tablesaw on the class path rather than the module path for the modules. 
    - Added support for sort-merge join as an alternative to the current "nested-loop" or cross product join to improve performance where both Tables are large. 
    - Adding IO support for Apache Arrow.
  - [Support for multiple backends? _201708](https://github.com/jtablesaw/tablesaw/issues/130)
    - Multiple backends are interesting, and I like what Morpheus has done. I have considered for some time using off-heap memory for a second backend, and found a library I like to help with that. I assume this is what Morpheus' mapped backend does. It would require some additional research to look into what it would take to provide the same functionality as the current tablesaw.
    - I have some concern about adding more backends before some of the core functionality is complete. I suspect it would slow down feature development and we're still missing some big things like joins.
  - 🍴 forks
  - https://github.com/tlabs-data/tablesaw

- https://github.com/burukeYou/JDFrame /apache2/202412/java
  - https://burukeyou.github.io/JDFrame/
  - 一个Java仿DataFrame模型的实现, 语意化和简化以及增强stream流式处理能力
  - 提供了DataFrame模型的若干基本功能比如复杂数据筛选、分组聚合、窗口函数、连接矩阵
# cpp
- https://github.com/hosseinmoein/DataFrame
  - /730Star/BSD/202012
  - a C++ statistical library that provides an interface similar to Pandas package in Python.
  - A DataFrame can have one index column and many data columns of any built-in or user-defined type.
  - DataFrame for statistical, Financial, and ML analysis in modern C++ using native types, continuous memory storage, and no pointers are involved
- https://github.com/rapidsai/cudf
  - GPU DataFrame Library
