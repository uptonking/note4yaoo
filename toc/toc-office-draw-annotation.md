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
- https://github.com/HumanSignal/label-studio /26kStar/apache2/202512/python/ts
  - https://labelstud.io/
  - a multi-type data labeling and annotation tool with standardized output format
  - It lets you label data types like audio, text, images, videos, and time series with a simple and straightforward UI and export to various model formats
  - `label-studio-converter`	Encode labels in the format of your favorite machine learning library
  - 依赖Django
  - [Export Annotations](https://labelstud.io/guide/export.html)
    - Label Studio stores your annotations in a raw JSON format in the SQLite database backend, PostgreSQL database backend, or whichever cloud or database storage you specify as target storage.
    - Image annotations exported in JSON format use percentages of overall image size, not pixels, to describe the size and location of the bounding boxes. 
    - Label Studio supports many common and standard formats for exporting completed labeling tasks.
    - coco, csv,json,CONLL2003/spaCy/YOLO

- https://github.com/lkk688/VisionLangAnnotate /MIT/202511/python/inactive
  - an advanced vision-language annotation framework that enables dynamic object detection and annotation based on natural language prompts.
  - VisionLangAnnotate consists of two main components:
    - Traditional Object Detection Pipeline: Multiple object detection models (DETR, YOLO, RT-DETR)
    - Vision-Language Models (VLM) Backend: llava, Qwen2.5-VL
  - Detect objects based on natural language descriptions
  - Combines traditional object detectors with Vision-Language Models
  - Unified API: Simple interface for various detection and annotation tasks
  - Generate annotations on-the-fly based on user requests
  - Support for both image and video inputs
  - Zero-Shot Capabilities: Detect novel objects without prior training
  - Export detection results to Label Studio compatible JSON format
  - Complete Annotation Loop: End-to-end pipeline from user requests to data pre-processing, object detection, vision annotation, and human validation

- https://github.com/recogito/text-annotator-js /BSD/202601/ts
  - A JavaScript library for adding interactive text annotation functionality to web applications.
  - The Text Annotator data model aligns closely with the W3C Web Annotation Data Model, but with a few key differences to optimize for performance and ease of use. 
    - Every annotation in Annotorious is represented by a JavaScript object with the following structure
# annotation
- https://github.com/apache/incubator-annotator /apache2/202211/ts/inactive
  - https://annotator.apache.org/
  - provides annotation enabling code for browsers, servers, and humans.
  - The goal is to help developers of annotation tools create their applications without having to reinvent the wheel, while applying a standards-driven approach based on the W3C’s Web Annotation data model, in order to facilitate an ecosystem of interoperable annotation tools 
  - [Fragment selector for PDFs + PDF.js integration _202206](https://github.com/apache/incubator-annotator/issues/125)
    - I recently found out that PDF.js is adding full annotation editing support to the library, which can be tracked here: PDF.js editing. I think this could be a great opportunity to push forward the fragment selector for PDFs to try to integrate it with PDF.js
    - It seems that pdf's annotation is more complex than Web Annotation so we can not just transofrm pdf's annotation to Web Annotation. For example, pdf's annotation can be random shape while we can only mark a rectangle by web annotation.
    - Web Annotation spec also supports non-rectangular selections
    - You can see an example of a non-rectangular SVG selector in this IIIF cookbook recipe
  - [Feature to save annotations in JSON format following the Web Annotation Data Model · Issue · mozilla/pdf.js _202206](https://github.com/mozilla/pdf.js/issues/15055)
    - I don't believe it's going to be "full" editing support, given the sheer number of Annotation-types that the PDF specification support, but most likely rather a few commonly used types.
    - We will work on an external library to access `AnnotationStorage` and exporting the annotations.
  - [Web Annotation Protocol Server](https://github.com/apache/incubator-annotator/issues/70)
    - https://github.com/snvfk1n/simple-annotation-server /MIT/202007/js/inactive
    - https://code.treora.com/gerben/web-annotation-discovery-server /20221p/inactive

- https://github.com/opendatalab/LabelLLM /apache2/202502/python/ts/inactive
  - The Open-Source Data Annotation Platform
  - including audio, images, and video
  - 主要是 运营管理端 + 任务执行端
- https://github.com/opendatalab/labelU /1.5kStar/apache2/202510/python
  - https://opendatalab.github.io/labelU/
  - Data annotation toolbox supports image, audio and video data.
  - 多功能图像标注工具，包括2D框、语义分割、多段线、关键点等多种标注方式
  - 支持视频分割、视频分类以及视频信息提取等功能
  - 支持音频分割、音频分类和音频信息提取
  - 通过集成AI模型，可以实现自动标注，提高标注效率。
- https://github.com/opendatalab/labelU-Kit /141Star/apache2/202511/ts
  - https://opendatalab.github.io/labelU-Kit/
  - https://labelu.shlab.tech/
  - https://opendatalab.github.io/labelU/playground/image
  - LabelU前端标注组件库，支持图片2D框、点、线、多边形、立体框及混合标注工具，可用于标注平台开发集成，开箱即用。
  - 支持视频标注
  - 支持音频标注
  - https://github.com/opendatalab/labelU /apache2/202503/python
    - https://opendatalab.github.io/labelU/
    - Data annotation toolbox supports image, audio and video data.
    - Universality: Supports exporting to various data formats, including JSON, COCO, MASK.

- https://github.com/hypothesis/pdf.js-hypothes.is /403Star/bsd/202208/js/专注于标注
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
  - https://universaldatatool.com/
  - https://universaldatatool.github.io/react-image-annotate/
  - Collaborate & label any type of data, images, text, or documents, in an easy web interface or desktop app.
  - a web/desktop app for editing and annotating images, text, audio, documents and to view and edit any data defined in the extensible `.udt.json/.udt.csv` standard.
  - Usable on web or as Windows, Mac or Linux desktop application
  - https://github.com/UniversalDataTool/react-image-annotate /MIT/202201/js/inactive
    - Create image annotations. Classify, tag images with polygons, bounding boxes or points.
  - 未支持 [OCR Annotation Support ](https://github.com/UniversalDataTool/universal-data-tool/issues/532)
  - [Feature: PDF Image Annotation _202004](https://github.com/UniversalDataTool/universal-data-tool/issues/49)
    - Been working with PDF in the past and, imo, the best is to convert everything to JPG using a lib like `pdf2image` or something similar. That allows control over the DPI for the image creation that should not be overlooked when comes the time to do inference. 
    - If we want to make something that is not well supported by other annotation tools or lib, something like PDF2text with a 2D mapping between the raw text and the original PDF would be insane. 
    - This is not easy to do, in Python I use pdfminer and pypdf2 to extract text. pdfminer can return coords of each letter/words while pypdf2 can't. 

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
# labelling-image/pdf
- https://github.com/annotorious/annotorious /809Star/BSD/202512/ts/vanillajs
  - http://annotorious.dev/
  - Add image annotation functionality to any web page with a few lines of JavaScript.
  - 给图片添加绘制 rect/polygon 的工具条
  - Annotorious integrates seamlessly with OpenSeadragon, allowing you to annotate high-resolution zoomable images

- https://github.com/mire403/VisionForge /202601/ts
  - VisionForge是一个轻量级、高扩展性的大模型图片训练&描述工具生成器，支持多家大模型API（Google、OpenAI 兼容、DeepSeek、Qwen、GLM、Claude、Doubao、自定义模型）。 它提供多图片上传、提示词优化、自动生成JSONL训练数据、多项信息分析（标签、OCR、场景分类、主色调、置信度、推理原因）等能力。 支持实时统计图表（置信度分布直方图与趋势曲线），适用于AI数据集制作、图像训练样本生成、遥感标注、计算机视觉模型预处理等场景。
  - Prompt双区交互：主 Prompt 区（用于图片标注/训练生成） + AI 优化助手（输入想法 → 一键优化并填充到主 Prompt）。
  - 三种输入方式：图片文件 / 图片文件夹（多图） / JSONL（可选，自动识别字段并映射）。
  - 实时运行视图：点击运行前仍保留数据集网格预览，点击运行后自动切换为实时日志/列表视图，展示每张图片的进度与输出。
  - 统计与可视化：标签词频、置信度直方图、置信度排序曲线（ranked confidence）、并支持将图导出为图片。
  - 导出功能：标准 JSONL（每行一条）、可选扩展字段、TXT 报告（统计）及图表导出。

- https://github.com/ZitySpace/react-annotate /ts
  - https://react-annotate-demo.vercel.app/
  - React component for computer vision dataset annotation
  - 依赖fabric、react-draggable、use-gesture

- https://github.com/labelflow/labelflow /ts
  - https://labelflow.ai/
  - an open platform for image labeling.

- https://github.com/NaturalIntelligence/imglab /1kStar/MIT/201910/js/inactive
  - https://solothought.com/imglab/
  - A web based tool to label images for objects that can be used to train dlib or other object detectors.
  - https://github.com/rachelcao277/LabelImage
    - 一款用于深度学习分割模型训练的图像标注工具（生成.json文件）
# anno-server
- https://github.com/jankaszel/simple-annotation-server /MIT/202007/js/inactive
  - simple annotation server intended for testing purposes, implementing both the Web Annotation Protocol as well as the Web Annotation Data Model with simple REST-based user management. 
  - The server is written in JavaScript and runs in Node.js, running an in-process LevelDB database.

- https://github.com/BigBlueHat/anno-proto-coucho /201610/js
  - Web Annotation Protocol Server built on Apache CouchDB
  - Apache CouchDB's HTTP API is quite similar to the Web Annotation Protocol except the later is specific to Annotation.
# more
