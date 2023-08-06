---
title: spec-format-catalog
tags: [catalog, format, spec]
created: 2019-12-02T10:25:27.789Z
modified: 2020-10-15T13:42:23.746Z
---

# spec-format-catalog

> specifications about file formats

# guide

# popular-file-formats

- csf (Component Story Format)
  - title, component, parameters, decrators
- [Storybook for everyone: CSF vs MDX](https://dev.to/lauracarballo/storybook-for-everyone-csf-vs-mdx-88b)
  - Both CSF and MDX provide a great way of building component libraries. 
  - I recently ran a twitter poll on preferred method when writing stories and nearly 70% of the people (80 votes aprox.) voted on using CSF, which is understandable as it is still the standard and recommended way. 
  - But, MDX is still a very convenient way of writing stories in those cases where CSF seems a bit of a barrier for non technical users or our component needs precise and well structured documentation.
- [What are your thoughts on the MDX format for @storybookjs](https://twitter.com/lcarb14/status/1379913918445801473)
  - I'm currently preferring MDX as it provides both Stories and Docs with a single file.
# tabular
- https://github.com/brimdata/zed
  - [Zed Formats](https://zed.brimdata.io/docs/formats)
  - The Zed data model defines a new and easy way to manage, store, and process data utilizing an emerging concept called super-structured data. 
  - The data model specification defines the high-level model that is realized in a family of interoperable serialization formats, providing a unified approach to row, columnar, and human-readable formats.
# hierarchical/hdf
- [HDF5 数据文件简介 - 知乎](https://zhuanlan.zhihu.com/p/104145585)
  - HDF5 文件一般以 .h5 或者 .hdf5 作为后缀名，有 2 primary objects: Groups 和 Datasets
  - Groups 就类似于文件夹，每个 HDF5 文件其实就是根目录 (root) group'/'。
  - Datasets 类似于 NumPy 中的数组 array
  - 每个 dataset 可以分成两部分: 原始数据 (raw) data values 和 元数据 metadata 

```
+-- Dataset
|   +-- (Raw) Data Values (eg: a 4 x 5 x 6 matrix)
|   +-- Metadata
|   |   +-- Dataspace (eg: Rank = 3, Dimensions = {4, 5, 6})
|   |   +-- Datatype (eg: Integer)
|   |   +-- Properties (eg: Chuncked, Compressed)
|   |   +-- Attributes (eg: attr1 = 32.4, attr2 = "hello", ...)
|
```

- Dataspace 给出原始数据的秩 (Rank) 和维度 (dimension)
- Properties 说明该 dataset 的分块储存以及压缩情况
  - Chunked: Better access time for subsets; extendible
  - Chunked & Compressed: Improves storage efficiency, transmission speed
- Attributes 为该 dataset 的其他自定义属性

- [HDF及HDF-EOS数据格式简介 - 知乎](https://zhuanlan.zhihu.com/p/434443399)
  - NASA把HDF格式作为存储和发布EOS （Earth Observation System）数据的标准格式。
  - 在HDF标准基础上，开发了另一种HDF格式即HDF-EOS ，专门用于处理EOS产品，使用标准HDF 数据类型定义了点、条带、栅格3 种特殊数据类型，并引入了元数据(Metadata) 

- [HDF5数据格式不适合深度学习](https://www.jdon.com/57578.html)
  - HDF5是最流行和最可靠的非表格数字数据格式之一
  - 缺点
  - HDF 文件的布局使它们难以在云存储系统（如 Amazon 的 S3 ）上进行有效查询，其中存储了越来越多的 ML 数据集
  - HDF5（Python 实现）基本上是单线程的。这意味着在给定时间只有一个核心可以读取或写入数据集。它不容易被并发读取访问
  - 由于 HDF 元数据散布在整个文件中，因此很难访问随机的数据块
# sparse 稀疏矩阵

# JSON-stat
- docs
  - https://json-stat.org/
  - https://github.com/jsonstat/toolkit
  - https://json-stat.org/samples/oecd.json

- Until the introduction of JSON-stat, the main statistical standards for data and metadata exchange were XML-based: they were usually complicated and verbose.
- JSON-stat is a simple lightweight JSON dissemination format best suited for data visualization, mobile apps or open data initiatives, that has been designed for all kinds of disseminators(传播者).
  - JSON-stat also proposes an HTML microdata schema to enrich HTML tables and put the JSON-stat vocabulary in the browser.

- The JSON-stat format is a simple lightweight JSON format for data dissemination. 
  - It is based in a cube model that arises from the evidence that the **most common form of data dissemination is the tabular form**.
- HTML microdata allows machine-readable data to be embedded in HTML documents in the form of nested groups of name-value pairs. 
  - JSON-stat proposes a vocabulary in microdata format to enrich HTML tables.
- If you have to process JSON-stat responses, you are not on your own. 
  - There are solutions available in several programming languages: JavaScript, Java, R, Python, Julia, PHP. 
  - And many end user tools to browse, filter, validate and convert JSON-stat.
# graphics
- SVG(SCALABLE VECTOR GRAPHICS)
  - SVG is a markup language for describing two-dimensional graphics applications and images, and a set of related graphics script interfaces. 
  - [SVG Working Group Charter](https://www.w3.org/Graphics/SVG/2014/new-charter)
  - [SVG Roadmap](https://www.w3.org/Graphics/SVG/WG/wiki/Roadmap)
# domains/apps
- [FHIR v4.3.0](https://www.hl7.org/fhir/)
  - FHIR is a standard for health care data exchange, published by HL7
# ref
- [Understand how structured data works](https://developers.google.com/search/docs/guides/intro-structured-data)
  - Structured data is a standardized format for providing information about a page and classifying the page content
  - Most Search structured data uses schema.org vocabulary, but you should rely on the documentation on developers.google.com as definitive for Google Search behavior
  - [JSON-LD](http://json-ld.org/)
    - A JavaScript notation embedded in a `<script>` tag in the page head or body. 
    - Google can read JSON-LD data when it is dynamically injected into the page's contents
  - [RDFa](https://rdfa.info/)
    - An HTML5 extension that supports linked data by introducing HTML tag attributes that correspond to the user-visible content that you want to describe for search engines. 
    - RDFa is commonly used in both the head and body sections of the HTML page.
  - [Microdata](https://www.w3.org/TR/microdata/)
    - An open-community HTML specification used to nest structured data within HTML content. 
    - It is typically used in the page body, but can be used in the head.
