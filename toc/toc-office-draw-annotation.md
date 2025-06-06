---
title: toc-office-draw-annotation
tags: [annotation, drawing, office, toc]
created: 2023-11-03T17:42:38.566Z
modified: 2023-11-03T17:43:01.518Z
---

# toc-office-draw-annotation

# guide
- 画板或批注类产品要参考规范 [Web Annotation Data Model](https://www.w3.org/TR/annotation-model/)
  - 富文本格式也可参考
  - 对image/pdf/富文本编辑器的标注，通常流行产品都会有产品自身的实现，不必执着于标准
# popular
- https://github.com/HumanSignal/label-studio /apache2/202503/python/ts
  - Label Studio is an open source data labeling tool. 
  - It lets you label data types like audio, text, images, videos, and time series with a simple and straightforward UI and export to various model formats. 
  - It can be used to prepare raw data or improve existing training data to get more accurate ML models.
  - Support for multiple data types including images, audio, text, HTML, time-series, and video.
  - Import from files or from cloud storage in Amazon AWS S3, Google Cloud Storage, or JSON, CSV, TSV, RAR, and ZIP archives.
  - Integration with machine learning models so that you can visualize and compare predictions from different models and perform pre-labeling.
  - Integration with machine learning models so that you can visualize and compare predictions from different models and perform pre-labeling.
# annotation
- https://github.com/apache/incubator-annotator /apache2/202211/ts/inactive
  - https://annotator.apache.org/
  - provides annotation enabling code for browsers, servers, and humans.
  - The goal is to help developers of annotation tools create their applications without having to reinvent the wheel, while applying a standards-driven approach based on the W3C’s Web Annotation data model, in order to facilitate an ecosystem of interoperable annotation tools 
  - [Web Annotation Protocol Server](https://github.com/apache/incubator-annotator/issues/70)
    - https://github.com/snvfk1n/simple-annotation-server /MIT/202007/js/inactive
    - https://code.treora.com/gerben/web-annotation-discovery-server /20221p/inactive

- https://github.com/opendatalab/LabelLLM /apache2/202502/python/ts
  - The Open-Source Data Annotation Platform
  - including audio, images, and video
- https://github.com/opendatalab/labelU-Kit /apache2/202503/ts
  - https://opendatalab.github.io/labelU-Kit/
  - https://labelu.shlab.tech/
  - LabelU前端标注组件库，支持图片2D框、点、线、多边形、立体框及混合标注工具，可用于标注平台开发集成，开箱即用。
  - 支持视频标注
  - 支持音频标注
  - https://github.com/opendatalab/labelU /apache2/202503/python
    - https://opendatalab.github.io/labelU/
    - Data annotation toolbox supports image, audio and video data.
    - Universality: Supports exporting to various data formats, including JSON, COCO, MASK.

- https://github.com/hypothesis/pdf.js-hypothes.is /bsd/202208/js/专注于标注
  - https://web.hypothes.is/
  - This is a copy of Mozilla's PDF.js viewer with Hypothesis annotation tools added.
  - https://github.com/hypothesis/h /2.8kStar/bsd/202311/python
    - h is the web app that serves most of the https://hypothes.is/ website, including the web annotations API 
    - The Hypothesis client is a browser-based annotator that is a client for h's API.
- https://github.com/instructure/pdf-annotate.js /MIT/201812/js/archived
  - Annotation layer for pdf.js (no longer maintained)

- https://github.com/rough-stuff/rough-notation /MIT/202010/ts
  - https://roughnotation.com/
  - Create and animate hand-drawn annotations on a web page
  - uses RoughJS to create a hand-drawn look and feel

- https://github.com/kba/anno-common /MIT/202105/js/inactive
  - https://kba.github.io/anno
  - This monorepo contains packages that provide the building blocks for annotation software implementing the Web Annotation Data Model and Web Annotation Protocol.
  - A store provides persistent storage of annotations. A store exposes methods that reflect the Web Annotation Protocol and the extensions implemented of this framework.
  - The store-mongolike module implements most of the store interface for document databases, such as mongodb or NeDB.

- https://github.com/goodmansasha/annotation-model /js
  - https://goodmansasha.github.io/annotation-model/
  - Javascript implementation of the W3C Web Annotation Data Model, useful for Web Extensions and serializing references to specific resources on a HTML page

- https://github.com/openannotation/annotator /MIT/201511/js/inactive
  - http://annotatorjs.org/
  - Annotation tools for the web. Select text, images, or (nearly) anything else, and add your notes.
  - It provides a set of interoperable tools for annotating content in webpages.

- https://github.com/out-of-cheese-error/gooseberry /MIT/202208/rust
  - A command line utility to generate a knowledge base from Hypothesis annotations
  - made with asciinema, svg-term-cli, and svgembed
  - Gooseberry provides a command-line interface for Hypothesis (a tool to annotate the web) and lets you generate a knowledge-base wiki without you having to actually type your knowledge out.
  - Gooseberry combines the ease of annotation offered by Hypothesis, bulk tagging and organization support in the command line, and a customizable plaintext wiki with HandleBars templating.

- https://github.com/UniversalDataTool/universal-data-tool /MIT/202205/js/inactive
  - Collaborate & label any type of data, images, text, or documents, in an easy web interface or desktop app.
  - a web/desktop app for editing and annotating images, text, audio, documents and to view and edit any data defined in the extensible `.udt.json/.udt.csv` standard.
  - Usable on web or as Windows, Mac or Linux desktop application
  - https://github.com/UniversalDataTool/react-image-annotate
    - Create image annotations. Classify, tag images with polygons, bounding boxes or points.

- https://github.com/osuresearch/annotator /MIT/202305/ts/inactive
  - https://osuresearch.github.io/annotator
  - React components for annotating forms and documents
  - 依赖tiptap2、@osuresearch/ui、mantine-hooks、iframe-resizer、react-aria、react-hook-form
  - https://github.com/osuresearch/ui
    - https://osuresearch.github.io/ui/v5
    - Research UI is The Ohio State University's Office of Research component library, based on Ohio State's design system - BUX.
    - 依赖react-aria
  - https://github.com/osuresearch/electron-example
    - Electron React Boilerplate uses Electron, React, React Router, Webpack and React Fast Refresh.
# anno-server
- https://github.com/jankaszel/simple-annotation-server /MIT/202007/js/inactive
  - simple annotation server intended for testing purposes, implementing both the Web Annotation Protocol as well as the Web Annotation Data Model with simple REST-based user management. 
  - The server is written in JavaScript and runs in Node.js, running an in-process LevelDB database.

- https://github.com/BigBlueHat/anno-proto-coucho /201610/js
  - Web Annotation Protocol Server built on Apache CouchDB
  - Apache CouchDB's HTTP API is quite similar to the Web Annotation Protocol except the later is specific to Annotation.
# more
