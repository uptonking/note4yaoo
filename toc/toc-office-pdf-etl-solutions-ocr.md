---
title: toc-office-pdf-etl-solutions-ocr
tags: [etl, examples, ocr, pdf, rag, solutions, toolchain]
created: 2026-04-07T12:06:57.196Z
modified: 2026-04-07T12:53:38.419Z
---

# toc-office-pdf-etl-solutions-ocr

# guide
- tips-ocr
  - popular-on-github: tesseract/OCRmyPDF(71k), PaddleOCR(67k), MinerU(51k), DeepSeek-OCR(21k)
  - 图片的使用场景比文档更高, ocr/translation的方案要考虑图片场景
  - 传统的ocr方案还没有结合llm来优化效果，而是应用层的数据处理管线开始用llm来提高质量和准确度
  - 🐛 ? 含图片内容的ocr结果是 markdown + base64图片
  - ⏳ 文本/富文本/原文的版本管理如何设计
  - 批量执行ocr的架构可参考papermerge/paperless
  - ocr API的用法还可以参考 基于llm的文本提取, 基于openai api来提取文本/ocr
  - ~~vlm流式输出的方案配合编辑器流式构建内容的ux体验会很好~~ , 前端交互重要性不高

- 支持多种ocr方案的实现
  - ragflow: docling, mineru, paddleocr
  - mineru-tianshu: MinerU, PaddleOCR-VL
  - pdfstract: docling, paddleocr, marker, pytesseract
  - docutranslate: docling, mineru

- pdf/ppt/image-editor
  - 编辑的一种思路: 图片 > html > svg, 其中图片转html的思路可参考 design to code
    - 此时编辑ppt的需求可转换为编辑html代码
    - 基于代码的方案交互性强
  - 编辑的一种思路: 生成图片后，(用inpaint)remove所有文字，然后再把文本渲染到bbox
    - 基于图片的方案方便缩放
    - 根据现有slides生成(inpaint)去文本的底图, 再将ocr的文本叠加上去
  - 编辑的一种思路: 直接生成svg，然后右键转换为形状
  - 不要执着于pdf/ppt编辑器, 现在市场需求很大的是nano-banana文生图的编辑
  - 基于ocr的方案 相对于 基于代码的方案 的优点，用户能直接拖拽修改文本/图形
  - ❓ 是否要对ppt格式的pdf单独处理，因为包含的文本较少，背景图片及图形可能不完整
  - 还可以参考漫画manga的编辑/翻译方案

- 💡 pdf的文本化
  - 输出不一定是markdown, 各厂商都有自己的偏向, qwenvl-html, Nanonets-markdown, docling-doctags
  - 可以不做完全体ocr，而优化重点数据的ocr，如 pdf-table > excel
  - vlm也可以提取bounding-box + 手动分割图片为主来提取表格、图表、图片
  - 更简单但低质量的方案，编辑器仅显示分页，每个编辑器页面和图片pdf的一页对应，编辑器内容为vlm识别的文本(不遵循pdf布局位置)，鼠标在点击识别文本处执行boundingbox搜索pdf图片的位置，并渲染高亮元素, 🤔🖼️ 这种方案的核心是图片操作
  - 🤔 统一文本搜索高亮的双栏ux-pdf/docx/xlsx: 左侧是类似vscode的结果列表(非分页布局), 右侧是原文预览

- ocr-labelling/annotation 没有统一标准
  - tesseract hocr
  - label-studio export format
  - pdfjs AnnotationStorate支持导出json然后手动转换
  - 图片查看器iiif不是专门为 anno 定制的标准
  - W3C’s Web Annotation 用户不多, apache项目搁置
  - 各模型都有自己偏向的格式，如paddle/qwenvl-bbox

- pdf/image/canvas-tools, 主流语言是js/python
  - sharp(apache2/js/cpp)-基于 libvips(LGPL/c), jimp(MIT/ts)
  - ImageMagick(FreeWithAttribution/c)
  - jspdf(MIT/js), react-pdf(MIT/ts), pdfkit(MIT/js)
  - scikit-image(BSD/py), Pillow(MIT/py/c)
  - docling(MIT/py), OCRmyPDF(MPL/py), pypdf(BSD/py), pdfplumber(MIT/py), PyMuPDF(AGPL/py)
  - gotenberg(MIT/go/libreoffice), pdfcpu(apache2/go)
  - imgproxy(MIT/go), imaginary(/MIT/go), imaging(MIT/go), imagor(apache2/go)
  - lazy-image(MIT/rs), photon(apache2/rs)
  - OpenImageIO(apache2/cpp)
  - sumatrapdf(GPL/c)
  - libreoffice(MPL/cpp)
  - pandoc(GPL/haskell)
  - gui-wrapper工具可参考文件管理器的逻辑

- resources
  - [Supercharge your OCR Pipelines with Open Models _202510](https://huggingface.co/blog/ocr-open-models)
  - [Technical Analysis of Modern Non-LLM OCR Engines _202512](https://intuitionlabs.ai/articles/non-llm-ocr-technologies)
# popular
- https://github.com/docling-project/docling /39.3kStar/MIT/202509/python
  - https://docling-project.github.io/docling
  - Docling simplifies document processing, parsing diverse formats
  - Transform PDF to JSON or Markdown with ease and speed
  - Parsing of multiple document formats incl. PDF, DOCX, PPTX, XLSX, HTML, WAV, MP3, images (PNG, TIFF, JPEG, ...), and more
  - 模块化设计，集成 Unstructured、LayoutParser 等库，支持本地化处理
  - ~~需 CUDA 环境，部分功能依赖商业模型~~ 
  - Advanced PDF understanding incl. page layout, reading order, table structure, code, formulas, image classification, and more
  - Unified, expressive DoclingDocument representation format
  - export formats: Markdown, HTML, DocTags and lossless JSON
  - Plug-and-play integrations incl. LangChain, LlamaIndex, Crew AI & Haystack for agentic AI
  - Optionally applies OCR, Extensive OCR support for scanned PDFs and images
  - Support of Visual Language Models (SmolDocling)
  - Works on macOS, Linux and Windows environments. Both x86_64 and arm64 architectures.
  - https://huggingface.co/ibm-granite/granite-docling-258M /apache2
    - a multimodal Image-Text-to-Text model engineered for efficient document conversion

- https://github.com/opendatalab/PDF-Extract-Kit /8.6kStar/apache2 > AGPL/202501/python/inactive
  - https://pdf-extract-kit.readthedocs.io/zh-cn/latest/index.html
  - 布局检测：使用LayoutLMv3模型进行区域检测，如图像，表格, 标题, 文本等；
  - 公式检测：使用YOLOv8进行公式检测，包含行内公式和行间公式；
  - 公式识别：使用UniMERNet进行公式识别；
  - 光学字符识别：使用PaddleOCR进行文本识别
  - [Update license from Apache 2.0 to AGPL-3.0 _20240914](https://github.com/opendatalab/PDF-Extract-Kit/commit/1471e22384d4b02e1357926e4908296ed31dac51)
    - Since this project uses YOLO code and PyMuPDF for file processing, these components require compliance with the AGPL-3.0 license

- https://github.com/run-llama/llama_index /45.5kStar/MIT/202511/python
  - https://developers.llamaindex.ai/
  - LlamaIndex (GPT Index) is a data framework for your LLM application.
  - [[Bug]: PDF parsing does not happen with `SimpleDirectoryReader`](https://github.com/run-llama/llama_index/issues/19260)
    - I guess the default pdf reader (`pypdf`) couldn't parse your document? Feel free to swap it with anything else (like llama parse, docling, etc)
    - The unreadable PDF content happens because `SimpleDirectoryReader` relies on external libraries to extract text from PDFs, but these dependencies (`PyMuPDF/fitz` or `pdfminer.six`) are not installed by default. When they're missing, you get raw PDF markup instead of extracted text details.
  - [Add in-memory loading for non-default filesystems in PDFReader _202404](https://github.com/run-llama/llama_index/pull/12659)
    - Loading documents for large PDF files in external file systems was taking a long time. After investigation, we found that we were making a lot of requests to the external filesystem in the process. To avoid this, we first load the content in-memory and then pass it to pypdf.
    - Interesting, so this is because passing the file directly was making way too many requests, so now we fully download the file into memory and then pass it in? Is this only an issue for PDFReader?
      - We've only run into that issue with pypdf as of now.
      - it's way faster now. That's also what pypdf does if you pass it a path instead of a stream, but that only supports the default filesystem

- https://github.com/google/langextract /15.5kStar/apache2/202509/python/提交少
  - https://pypi.org/project/langextract/
  - a Python library that uses LLMs to extract structured information from unstructured text documents based on user-defined instructions.
  - Precise Source Grounding: Maps every extraction to its exact location in the source text, enabling visual highlighting for easy traceability and verification.
  - Reliable Structured Outputs: Enforces a consistent output schema based on your few-shot examples
  - Optimized for Long Documents by using an optimized strategy of text chunking, parallel processing, and multiple passes for higher recall.
  - Flexible LLM Support: Supports your preferred models, from cloud-based LLMs like the Google Gemini family to local open-source models via the built-in Ollama interface.
  - 🐛 [Proposal: Add Docling Integration for End-to-End Document Extraction  _202508](https://github.com/google/langextract/issues/184)
    - LangExtract today works only on raw text strings. In real-world workflows the source is usually a PDF , DOCX or PPTX. Users currently have to: Manually convert the file to text (losing layout & provenance).
    - Proposed Solution: Integrate Docling library as an optional front-end
  - 🐛 [Is it able to work on large PDF files? ](https://github.com/google/langextract/issues/178)
    - 👷 202508: PDF support is not available yet but it's something that I'm interested in. I have a small prototype running on my local and as the library has core aspects stabilized will work on adding this in.
  - [Question: Does Langextract work better on full documents or chunks? _202508](https://github.com/google/langextract/issues/206)
    - From my current tests it seems to work better when using docling to chunk it (at least in terms of building a knowledgegraph). I guess its due to contexual / visual chunking vs naive chunking.

- https://github.com/Unstructured-IO/unstructured /10.5kStar/apache2/202503/python
  - https://www.unstructured.io/
  - provides open-source components for ingesting and pre-processing images and text documents, such as PDFs, HTML, Word docs, and many more.

- https://github.com/microsoft/markitdown /MIT/202411/python
  - Python tool for converting files and office documents to Markdown.
  - a utility tool for converting various files to Markdown (e.g., for indexing, text analysis, etc.)
  - supports: PDF (.pdf) PowerPoint (.pptx) Word (.docx) Excel (.xlsx) Images (EXIF metadata, and OCR) Audio (EXIF metadata, and speech transcription) HTML (special handling of Wikipedia, etc.) Various other text-based formats (csv, json, xml, etc.)
  - [PDF performance (PDFMiner) _202505](https://github.com/microsoft/markitdown/issues/1276)
    - I've been using MarkItDown for conversion of some PDF files in a project I'm working on and I've noticed it performs really poorly with larger documents.
    - This is in stark contrast to other libraries like PyMuPDF and specifically its markdown variant (PyMuPDF4LLM) which in my tests performed much faster.
  - [[Feature Request] Magika Dependency Optional ](https://github.com/microsoft/markitdown/issues/1234)
    - I'm trying to use MarkItDown in the browser via Pyodide and Magika's dependency on ONNX is causing trouble.
  - https://msftmd.replit.app/
    - Powered by Microsoft MarkItDown, this tool converts various file formats to clean, structured Markdown for easy analysis and indexing.
    - https://x.com/mattppal/status/1867703377888784880
      - If you're wondering how I did this so fast, it was Agent + Assistant + deploy on Replit
- https://github.com/Michaelliv/markit /MIT/202603/ts
  - Convert anything to markdown. PDF, DOCX, PPTX, XLSX, HTML, EPUB, Jupyter, RSS, images, audio, URLs, and more. Pluggable converters, built-in LLM providers for image description and audio transcription. 
  - Works as a CLI and as a library.
  - https://x.com/micLivs/status/2037226476727140410
    - markit stays under 325ms on everything. markitdown crosses 3 seconds on a 404KB pdf.
    - 5-10x faster than markitdown. same output. better tables.
    - the gap is structural, bun vs python startup + runtime. markitdown can't close this.

- https://github.com/datalab-to/surya /19kStar/GPL/202510/python
  - https://www.datalab.to/
  - OCR, layout analysis, reading order, table recognition in 90+ languages
  - Works with PDF, images, word docs, and powerpoints
  - Our model weights use a modified AI Pubs Open Rail-M license (free for research, personal use, and startups under $2M funding/revenue) and our code is GPL. 
  - I've included a streamlit app that lets you interactively try Surya on images or PDF files. 

- https://github.com/datalab-to/marker /27.3kStar/GPLv3/202508/python
  - https://www.datalab.to/
  - Marker converts documents to markdown, JSON, chunks, and HTML quickly and accurately.
  - Converts PDF, image, PPTX, DOCX, XLSX, HTML, EPUB files in all languages
  - Does structured extraction, given a JSON schema (beta)
  - Extensible with your own formatting and logic
  - 基于 PyMuPDF 和 Tesseract OCR，支持 GPU 加速（Surya OCR 引擎），开源轻量化
  - 处理速度快（比同类快 4 倍）
  - 缺乏复杂布局解析能力，依赖本地 GPU 资源
  - Removes headers/footers/other artifacts
  - Works on GPU, CPU, or MPS
  - Optionally boost accuracy with LLMs (and your own prompt)
  - For the highest accuracy, pass the `--use_llm` flag to use an LLM alongside marker. This will do things like merge tables across pages, handle inline math, format tables properly, and extract values from forms. 
  - It can use any gemini or ollama model. 
  - [Ingesting PDFs and why Gemini 2.0 changes everything | Hacker News](https://news.ycombinator.com/item?id=42952605)
    - Marker output will be higher quality than docling output across most doc types, especially with the `--use_llm` flag. A few specific things we do differently:
    - We have hybrid mode with gemini that merges tables across pages, improves quality on forms, etc.
    - we run an ordering model, so ordering is better for docs where the PDF order is bad
    - OCR is a lot better, we train our own model, surya
    - References and links
    - Better equation conversion (soon including inline)

- https://github.com/NanoNets/docstrange /460Star/MIT/202508/python
  - https://docstrange.nanonets.com/
  - Extract and convert data from any document, images, pdfs, word doc, ppt or URL into multiple formats (Markdown, JSON, CSV, HTML) with intelligent content extraction and advanced OCR.
  - Cloud Processing (Default): Instant free conversion with cloud API 
  - Local Processing: CPU/GPU options for complete privacy - no data sent anywhere
  - 🐛 代码中未看到流式处理文件的逻辑, 对处理大文件不友好
  - Universal Input: PDFs, Word docs, Excel, PowerPoint, images, URLs, and raw text
  - URL Processing: Direct conversion from web pages
  - Smart Output: Markdown, JSON, CSV, HTML, and plain text formats
  - Advanced OCR: Multiple OCR engines with automatic fallback
  - MCP Server: Integrate with Claude Desktop for intelligent document navigation
  - [Package for converting PDF, images and docs to structured data like JSON, markdown, HTML : r/node _202509](https://www.reddit.com/r/node/comments/1nqxada/package_for_converting_pdf_images_and_docs_to/)
    - I've published a Node.js client for DocStrange 
- https://github.com/NanoNets/docext /1.8kStar/apache2/202508/python/inactive
  - An on-premises, OCR-free unstructured data extraction, markdown conversion and benchmarking toolkit

- https://github.com/yobix-ai/extractous /1.6kStar/apache2/202412/rust/inactive
  - Fast and efficient unstructured data extraction. 
  - Written in Rust with bindings for many languages.
  - Extractous offers a fast and efficient solution for extracting content and metadata from various documents types such as PDF, Word, HTML, and many other formats. 
  - Extractous is 25x faster than the popular unstructured-io library
  - 高性能非结构化数据提取工具：extractous，比unstructured-io快25倍，支持微软Office、PDF、网页、图片、电子书、邮件等多种格式
  - Extractous was born out of frustration with the need to rely on external services or APIs for content extraction from unstructured data. 
    - unstructured-io stood out as the popular and widely-used library for parsing unstructured content with in-process parsing. 
    - unstructured-io wraps around numerous heavyweight Python libraries, resulting in slow performance and high memory consumption
  - efficient solution for extracting content and metadata from various documents types such as PDF, Word, HTML, and many other formats.
  - solution in Rust with bindings for many programming languages.
  - Extractous maintains a dedicated focus on text and metadata extraction. It achieves significantly faster processing speeds and lower memory utilization through native code execution.
  - For file formats not natively supported by the Rust core, we compile the well-known Apache Tika into native shared libraries using GraalVM ahead-of-time compilation
  - Extracts text from images and scanned documents with OCR through `tesseract-ocr`.
  - 〰️ Extract a content of a file(URL/ bytes) to a `StreamReader` and perform buffered reading
- https://github.com/bzsanti/oxidizePdf /AGPL/202511/rust/NoDeps
  - A pure Rust PDF generation and manipulation library with zero external PDF dependencies.
  - Production-ready for basic PDF functionality with validated performance of 3, 000-4, 000 pages/second for realistic business documents
  - Pure Rust Core - No C dependencies for PDF operations (OCR feature requires Tesseract)
  - CJK Text Support - Chinese, Japanese, and Korean text rendering and extraction with ToUnicode CMap
  - AI/RAG Integration - Document chunking for LLM pipelines with sentence boundaries and metadata (v1.3.0+)
  - Low memory usage - Efficient streaming for large PDFs

- https://github.com/ucbepic/docetl /3.6kStar/MIT/202602/python/ts
  - https://docetl.org/
  - https://www.docetl.org/playground
  - DocETL is a tool for creating and executing data processing pipelines, especially suited for complex document processing tasks. 
  - It offers a low-code, declarative YAML interface to define LLM-powered operations on complex data.
  - DocETL is the ideal choice when you're looking to maximize correctness and output quality for complex tasks over a collection of documents or unstructured datasets.

- https://github.com/whyhow-ai/knowledge-table
  - 结构化数据提取工具，它可以以自然语言查询的方式从非结构化文档中提取结构化数据，并以表格或图表的形式展现
  - 文档数据的结构化入库，比如从合同里提取关键交易信息，然后结构化展示

- https://github.com/kreuzberg-dev/kreuzberg /3.7kStar/MIT/202601/python>rust
  - https://github.com/Goldziher/kreuzberg
  - https://kreuzberg.dev/
  - Extract text and metadata from a wide range of file formats (56+), generate embeddings and post-process at native speeds without needing a GPU.
  - Extensible architecture – Plugin system for custom OCR backends, validators, post-processors, and document extractors
  - OCR support – Tesseract (all languages via native binding), EasyOCR/PaddleOCR (Python), Guten (Node.js), extensible via plugin API
  - Memory efficient – Streaming parsers for multi-GB files
  - Embeddings Support (Optional): Kreuzberg requires ONNX Runtime version 1.22.x for embeddings. All other Kreuzberg features work without ONNX Runtime.
  - 🎯 [Announcing Kreuzberg v4 (Open Source) : r/LocalLLaMA _202601](https://www.reddit.com/r/LocalLLaMA/comments/1q9t9op/announcing_kreuzberg_v4_open_source/)
    - Rust core: Significantly faster extraction and lower memory usage. No more Python GIL bottlenecks.
    - Pandoc is gone: Native Rust parsers for all formats. 
    - Plugin system: Register custom document extractors, swap OCR backends (Tesseract, EasyOCR, PaddleOCR), add post-processors for cleaning/normalization, and hook in validators for content verification.
    - ML pipeline features: ONNX embeddings on CPU (requires ONNX Runtime 1.22.x), streaming parsers for large docs, batch processing, byte-accurate offsets for chunking.
    - `LibreOffice` is optional and only used for a small subset of legacy/edge formats. For common formats like PDF, DOCX, HTML, email, etc., Kreuzberg uses native Rust parsers and doesn’t require LibreOffice. 
    - Any Docling integration?
      - Not directly- they overlap some but are separate projects. Kreuzberg is x50 times faster than docling on a CPU (not suprising, since docling is GPU orientated). Docling is better in terms of complex layout extraction. 
# ocr-solutions/vendors
- https://github.com/PaddlePaddle/PaddleOCR /66.5kStar/apache2/202512/python/cpp
  - https://www.paddleocr.ai/
  - 2025年5月20日，飞桨团队发布PaddleOCR 3.0，支持多文字类型识别和手写体识别，满足大模型应用对复杂文档高精度解析的旺盛需求，并新增对昆仑芯、昇腾等国产硬件的支持。
  - 2025 年 10 月 16 日，PaddleOCR 开源了先进、高效的文档解析模型 PaddleOCR-VL，其核心组件为 PaddleOCR-VL-0.9B, 由 NaViT 风格的动态分辨率视觉编码器与 ERNIE-4.5-0.3B 语言模型组成，能够实现精准的元素识别
  - PaddleOCR-VL - 通过 0.9B 超紧凑视觉语言模型增强多语种文档解析
  - PP-OCRv5 — 全场景文字识别, 单模型支持五种文字类型（简中、繁中、英文、日文及拼音）
  - PP-StructureV3 — 将复杂PDF和文档图像智能转换为保留原始结构的Markdown文件和JSON文件
  - PP-ChatOCRv4 — 原生集成ERNIE 4.5，从海量文档中精准提取关键信息
  - [Awesome projects based on PaddleOCR](https://github.com/PaddlePaddle/PaddleOCR/blob/main/awesome_projects.md)
  - https://github.com/PaddlePaddle/PaddleX /5.9kStar/apache2/202512/python/cpp
    - https://paddlepaddle.github.io/PaddleX/
    - PaddleX 3.0 是基于飞桨框架构建的低代码开发工具，它集成了众多开箱即用的预训练模型，可以实现模型从训练到推理的全流程开发，支持国内外多款主流硬件

- https://github.com/opendatalab/MinerU /44.2kStar/AGPLv3/202509/python
  - https://opendatalab.github.io/MinerU/
  - 一站式开源高质量数据提取工具，将PDF转换成Markdown和JSON格式
  - Magic-PDF 是一款将 PDF 转化为 markdown 格式的工具。支持转换本地文档或者位于支持S3协议对象存储上的文件。
  - Magic-Doc 是一款支持将网页或多格式电子书转换为 markdown 格式的工具。
    - 支持176种语言的准确识别
  - 集成 LayoutLMv3、YOLOv8 等模型，支持多模态解析（表格/公式/图像）
  - 支持 API 和图形界面
  - 依赖 GPU，表格处理速度较慢，配置复杂
  - MinerU2.5: currently the most powerful multimodal large model for document parsing. With only 1.2B parameters
  - Output text in human-readable order, suitable for single-column, multi-column, and complex layouts.
  - Extract images, image descriptions, tables, table titles, and footnotes.
  - Automatically recognize and convert formulas in the document to LaTeX format.
  - Automatically recognize and convert tables in the document to HTML format.
  - Automatically detect scanned PDFs and garbled PDFs and enable OCR functionality.
  - Remove headers, footers, footnotes, page numbers, etc., to ensure semantic coherence
  - Supports running in a pure CPU environment, and also supports GPU(CUDA)/NPU(CANN)/MPS acceleration
  - Compatible with Windows, Linux, and Mac platforms
  - https://huggingface.co/spaces/opendatalab/MinerU
  - [Connect to the local LLM接入本地大语言模型 _202503](https://github.com/opendatalab/MinerU/issues/1976)
    - 教程没写就只是预留字段而已，有想做成llm方向的想法
  - [issue: MinerU not working in vllm mode ](https://github.com/open-webui/open-webui/discussions/18446)
    - Its not in the code yet, the only options are vlm and pipeline

- https://github.com/RapidAI/RapidDoc /apache2/202512/python/非VLM
  - RapidDoc 是一个轻量级、专注于文档解析的开源框架，支持 OCR、版面分析、公式识别、表格识别和阅读顺序恢复 等多种功能。
  - 框架基于 `Mineru` 二次开发，移除 VLM，专注于 Pipeline 产线下的高效文档解析，在 CPU 上也能保持不错的解析速度。
  - 基于 MinerU 改造而来，已移除原项目中的 YOLO 模型，并替换为 PP-StructureV3 系列 ONNX 模型。 由于已移除 AGPL 授权的 YOLO 模型部分，本项目整体不再受 AGPL 约束。
  - 项目所使用的核心模型主要来源于 PaddleOCR 的 PP-StructureV3 系列（OCR、版面分析、公式识别、阅读顺序恢复，以及部分表格识别模型），并已全部转换为 ONNX 格式，支持在 CPU/GPU 上高效推理。
  - 基于gradio开发的webui，界面简洁，仅包含核心解析功能，免登录
  - [MinerU商业化二开 _202505](https://linux.do/t/topic/640019)
    - 官方版本问题：包含禁止非商业的排序模型layoutreader，
    - 使用规则排序替换排序模型layoutreader
    - 优化Dockerfile（在项目根目录下）：集成libreoffice到容器，支持直接解析docx、ppt等文件
    - 解决libreoffice转码和MinerU识别中文乱码问题
    - 使用fastapi开发了api服务，部署后无需再次做接口开发（在web_service目录下）

- https://github.com/tesseract-ocr/tesseract /71.5kStar/apache2/202512/cpp
  - https://tesseract-ocr.github.io/
  - Tesseract Open Source OCR Engine
  - Tesseract has unicode (UTF-8) support, and can recognize more than 100 languages "out of the box".
  - Tesseract supports various image formats including PNG, JPEG and TIFF.
  - Tesseract supports various output formats: plain text, hOCR (HTML), PDF, invisible-text-only PDF, TSV, ALTO and PAGE.
  - Tesseract was originally developed at Hewlett-Packard Laboratories Bristol UK in 1985. From 2006 until August 2017 it was developed by Google.

- https://github.com/ocrmypdf/OCRmyPDF /32kStar/MPLv2/202512/python
  - http://ocrmypdf.readthedocs.io/
  - OCRmyPDF adds an OCR text layer to scanned PDF files, allowing them to be searched or copy-pasted.
  - Generates a searchable PDF/A file from a regular PDF
  - Distributes work across all available CPU cores
  - Uses `Tesseract` OCR engine to recognize more than 100 languages
  - Battle-tested on millions of PDFs.
  - https://ocrmypdf.readthedocs.io/en/latest/advanced.html
    - OCRmyPDF supports two PDF rasterizers: pypdfium2(Faster), Ghostscript(system binary)
    - OCRmyPDF uses PDF renderers to create the invisible text layer. `fpdf2` renderer (default);  `sandwich` renderer uses Tesseract’s text-only PDF feature;  The hocr and hocrdebug renderer options are deprecated and automatically redirect to fpdf2.
  - 🆚 PyTesseract has more features don’t particularly need PDF output, but less features than OCRmyPDF’s API for creating PDFs.
  - 🤔 [Proposal: Improve OCR Accuracy with LLM-based Post-processing _202503](https://github.com/ocrmypdf/OCRmyPDF/issues/1491)
    - OCRmyPDF and Tesseract work well, but they sometimes produce errors, especially when processing complex fonts, handwritten text, or low-quality scans. One potential way to improve OCR accuracy is by integrating a post-processing step using a Large Language Model (LLM) such as GPT-4, Llama, or Claude.
    - I don't think this would be a good idea or very practical. A better OCR engine based on LLM or recent ML would improve results more than post processing since it can actually read the input text more accuracy, as opposed to guessing what bad output text might mean from the text alone. There's no obvious way to correct positional information when the word count differs after correction and it will.
    - The easiest thing to do at this point is use ocrmypdf and then a tool like pdftotext to get the recognized text out. You could then feed this to an LLM to improve the output text (in many cases) without positional information
  - [[Feature]: use local (small) vision llm for higer OCR accuracy _202504](https://github.com/ocrmypdf/OCRmyPDF/issues/1517)
    - Taking Qwen2.5-VL as an example, it is trained to output "Qwen HTML" format, with bounding box coordinates added to each HTML tag. 
  - [Saving the images ocrmypdf temporarily creates OR use existing pdf-to-img pdfs _202501](https://github.com/ocrmypdf/OCRmyPDF/discussions/1457)
    - I currently have an OCR workflow that uses Surya OCR for ocring and table recognition and generating text files and CSVs from scanned semi-technical PDF documents. These outputs are then fed into an LLM data extraction tool. While Surya performs well, it doesn't create searchable PDFs. To address this, I run OCRmyPDF on the original PDF as a final step to generate a searchable PDF.
    - However, I've noticed an inefficiency in this approach since both Surya OCR and OCRmyPDF perform PDF to image conversion and preprocessing. 
    - The goal is to perform the PDF to image conversion only once throughout the entire workflow.
    - You could create a OCRmyPDF plugin that uses Surya as its OCR engine instead of Tesseract for example. There's an `OCRmyPDF-EasyOCR` that demonstrates how this could be done (although the more current approach would be to render to hOCR).
  - https://github.com/clefru/ocrmypdf-paddleocr /MPL/202603/python
    - A PaddleOCR plugin for OCRmyPDF, enabling the use of PaddleOCR as an alternative OCR engine to Tesseract.
    - Optimized bounding boxes for accurate text selection in PDF output
    - Maps OCRmyPDF/Tesseract language codes to PaddleOCR codes
    - Converts PaddleOCR output to hOCR format for OCRmyPDF to overlay on PDFs, which OCRmyPDF uses to create a searchable PDF.
    - The plugin uses PaddleOCR 3.x's native return_word_box=True parameter to get accurate word-level bounding boxes directly from the OCR engine
    - [feat: add PaddleOCR-VL engine support via --paddle-engine vl · clefru/ocrmypdf-paddleocr@46fd027 _202603](https://github.com/clefru/ocrmypdf-paddleocr/commit/46fd027feb69de08ab831be27e337f97086ff2f0)
      - Adds a second OCR engine backed by the PaddleOCR-VL 0.9B VLM
  - https://github.com/ocrmypdf/OCRmyPDF-EasyOCR /MIT/python
    - This is plugin to run OCRmyPDF with the EasyOCR engine instead of Tesseract OCR, the default OCR engine for OCRmyPDF. 
  - [OCRmyPDF: Add an OCR text layer to scanned PDF file | Hacker News _202207](https://news.ycombinator.com/item?id=32028752)
    - LibreOffice has a cool option where you can generate the PDF with the editable text format embedded. You get a clean PDF that is also fully editable. Easy tech, but also useful.

- https://github.com/FanQinFred/OCRmyPDF-Desktop /apache2/202312/js/vue/inactive
  - 在OCRmyPDF的基础上，集成了所需环境，并使用Electron开发了桌面端
  - https://github.com/razem-io/OCRmyPDFonWEB /MIT/202305/python/inactive
    - Streamlit Web UI for OCRmyPDF
    - https://github.com/mghulamqadir/scanned-to-searchable-pdf /Streamlit
  - https://github.com/digidigital/OCRthyPDF-Essentials /AGPL/202407/python/inactive
    - Make your PDF files text-searchable (A GUI for OCRmyPDF)
  - https://github.com/denovochen/OCRmyPDF-GUI /MPL/202506/python/qt
    - 一个图形用户界面，让OCRmyPDF命令行工具的强大功能变得简单易用
    - 批量处理：一次处理多个PDF文件，并显示详细进度
    - 高级OCR选项：自动校正倾斜页面、自动旋转、清理图像等
    - OCRmyPDF, Tesseract OCR, PySide6 (Qt for Python)
  - https://github.com/alexanderlanganke/ocrmypdfgui /MIT/202506/python
    - GUI wrapper to run batch jobs on my filesystem
  - https://github.com/piazin/ocrmypdf-js /ts
    - For everything to work correctly, you need to have it installed on your OS ocrmypdf.

- https://github.com/naptha/tesseract.js /37.6kStar/apache2/202512/js
  - https://tesseract.projectnaptha.com/
  - Pure Javascript OCR for more than 100 Languages
  - Tesseract.js aims to bring the Tesseract OCR engine (a separate project) to the browser and Node.js, and works by wrapping a WebAssembly port of Tesseract.
  - Tesseract.js does not support PDF files and does not modify the Tesseract recognition model to improve accuracy.
  - Scribe.js is an alternative library created to accommodate common feature requests that are outside of the scope of this repo. 
- https://github.com/scribeocr/scribe.js /234Star/AGPL/202512/js
  - a JavaScript library that performs OCR and extracts text from images and PDFs.
  - Scribe.js includes improvements to the Tesseract recognition model and supports extracting text from PDF documents
  - https://github.com/scribeocr/scribeocr /728Star/AGPL/202512/js
    - https://scribeocr.com/
    - Web interface for recognizing text, proofreading OCR, and creating fully-digitized documents
    - a free (libre) web application for recognizing text from images, proofreading OCR data, and creating fully-digitized documents
    - This repo only contains code for the user interface. Recognition is run using the Scribe.js library
    - 实测识别后的文档仍是`<canvas>`元素, 点击识别后的文本时, 仅点击处的文本会显示为`<span>`.
    - To allow for efficient proofreading, Scribe OCR precisely prints editable OCR text over source images.
      - 绿色代表识别高正确性, 黄色代表校对警告, 红色代表低正确性

- https://github.com/deepseek-ai/DeepSeek-OCR /21.5kStar/MIT/202510/python
  - [DeepSeek-OCR: Contexts Optical Compression | Abstract](https://arxiv.org/abs/2510.18234)

- https://github.com/rednote-hilab/dots.ocr /5.9kStar/MIT/202512/python/mdl-1.7b
  - https://dotsocr.xiaohongshu.com/
  - dots.ocr is a powerful, multilingual document parser that unifies layout detection and content recognition within a single vision-language model while maintaining good reading order.
  - Multilingual Support: dots.ocr demonstrates robust parsing capabilities for low-resource languages, achieving decisive advantages across both layout detection and content recognition on our in-house multilingual documents benchmark.
  - Unified and Simple Architecture: By leveraging a single vision-language model, dots.ocr offers a significantly more streamlined architecture than conventional methods that rely on complex, multi-model pipelines. 
    - Switching between tasks is accomplished simply by altering the input prompt, proving that a VLM can achieve competitive detection results compared to traditional detection models like DocLayout-YOLO.

- https://github.com/JaidedAI/EasyOCR /28.6kStar/apache2/202409/python/cpp/inactive
  - https://www.jaided.ai/
  - Ready-to-use OCR with 80+ supported languages and all popular writing scripts including: Latin, Chinese, Arabic, Devanagari, Cyrillic, etc.
  - In case you do not have a GPU, or your GPU has low memory, you can run the model in CPU-only mode by adding gpu=False.

- https://github.com/junhoyeo/BetterOCR /597Star/MIT/202311/python/inactive
  - Better text detection by combining multiple OCR engines with LLM.
  - OCR Engines Currently supports EasyOCR (JaidedAI), Tesseract (Google), and Pororo (KakaoBrain).
  - [Show HN: BetterOCR combines and corrects multiple OCR engines with an LLM | Hacker News _202310](https://news.ycombinator.com/item?id=38048228)

- https://github.com/wolfmanstout/screen-ocr /apache2/202510/python
  - screen-ocr package makes it easy to perform OCR on portions of the screen
  - WinRT is a Windows-only backend that is very fast and reasonably accurate.
  - Tesseract is a cross-platform backend that is much slower and slightly less accurate than WinRT
  - EasyOCR is a very accurate but slow backend and only runs on Python 64-bit

- https://github.com/breezedeus/Pix2Text /2.7kStar/MIT/202507/python/inactive/华人作者
  - https://p2t.breezedeus.com/
  - Pix2Text (P2T) aims to be a free and open-source Python alternative to Mathpix
  - Open-Source Python3 tool with SMALL models for recognizing layouts, tables, math formulas (LaTeX), and text in images, converting them into Markdown format.
  - Text Recognition Engine: Supports 80+ languages such as English, Simplified Chinese, Traditional Chinese, Vietnamese, etc. For
    - English and Simplified Chinese recognition, it uses the open-source OCR tool `CnOCR`, while for other languages, it uses the open-source OCR tool `EasyOCR`.

- https://github.com/Rayyan9477/ocr-app /202511/ts
  - OCR platform that combines multiple engines, AI enhancement, and HIPAA-compliant security to deliver exceptional document processing.
  - Our platform employs specialized OCR engines working in parallel:
    - OCRmyPDF: Industrial-strength PDF processing
    - Enhanced Tesseract: Optimized for various document types
    - Intelligent Orchestrator: Automatic engine selection
    - AI Enhancement: Machine learning-powered accuracy improvements
  - HIPAA Compliance	End-to-end encryption, audit logs

- https://github.com/TurkuNLP/ocr-postcorrection-lm /202510/python
  - Code to try out ocr postcorrection with language models
  - [OCR Error Post-Correction with LLMs in Historical Documents: No Free Lunches](https://arxiv.org/abs/2502.01205v1)
  - https://github.com/Shef-AIRE/llms_post-ocr_correction /202406/python
    - This repository contains the code for the paper Leveraging LLMs for Post-OCR Correction of Historical Newspapers, where LLMs are adapted for a prompt-based approach to post-OCR correction.
  - https://github.com/savi8sant8s/ptbr-post-ocr-sc-llm /MIT/202501/python
    - A proposal for post-OCR spelling correction using Language Models

- https://github.com/vlm-run/vlmrun-hub /537Star/apache2/202512/python
  - https://docs.vlm.run/hub
  - VLM Run Hub, a comprehensive repository of pre-defined Pydantic schemas for extracting structured data from unstructured visual domains such as images, videos, and documents. 
  - 似乎未开源代码，但pip包安装后可本地运行
# pdf-utils
- https://github.com/py-pdf/pypdf /9.6kStar/BSD/202511/python
  - https://pypdf.readthedocs.io/en/latest/
  - A pure-python PDF library capable of splitting, merging, cropping, and transforming the pages of PDF files
  - It can also add custom data, viewing options, and passwords to PDF files. 
  - pypdf can retrieve text and metadata from PDFs as well.
  - [Reading the PDF metadata on large files _202507](https://github.com/py-pdf/pypdf/discussions/3390)
    - Is there a way to get the PDF attributes like Creation Date without loading the whole file into memory? We have large multi-gigabyte files and are trying to process them on a fleet of smaller ECS instances. The streaming features of pypdf have been great, but would love to get the same metadata without loading the whole file into memory.
    - Have you tried to pass a buffered file stream as stream argument ?
  - [Implementation of get_contents ](https://github.com/py-pdf/pypdf/discussions/3352)
    - `get_data()` is accessing the (decoded) byte data of the corresponding content stream, thus this only relevant when reading from the original PDF file.
    - skimming through the usages of self.pdf in ContentStream seems to indicate that this is used to avoid cloning if the content streams are both targeting the same PDF reference

- https://github.com/pdfminer/pdfminer.six /6.8kStar/MIT/202511/python
  - https://pdfminersix.readthedocs.io/
  - Community maintained fork of pdfminer
  - a tool for extracting information from PDF documents. It focuses on getting and analyzing text data. 
  - Pdfminer.six extracts the text from a page directly from the sourcecode of the PDF. 
  - It can also be used to get the exact location, font or color of the text.
  - It is built in a modular way such that each component of pdfminer.six can be replaced easily. You can implement your own interpreter or rendering device that uses the power of pdfminer.six for other purposes than text analysis.
  - Written entirely in Python.
  - Support for PDF-1.7 specification (well, almost).
  - Support for CJK languages and vertical writing.
  - Automatic layout analysis.
  - [For optimization of extracting text page by page  ](https://github.com/pdfminer/pdfminer.six/issues/533)
    - I get that using `StringIO` is a bit cumbersome. But using input and output streams in the way it was setup and its difficult to change. Anyway, besides being cumbersome it doesn't give any performance penalty.
  - https://github.com/euske/pdfminer /MIT/202001/archived
- https://github.com/dhdaines/playa /MIT/202511/python
  - The purpose of PLAYA is to provide a robust, efficent, parallel and parallelizable, pure-Python and Pythonic (for its author's definition of the term), lazy interface to the internals of PDF files.
  - PLAYA allows you to take advantage of multiple CPUs. This parallelism currently operates at the page level since this is the most logical way to split up a PDF
  - [Playa PDF: A strong pdfminer successor : r/Python](https://www.reddit.com/r/Python/comments/1jfk466/playa_pdf_a_strong_pdfminer_successor/)
  - This library is similar in scope to pdfminer and its fork pdfminer.six
  - It handles a broader range of PDFs and PDF issues, being very close to the (horrible) specification. For example, the author of the library (dhaines) has recently added an enormous test suite from PDF.js
  - it is faster than the other Python libs by a factor of at least two, if not three, and not only when parallelizing.
  - complete metadata extraction - this part is what got me into this since I am integrating this with Kreuzberg now 
  - It uses modern and full-type hints and exports, proper dataclasses.
  - https://github.com/dhdaines/paves /MIT/202511/python
    - PLAYA is intended to get objects out of PDF, with no dependencies or further analysis. 
    - The primary goal of PLAYA-PDF is to give access to all the objects and particularly the metadata in a PDF. 
    - One goal of PAVÉS (because there are a few) is to give an easy way to visualise these objects and metadata.

- https://github.com/jsvine/pdfplumber /9.2kStar/MIT/202511/python 
  - Plumb a PDF for detailed information about each text character, rectangle, and line. Plus: Table extraction and visual debugging.
  - Works best on machine-generated, rather than scanned, PDFs. 
  - Built on pdfminer.six.

- https://github.com/datalab-to/pdftext /644Star/apache2/202506/python
  - Text extraction like `PyMuPDF`, but without the AGPL license. PDFText extracts plain text or structured blocks and lines. 
  - It's built on `pypdfium2`, so it's fast, accurate, and Apache licensed.
  - It first uses pypdfium2 to extract characters in order, along with font and other information. Then it uses a simple decision tree algorithm to group characters into lines and blocks. It does some simple postprocessing to clean up the text.
  - built on some amazing open source work, including:  pypdfium2, scikit-learn
# web-etl/crawling
- https://github.com/mendableai/firecrawl /AGPLv3/202502/python/rust/ts
  - https://firecrawl.dev/
  - Turn entire websites into LLM-ready markdown or structured data. 
  - Scrape, crawl and extract with a single API.
  - The hard stuff: proxies, anti-bot mechanisms, dynamic content (js-rendered), output parsing, orchestration
  - Batching (New): scrape thousands of URLs at the same time with a new async endpoint.
  - open-version: scrape, extract, map, formats, sdk
  - cloud-version: anti-bot, dashboard, actions, browserless, enterprise
  - This project is primarily licensed under AGPLv3
    - However, certain components of this project are licensed under the MIT 
    - The SDKs and some UI components are licensed under the MIT License. 
- https://github.com/OpenAISpace/ai-trend-publish /MIT/202502/ts
  - 一个基于 AI 的趋势发现和内容发布系统，支持多源数据采集、智能总结和自动发布到微信公众号
  - 多源数据采集: Twitter/X, 网站内容抓取 (基于 FireCrawl)
  - 使用 DeepseekAI 进行内容总结
  - 定时发布任务
  - 定时任务: node-cron
  - 模板引擎: EJS

- https://github.com/Dicklesworthstone/markdown_web_browser /MIT/202604/python
  - Transform any website into clean, proveable Markdown with full OCR accuracy
  - Render any URL with headless Chrome-for-Testing, tile screenshots into OCR-friendly slices, and stream structured Markdown + provenance back to AI agents, web apps, and automation pipelines.
  - Two ways to use it:
    - Browser UI  http://localhost:8000/browser
    - CLI + API - Programmatic capture for automation, batch processing
  - Backend captures page as tiled screenshots via headless Chrome
    - `Playwright` (Chromium CfT, viewport 1280×2000, DPR 2, reduced motion) performs a deterministic viewport sweep.
    - `pyvips` slices sweeps into ≤1288 px tiles with ≈120 px overlap; each tile carries offsets, DPR, hashes.
  - OCR extracts text from each tile with 95%+ accuracy
    - The OCR client submits tiles (HTTP/2) to hosted or local `olmOCR`, with retries + concurrency
    - Stitcher merges Markdown, aligns headings with the DOM outline, trims overlaps via SSIM + fuzzy text comparisons
  - Real-time Progress: Live tile processing updates with progress bars

- https://github.com/getmaxun/maxun /AGPL/202503/ts
  - https://www.maxun.dev/
  - Open-source no-code web data extraction platform. 
  - Maxun lets you create custom robots which emulate user actions and extract data. A robot can perform any of the actions: Capture List, Capture Text or Capture Screenshot. Once a robot is created, it will keep extracting data for you without manual intervention
  - BYOP (Bring Your Own Proxy) lets you connect external proxies to bypass anti-bot protection. Currently, the proxies are per user. Soon you'll be able to configure proxy per robot.
# tesseract
- https://github.com/atorhub/anj-dual-ocr-parser /202512/js
  - https://atorhub.github.io/anj-dual-ocr-parser/
  - Advanced client-side invoice OCR, parsing, export, and history system — powered entirely by browser technologies, no backend required.
  - ANJ Dual OCR Parser — AI-powered invoice/bill extractor featuring dual-pass OCR (quick + enhanced), smart parsing, automatic field detection, and multi-format export (JSON, CSV, XLSX, PDF, ZIP)
  - Tesseract.js, IndexedDB, html2canvas, jsPDF
  - If Image → processed with Tesseract.js

- https://github.com/hertzg/tesseract-server /MIT/202406/ts/inactive
  - lightweight HTTP server that converts photos, images and scanned documents to text using optical character recognition by utilizing the power of Google Tesseract.
  - The service provides configurations as cli options.
  - https://github.com/antonioanerao/ocr_pdf_api /MIT

- https://github.com/CogStack/ocr-service /elastic/202512/python
  - a python fast-api OCR service, attempting to resolve scalability and performance issues. 
  - This is a python-replacement of the previous Tika-service in an attempt to resolve scalability and performance issues. It also relies on tesseract ocr but without the ambiguities of the Tika framework.
  - Windows: this project can and should be run inside WSL (preferabily ubuntu) 
  - 🔀 This service is fast but it is resource intensive, and will attempt to use all cores on your machine. You can spin up multiple docker services in the hopes of having multiple requests handled at the same time.
  - limitations: You will notice that requests are handled sequentially rather than in parallel (one at a time), this is partly due to using libreoffice/soffice binary package (this is likely to change in the future) to convert most documents to a common format
    - Because this background application does not handle parallelisation very well it is recommended to have multiple docker services running instead OR you can spin up multiple workers via the OCR_WEB_SERVICE_WORKERS variable
    - Another cause for sequential request processing is the sharing of resources, one thread has access by default to all cores, this matters because the current implementation splits a document into multiple pages and attempts to ocr each page on a separate core, resulting in good speed but a competition for resources.
  - https://github.com/CogStack/tika-service /java/inactive
    - This project implements Apache Tika running as a web service using Spring Boot. 
    - It exposes a REST API so that a client can send a document in binary format and receive back the extracted text.

- https://github.com/SteveKhoa/ocr-api-backend /202405/python/inactive
  - A containerized web service for Optical Character Recognition.
  - Built with FastAPI, SQLite, Google Tesseract OCR Engine, and Docker.
  - Improved accuracy from baseline Tesseract with DBScan clustering algorithm.
  - Base64-encoded images for interoperability.

- https://github.com/LiveWithCodeAnkit/AI-OCR /202501/python
  - Advanced AI-OCR with FastAPI and OpenAI Integration
  - It leverages powerful image processing libraries such as OpenCV, Pillow (PIL), and `pytesseract` to extract accurate text from images and PDFs
  - Multi-File Support: Upload and process multiple images or PDFs simultaneously.
  - Automatically detect and fix image rotation and skewness.
  - Intelligent text formatting and validation using OpenAI APIs.
  - https://github.com/lifeiswilde/textract-ai
    - extracts text from PDF files, processes the extracted text using the OpenAI API, and generates a final processed document. 
    - Converts PDF files to images using pdf2image
    - Extracts text from images using pytesseract

- https://github.com/robertknight/tesseract-wasm /349Star/BSD/202510/ts/wasm
  - https://robertknight.github.io/tesseract-wasm/
  - A WebAssembly build of the Tesseract OCR engine for use in the browser and Node.
  - Using WebAssembly SIMD when available (Chrome >= 91, Firefox >= 90, Safari >= 16.4) to improve text recognition performance.
  - 在线示例可输出 文本 和 hocr的html

- https://github.com/bhimrazy/receipt-ocr /MIT/202601/python
  - An efficient OCR engine for receipt image processing.
  - featuring both a dedicated Tesseract OCR module and a general receipt processing package using LLMs

- https://github.com/manisandro/gImageReader /GPL/202601/cpp
  - a simple Gtk/Qt front-end to tesseract-ocr.
  - Import PDF documents and images from disk, scanning devices, clipboard and screenshots
  - Process multiple images and documents in one go
  - Recognize to plain text or to hOCR documents
  - Generate PDF documents from hOCR documents
  - 支持win/linux, 不支持mac

## utils

- https://github.com/asottile/tessdata /MIT/202604/python
  - pip installable versions of tesseract-ocr data
# paddleocr
- https://github.com/majcheradam/ocrbase /MIT/202601/ts
  - Turn PDFs into structured data at scale. 
  - Real-time WebSocket updates.
  - PaddleOCR-VL-0.9B for accurate text extraction
  - Structured extraction - Define schemas, get JSON back
  - Built for scale - Queue-based processing for thousands of documents
  - WebSocket notifications for job progress
# mineru
- https://github.com/zt6453928/ailat-translation /MIT/202601/python/js
  - https://mineru.net/apiManage/docs
  - AI-Powered Document Translation Tool
  - A web-based PDF document parsing and translation tool that supports intelligent document parsing, multi-language translation, and various export formats.
  - Supports PDF, DOCX and other document formats, extracts text, images, tables, and formulas
  - Export to PDF, Markdown, HTML, DOCX, JSON, LaTeX
  - Multiple Translation Engines: Supports DeepLX and OpenAI-compatible APIs
  - Real-time Preview: Side-by-side comparison of original and translated content
  - 🛝
    - 采用 vlm 方案
    - pdf原文件上传后保存在 `outputs/<task_id>/original.pdf` .
    - mineru解析后的文本内容仅在memory, 未持久化
  - [开源一个支持多格式文档翻译应用 ](https://linux.do/t/topic/1511535)
    - 出于身边同学对论文翻译的需求，所以开发了这个项目，除了论文我也用来对一些AI教程文档进行翻译
    - 灵感来自于MinerU, PDF格式还支持对照翻译

- https://github.com/ZiChuanLan/PDF2PPT /MIT/202603/python/ts
  - https://ppt.015201314.xyz/
  - 将扫描版 PDF、课件截图和图片型文档转换为尽量高保真、尽量可编辑的 PPTX。
  - PDF2PPT 的目标不是“把 PDF 贴进 PPT”，而是尽量把页面重建为可编辑文本、独立图片区域和页面底图，在保留原稿观感的同时提高后续编辑能力。
  - 不只是截图式导出，而是尽量把页面重建为文本层、图片块和页面底图
  - 不只适合单机试用，也适合部署成 Web、API、Worker 的完整服务
  - 可以在本地 OCR、远程 OCR 和文档解析链路之间切换
    - 支持本地 OCR、远程 OCR、百度文档解析、MinerU 等多种链路
  - [【开源】PDF2PPT: 将PDF转为可编辑的PPT。支持MCP的调用，支持OPENAI兼容VLM视觉模型，MINERU，百度AI和本地OCR。支持页脚清除，图片可编辑等功能。 - 开发调优 - LINUX DO _202603](https://linux.do/t/topic/1840954)
    - 允许自定义提示词让AI（deepseek-ocr）直出bbox和文字
  - limitations
    - 本地OCR中的Paddleocr未测验，可能有BUG。
    - Mineru由于远程额度够用，故没在本地OCR中加入。
    - 不支持批量

- https://github.com/blacksamuraiiii/pdf2ppt /MIT/202601/python
  - 将 AI 生成的 PDF 文稿（如 Google NotebookLM 导出的内容）或其他标准 PDF 文档，通过智能解析转换为可编辑的 PowerPoint (PPTX) 演示文稿。
  - 提供 基于 CustomTkinter 的现代化界面 (app.py) 和 cli
  - 每个元素都带有精确的边界框坐标 [x1, y1, x2, y2]
  - 支持中英文混排识别
  - Area-based 字号算法: 根据 bbox 面积和字符密度自动计算最佳字号
  - Layout.json 多源解析: 同时利用 layout.json 和 content_list.json，提取 image_caption 的精确 bbox
  - [基于MinerU的pdf转ppt工具（更新v0.3，加入去水印） _202601](https://linux.do/t/topic/1490727)
    - 基于MinerU强大的解析能力，将文字、图片、表格按照位置进行解析重组，字体大小根据Area-based放缩，让Antigravity改了几稿，做了一个简单的GUI页面
    - 加了一个去右下角水印的选项

- https://github.com/lpdswing/mineru-web /AGPL/202601/python/ts/vue
  - 提供文档解析、信息提取和智能分析功能。
  - 采用前后端分离架构，结合容器化技术，为用户提供高效、可靠的文档处理解决方案。
  - 基于 FastAPI 和 Vue 3 构建, Element Plus
  - 支持 PDF、Word、Excel 等多种文档格式的处理
  - 采用异步任务队列，支持大规模文档并发处理
  - 支持 NVIDIA GPU 和华为昇腾 NPU
  - [[开源]Mineru-web，为mineru打造的ui界面 _202511](https://linux.do/t/topic/1115235)
    - 项目最开始的目的是为了在私有环境给非开发人员使用，提高工作效率。按最开始官方版本的UI界面复刻的
    - pdf预览用的浏览器的功能，理论不卡
    - 图片直接解析并存储到minio

## utils

- https://github.com/frondesce/mineru-kb-packager /python
  - Post-process a MinerU extraction directory into a retrieval-ready knowledge base dataset for RAG pipelines.
  - [开源：MinerU → RAG 数据集转换工具 - LINUX DO _202604](https://linux.do/t/topic/1940345)
    - MinerU 自身的输出格式很标准，但有一些标记和符号对于 RAG 模型来说反而是噪声。
# ocr-examples
- https://github.com/AKSarav/pdfstract /108Star/apache2/202601/python/js
  - The Extraction and Chunking Layer in Your RAG Pipeline - Available as CLI - WEBUI - API
  - Extract structured text, tables, and metadata from PDFs using various libraries (PyMuPDF4LLM, MarkItDown, Marker, Docling, PaddleOCR, DeepSeek-OCR, Tesseract, MinerU, Unstructured, and more)
  - Chunk the text into smaller chunks using various libraries (Token, Sentence, Recursive, Table, Semantic, Code, Late, Neural, Slumber, and more)
    - 10+ chunking methods powered by `Chonkie`.
  - Embed the chunks using various libraries (Sentence Transformers, OpenAI, etc.)
  - Multiple Output Formats: Markdown, JSON, and Plain Text
  - On-Demand Model Downloads: Download ML models only when needed
  - Batch Processing: Parallel conversion of 100+ PDFs with detailed reporting
  - 依赖fastapi、Chonkie、PyMuPDF, Marker, Docling
  - 🆚 [Built a small tool to compare PDF → Markdown libraries (for RAG / LLM workflows) : r/Rag _202507](https://www.reddit.com/r/Rag/comments/1m1j10e/built_a_small_tool_to_compare_pdf_markdown/)
    - I’ve been exploring different libraries for converting PDFs to Markdown to use in a Retrieval-Augmented Generation (RAG) setup.
    - But testing each library turned out to be quite a hassle — environment setup, dependencies, version conflicts, etc.
    - Currently, it supports: docling pymupdf4llm markitdown marker

- https://github.com/readur/readur /547Star/MIT/202601/rust/ts/Axum
  - Quick, painless, intuitive OCR platform written in Rust and TypeScript. 
  - Tesseract OCR for text extraction
  - Axum for the web framework
  - Drag-and-drop support for PDF, images, text files, and Office documents (DOCX, XLSX, DOC*)
  - Automatic text extraction using Tesseract and Office document parsing
  - WebDAV, Local Folders, and S3-compatible storage integration
  - Beautiful React frontend with Material-UI components and responsive design
  - Document tagging and categorization
  - OIDC Setup - Single Sign-On integration

- https://github.com/fabriziosalmi/pdf-ocr /MIT/202602/python/inactive
  - web-based application built with Flask to convert PDF documents into editable formats (DOCX, TXT, Markdown, HTML) using Optical Character Recognition (OCR).
  - 支持image preprocessing
  - ocr支持tesseract/EasyOCR/pyocr
  - Poppler PDF Rendering Library

- https://github.com/tmzncty/dots_ocr_suite /202512/python/js
  - 一个基于 DotsOCR 库开发的 OCR（光学字符识别）处理工具箱，包含 PDF 转 Word (DOCX) 的完整应用。
  - PDF 转 DOCX 转换器 (完整版): 自动进行拆图、OCR 识别、版面分析, 
    - 利用多核 CPU 并行处理，大幅提升长文档的转换速度,
    - 实时进度：清晰展示拆图、识别、生成的每一个步骤进度, 
    - 支持下载 Word 文档 (.docx) 或包含 Markdown、JSON 数据的 ZIP 压缩包
  - 在“批量处理”标签页，您可以一次性拖入多个 PDF 文件。 自动排队：文件会自动进入队列逐个处理。您可以在下方列表中查看每个文件的实时进度
  - 文件名为 openai_test_tool.py。这是一个专用于内网多后端 API 调试与性能对比的工具。
    - 支持对多个 OpenAI 兼容接口（如 vLLM, LocalAI）同时发起并发请求。
    - Vision 支持：内置图片转 Base64 功能，方便测试 GPT-4 Vision 等多模态接口。
  - 本项目默认连接的 OCR 后端地址为 192.168.24.78:8000。 如果你有自己的 OCR 服务器，或者后端地址发生了变化，请修改 dots_ocr_lib.py 文件中的配置

- https://github.com/neosun100/DeepSeek-OCR-WebUI /279Star/MIT/202601/python/vue/提交多
  - 基于 DeepSeek-OCR 模型的智能图像识别 Web 应用, 参考了 deepseek_ocr_app
    - 多语言客户端示例（Python、JavaScript、Go、TypeScript）
    - 首次运行会下载约 7GB 的模型，请耐心等待
    - ModelScope 自动切换 - HuggingFace 不可用时自动切换
  - 🍎 v3.3 带来原生 Apple Silicon 支持, M3 Pro 上约 3 秒/张
  - 7 种识别模式 - 文档、OCR、图表、图片、查找、自定义prompt等
    - 4 个实战场景（发票提取、批量处理、PDF 处理、表格识别）
  - 上传 PDF 文件后，系统会自动将每一页转换为独立的图片，并保持后续的所有处理逻辑（OCR识别、批量处理等）
  - 🆚 Find 模式: 左右分栏布局, 示例效果用bbox标注出查询的内容(image形式)
  - Bounding Box Visualization - Find mode automatically annotates positions
  - 多语言支持 - 简体中文、繁体中文、英语、日语
  - 后端并发优化 - 使用 ThreadPoolExecutor 实现非阻塞推理
  - 可视化 OCR 进度和队列管理 - 实时队列状态和位置追踪
  - 与 Knowledge-Base-Self-Hosting-Kit/streamdown 示例ui类似
  - https://github.com/neosun100/HunyuanOCR-WebUI /apache2/python
    - 基于腾讯混元OCR的完整Web界面解决方案

- https://github.com/rdumasia303/deepseek_ocr_app /1.5kStar/MIT/202511/python/js/inactive
  - A quick vibe coded app for deepseek OCR
  - React frontend and FastAPI backend
  - Upload PDF files up to 100MB, Real-time progress tracking for large documents
  - 左右分栏布局，右侧用bbox标注搜索的实体, 支持ocr/describe/find/prompts4种场景
  - 支持图片/pdf

- https://github.com/th1nhhdk/local_ai_ocr /613Star/apache2/202601/python/ts/PySide6
  - An local, offline (after initial setup), portable OCR software that can process images and PDF files, using DeepSeek-OCR AI (running directly on your machine).
  - Queue system: Allows processing multiple files sequentially.
  - if GPU is not available, it automatically switches to CPU
  - Multi language support: English, Vietnamese, Chinese, Japanese, ...
  - Multiple file format support: Images .png, .jpg, .webp, .heic, .heif and .pdf documents.
  - Allows selecting page range for processing
  - Fancy Output: Supports displaying Formatted text instead of raw text, allows keeping formatting for pasting into Word, ...
  - 🆚 类似grounding(? 缩略图形式) - OCR process illustration: See exactly what the AI detected as OCR progresses (pretty cool).
  - 依赖PySide6、pillow、PyMuPDF、ollama
  - 3 processing modes:
    - Standard OCR: Extracts text, does not preserve layout well.
    - Free OCR: Extracts text, preserve layout better than "Standard OCR".
    - Markdown Document (keep formatting): Extracts text, attempts to preserve layout (Tables, ...)

- https://github.com/fufankeji/DeepSeek-OCR-Web /531Star/202510/python/ts/inactive
  - 基于 DeepSeek-OCR 的多模态文档解析工具。采用 FastAPI 后端 + React 前端
  - 支持 PDF、图片等多种格式的文档上传和解析
  - 专业的表格识别和图表数据提取功能
  - 将 PDF 内容转换为结构化的 Markdown 格式
  - 🆚 示例效果双栏布局，bbox覆盖在pdf原文上(输出新pdf文件)
  - 首先需要下载 DeepSeek-OCR 模型权重，可从 Hugging Face 或 魔搭社区（ModelScope） 获取
  - https://github.com/newlxj/DeepSeek-OCR-Web-UI /仅简单ocr

- https://github.com/ihatecsv/deepseek-ocr-client /713Star/MIT/202512/python/js
  - A real-time Electron-based desktop GUI for DeepSeek-OCR， 暂不支持webui
  - GPU acceleration (CUDA)
  - Flask backend manages the model, Electron frontend for the UI.
  - 识别文本是流式输出
  - 🐛 仅支持image，暂不支持pdf; 不支持批处理
  - 使用针对mac优化的模型 https://huggingface.co/Dogacel/DeepSeek-OCR-Metal-MPS
  - [A quickly put together a GUI for the DeepSeek-OCR model that makes it a bit easier to use : r/LocalLLaMA _202510](https://www.reddit.com/r/LocalLLaMA/comments/1ocx27p/a_quickly_put_together_a_gui_for_the_deepseekocr/)

- https://github.com/Cross2pro/DeepSeek-OCR-Dashboard /MIT/202604/python/ts/vue
  - FastAPI + Vite/Vue wrapper around the DeepSeek-OCR model for quick local testing.
  - PDF & image upload, with automatic PDF page splitting
  - Progress visualization during uploads/inference so you know it’s working.
  - Bounding-box overlay for layout/annotation visualization.
  - History management: View and manage past OCR results.
  - grounding是图片形式?

- https://github.com/Dogacel/deepseek-ocr-client-macos /MIT/202511/python/js
  - A real-time Electron-based desktop GUI for DeepSeek-OCR
  - [Dogacel/DeepSeek-OCR-Metal-MPS · Hugging Face](https://huggingface.co/Dogacel/DeepSeek-OCR-Metal-MPS)
    - This repository uses the weights from the original DeepSeek-OCR and modifies model to support MPS and CPU inference

- https://github.com/miaoxutao123/deepseek-ocr-translate /MIT/202511/python/ts/vue
  - 使用 DeepSeek-OCR 和 AI 模型实现 PDF 文档的准确翻译
  - 后台异步翻译，实时显示进度和结果，支持暂停/继续/停止
  - OCR 流程: PDF → 图片转换 → DeepSeek-OCR 识别 → 跨页句子合并 → 标签清理 → 存储
  - 翻译流程: 加载文本 → 智能分句 → 后台逐句翻译 → 应用纠错 → 实时显示 → 保存结果
  - Silicon Flow - API 基础设施
  - vue Element Plus - 精美的 UI 组件

- https://github.com/matica0902/MLX-Video-OCR-DeepSeek-Apple-Silicon /AGPL/202512/python/js
  - 影片/PDF/圖片 三合一 OCR, 專為 Apple Silicon 優化的全功能 OCR 解決方案

- https://github.com/wcpsoft/deepseek-ocr-cli /apache2/202511
  - 基于 DeepSeek-OCR 项目改造，提供了增强功能，增加了对多种文档格式的支持，包括 Word、PPT、Excel 等，并提供统一的命令行接口和Web界面进行处理。
  - 双引擎支持：支持vLLM和Transformers两种推理引擎
  - 模块化架构：采用工厂模式设计，vLLM和Transformers引擎解耦，易于扩展和维护
  - 为了支持办公文档格式转换（Word、PPT、Excel等），需要安装LibreOffice
- https://github.com/benedict2310/DeepSeekOCR-Cli /202511/python
  - A quick test to get deepseek ocr to run on a Mac with either images or pdfs
  - Runs natively on Apple Silicon (M1-M4) using PyTorch MPS acceleration

- https://github.com/Moskize91/doc-page-extractor /MIT/202512/python
  - Document page extraction tool powered by DeepSeek-OCR.
  - This package requires PyTorch with CUDA support (GPU Required).
  - It depends on the DeepSeek-OCR model which uses easydict (LGPLv3) for configuration management.

- https://github.com/ikantkode/hunyuan-1b-ocr-app /202511/python
  - [HunyuanOCR-1B - Dockerized Streamlit OCR App - Quite Amazing. : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1p6wios/hunyuanocr1b_dockerized_streamlit_ocr_app_quite/)
  - https://github.com/neosun100/HunyuanOCR-WebUI /apache2/python
    - 基于腾讯混元OCR的完整Web界面解决方案
    - This project uses Gradio to build the web interface and supports one-click Docker deployment
  - https://github.com/PRITHIVSAKTHIUR/HunyuanOCR-Demo /apache2
    - A Gradio-based demonstration application for the Tencent HunyuanOCR model, focused on optical character recognition (OCR) tasks such as text detection, extraction, and coordinate formatting from images

- https://github.com/hiroi-sora/Umi-OCR /40.7kStar/MIT/202511/python/qt-qml
  - 开源、免费的离线OCR软件。
  - 支持截屏/批量导入图片，PDF文档识别，排除水印/页眉页脚，扫描/生成二维码。内置多国语言库
  - 本项目所有代码开源，完全免费。
  - 解压即用，离线运行，无需网络。
  - 自带高效率的离线OCR引擎，内置多种语言识别库
  - 支持的离线OCR引擎：PaddleOCR-json, RapidOCR-json
  - 功能：截图OCR / 批量OCR / PDF识别 / 二维码 / 公式识别

- https://github.com/eastrd/ArchivEye /101Star/AGPL/202304/ts/inactive
  - an offline PDF OCR tool developed to safeguard the privacy and confidentiality of sensitive documents.
  - A GUI offline OCR tool for searching scanned PDF documents on a per-page basis, prioritizing accessibility, privacy, and user experience with Nextron and NodeJS
  - ArchivEye requires `Tesseract` and `GhostScript` to be installed on your system.
    - Tesseract is an integral part of ArchivEye, providing powerful OCR capabilities that convert extracted individual pages into searchable text.
    - GhostScript is used to extract individual pages from the PDF file as images for Tesseract to OCR.

- https://github.com/error-wtf/pdf-translator-enhanced /202512/python
  - Translate scientific PDFs with 100% formula preservation and professional quality
  - Fork of thelanguagenerd/pdf-translator with improved formula protection, table detection, and 20 language support.
  - https://github.com/thelanguagenerd/pdf-translator /CC0
    - english scientific PDF to LaTeX and back to PDF translator

- https://github.com/iptag/mineru-api /MIT/202512/js
  - 基于mineru网页端，抓包分析后将核心的上传及转换功能集成为api，供其他服务调用
  - [[开源]两个比较有意义的docker项目吧，一个是mineru-api，另一个是微信和T的音频转换api ](https://linux.do/t/topic/975584)

- https://github.com/yuzi-ska/OCR-Finder /MIT/202604/python
  - 本地离线 OCR 图片搜索工具，递归扫描文件夹，查找包含目标文本的图片。
  - 本地离线运行 - 使用 RapidOCR ONNX Runtime，无需联网
  - 环境要求 Python 3.10+ Windows
  - [【开源自荐】OCR Finder 递归扫描本地离线的 OCR 图片搜索工具 - LINUX DO _202604](https://linux.do/t/topic/1884459)
    - 和OCR原作用一样，提取图片中的文字信息，关键词是想要在图片中找到的字
    - 使用的本地模型是PaddleOCR的v4版本，结合性能需求等综合下来的识别率算挺高的了，PP模型对手写体也有做优化，我测试下来基本只要不是非常奇怪的手写体大多都能识别

- https://github.com/ikantkode/exaOCR /202601/python
  - simple CPU only OCR for pdf/images/word/excel to markdown. With streamlit.

- https://github.com/RRRRUDDDD/LLM_OCR /MIT/202604/js
  - https://ocr.yoshinagakoi.eu.org/
  - 基于多模态大语言模型的智能文字识别工具。通过 Vision API 从图片中提取文字，支持流式输出、LaTeX 公式渲染、PDF 处理、多格式导出。
  - 纯浏览器端运行，无需后端服务。
  - PDF 支持 — 上传 PDF 文件后自动逐页提取，每页独立处理
  - LLM 驱动识别 — 使用多模态大模型进行文字识别，非传统 OCR 引擎
  - 流式实时输出 — 通过 SSE 流式返回识别A结果，逐字显示
  - 支持直接复制，markdown，txt，word 四种导出方式
  - 多图批量处理 — 支持同时上传多张图片，基于 p-queue 任务队列自动管理并发
  - 智能重试
  - IndexedDB 持久化 — OCR 结果通过 Dexie.js 存入浏览器数据库
  - 客户端图片压缩 — Web Worker + OffscreenCanvas 后台压缩，不阻塞主线程；不支持时自动回退
  - [[开源] 做了一个用LLM来OCR的工具，欢迎各位佬友使用！ - LINUX DO _202604](https://linux.do/t/topic/1888946)

## utils-ocr

- https://github.com/yigitkonur/llm-based-ocr /AGPL/202511/python
  - PDF-to-Markdown OCR API using LLMs with vision capabilities. 
  - The LLM-powered OCR engine that turns any PDF into beautifully formatted Markdown. 
  - Swift OCR: Converts pages → Sends to GPT-4 Vision → Formats as Markdown
  - Features parallel processing, batching, and auto-retry logic for scalable extraction.
  - uses `PyMuPDF` for PDF processing
    - Fork this project and swap PyMuPDF for pdf2image + Poppler.

- https://github.com/mfzzf/deepseek-ocr-openai 
  - DeepSeek-OCR 模型 OpenAI 兼容接口实现
  - 支持流式输出，可实时获取识别结果
  - API 调用示例 (OpenAI 兼容)
  - ocr API的用法还可以参考 基于llm的文本提取
  - https://github.com/neosantara-xyz/deepseek-ocr-api
    - Serverless OCR API powered by DeepSeek-OCR (3B parameters) deployed on Modal.
    - OpenAI-compatible vision API endpoints

- https://github.com/arrase/OCR /202601/python
  - https://arrase.github.io/OCR/
  - Converts a PDF to text (Markdown) by rendering each page to an image and sending it through the deepseek-ocr:latest model served by Ollama via its OpenAI-compatible API (Responses API).

- https://github.com/r-uben/deepseek-ocr-cli /MIT/202601/python/ollama
  - CLI tool for OCR using DeepSeek-OCR model via Ollama. Local processing with zero cloud dependencies.
  - Bounding box annotations removed

- https://github.com/dnvriend/ollama-deepseek-ocr-tool /MIT/202512/python
  - A CLI tool for batch OCR processing of document images using DeepSeek-OCR via Ollama

- https://github.com/anonNo2/deepseek-ocr-server /202511/python
  - 使用Deepseek-OCR 的异步并发pdf处理服务
  - Asynchronous Processing - Non-blocking task queue with status tracking

- https://github.com/fufankeji/vllm-ocr-server /202511/python/ts
  - 大模型Agent开发实战》（体验课）
  - multimodal OCR system built with LangChain 1.0 and vLLM. 
  - Integrates MinerU, PaddleOCR‑VL, and DeepSeek‑OCR with a unified REST API and frontend UI
  - 🔌 Unified parsing interface: pluggable selection of MinerU, PaddleOCR‑VL, and DeepSeek‑OCR
  - Batch parsing: supports batch processing for PDFs and images; auto-splits multi‑page documents
  - Standardized outputs: unified format with Markdown/JSON and image exports
  - Multimodal support: extract text, tables, formulas, images, and more
  - 核心功能一：源码部署 MinerU，使用 vLLM 启动推理服务，并以 MCP Server方式与LagnChain完成集成，支持批量解析多模态PDF、图片格式文件；
  - 核心功能二：使用 vLLM 推理框架部署启动 DeepSeek-OCR 解析服务接口，并支持批量解析PDF和图像文件格式；
  - 核心功能三：本地部署 PaddleOCR-VL ，并通过 PaddleOCR CLI 工具挂载 vLLM 推理服务，提供极高性能的OCR解析服务，支持批量解析PDF和图像文件格式；

- https://github.com/EsmaeilNarimissa/SciDOCX /MIT/202511/python/inactive
  - scientific document conversion and multimodal RAG pipeline powered by DeepSeek-OCR and Qwen2-VL.
  - DeepSeek-OCR: pdf > markdown > pandoc > docx
  - Dual Output:
    - Markdown and DOCX for editing and publishing.
    - JSONL elements (paragraphs, tables, figures) for multimodal retrieval.
  - Embedded Figures: Extracts, deduplicates, and embeds figures with correct captions in both DOCX and JSONL outputs.
  - optionally use Qwen2-VL-2B-Instruct to generate concise, factual figure descriptions.
  - PyMuPDF for PDF processing

- https://github.com/freelawproject/doctor /BSD/202511/python
  - https://free.law/projects/doctor
  - A microservice for document conversion at scale
  - ocr_available: Whether doctor should use tesseract to provide OCR services for the document. OCR is always possible in doctor, but sometimes you won't want to use it, since it can be slow.

- https://github.com/MLNativeAI/paperjet /AGPL/202512/ts
  - https://getpaperjet.com/
  - Open-source platform to securely extract data from any document. Build custom workflows while keeping your data private.
  - Fully open-source - The web and self-hosted versions have the same feature set
  - Zero cloud dependencies - PaperJet doesn’t depend on any cloud services. Everything is self-contained in Docker
  - Built for large documents: easily ingest hundreds of pages at once
  - Use any LLM with your own keys (BYOK)
  - local providers: VLLM, LM Studio and Ollama

- https://github.com/TimmyOVO/deepseek-ocr.rs /2.1kStar/apache2/202511/rust
  - Rust multi‑backend OCR/VLM engine (DeepSeek‑OCR, PaddleOCR‑VL, DotsOCR) with DSQ quantization and an OpenAI‑compatible server & CLI – run locally without Python
  - Rust implementation of the DeepSeek-OCR inference stack with a fast CLI and an OpenAI-compatible HTTP server. 
  - The workspace packages multiple OCR backends, prompt tooling, and a serving layer so you can build document understanding pipelines that run locally on CPU, Apple Metal, or (alpha) NVIDIA CUDA GPUs.
  - The original DeepSeek-OCR ships as a Python + Transformers stack—powerful, but hefty to deploy and awkward to embed. 
  - Candle for tensor compute, with Metal and CUDA backends and FlashAttention support.
  - Rocket + async streaming for OpenAI-compatible /v1/responses and /v1/chat/completions.

- https://github.com/microsoft/OmniParser /CCBy4/202502/python
  - A simple screen parsing tool towards pure vision based GUI agent
  - 用于把屏幕截图转化成LLM可处理的结构化格式，再结合屏幕操作工具即可让LLM操作屏幕

- https://github.com/eloops/hocr2pdf /MIT/202509/js/inactive
  - take scanned image, and hocr output from tesseract, create PDF. Thats it.

- https://github.com/sandraschi/ocr-mcp /MIT/202601/python
  - FastMCP server providing advanced OCR capabilities with current state-of-the-art models (DeepSeek-OCR, Florence-2, DOTS. OCR, PP-OCRv5, Qwen-Image-Layered decomposition), WIA scanner control, and multi-format document processing for PDFs, CBZ comics, and images.

- https://github.com/jbaiter/ocr-parser /MIT/202309/ts
  - This library provides a simple interface to parse OCR data from a stream, buffer or string. 
  - It does not rely on any DOM APIs and can therefore be used in contexts where there is no built-in support for XML parsing, most notably in Web Workers and Service Workers.
  - Currently the library supports hOCR and ALTO OCR markup.

- https://github.com/orasik/parsevision /apache2/202407/python/inactive
  - open source tool to visualise what OCR is parsing in a PDF document to help developers and product teams identify if the parsing has missed some vital information from the document.
  - The tool runs locally, no data are sent outside your machine
  - 支持 Tesseract, EasyOCR
  - 效果类似hocr的文字图层，没有画框的文字就是未识别出的

- https://github.com/Qianxia666/ocr /GPL/202511/python
  - 利用 OpenAI API 进行图片和 PDF 文档的 OCR 识别，支持异步任务处理、实时通信和完整用户机制的任务管理系统。
  - 自动将识别结果格式化为 Markdown 格式，支持数学公式（KaTeX）
  - 批量处理: 支持 PDF 多页文档的批量识别
  - 异步处理: 采用异步任务队列，支持大文件的后台处理

- https://github.com/Fusyong/recover-layout-from-ocr /202509/python/inactive
  - PDF OCR Utils and Examples, especially for workbook text extraction, layout recovery, and conversion to Markdown.
  - 使用PyMuPDF进行PDF转换为图片
  - 使用RapidOCR进行OCR识别
  - 将OCR结果转换为文本行，过滤不需要的box和row
    - 兼容 有道OCR/pymupdf/RapidOCR 的JSON格式
  - 给文本行中的标题标出Markdown标记
  - 保存为jpg后OCR效果比png好，不知何故

- https://github.com/mary-lev/llm-ocr /202506/python
  - LLM-powered OCR evaluation and correction package that supports multiple language models for OCR processing and text correction tasks.

- https://github.com/trykuku/ocr_cook /202601/python/ts
  - 一个基于 OCR 技术的 Photoshop 自动化工具，可以自动识别图片中的文字并生成 Photoshop JSX 脚本，支持在 Photoshop 中自动创建文字图层。
  - 图片 OCR 识别：基于 PaddleOCR 和 PaddleX，支持高精度文字识别
  - 智能文字定位：精确识别文字在图片中的位置和大小
  - 翻译功能：可选的中文到英文翻译功能（Electron 版本）
  - fastapi + PyInstaller 打包后端为独立可执行文件

- https://github.com/athrael-soju/Snappy /66Star/MIT/202512/python/ts
  - Snappy implements region-level document retrieval by unifying vision-language models with OCR through spatial coordinate mapping. 
  - Unlike traditional systems that return entire pages (VLMs) or lack semantic grounding (OCR-only), Snappy uses `ColPali`'s patch-level similarity scores as spatial relevance filters over OCR-extracted regions; operating entirely at inference time without additional training.
    - 方案与模型绑定
  - The approach formalizes coordinate mapping between vision transformer patch grids (32×32) and OCR bounding boxes, repurposing ColPali's late interaction mechanism to generate interpretability maps.
    - 类似将ocr的bbox渲染为了热力图

- https://github.com/maxent-ai/ocrpy /MIT/202211/python/inactive
  - https://maxentlabs.com/ocrpy
  - OCR, Archive, Index and Search: Implementation agnostic OCR framework.
  - Unified interface to google vision, aws textract, azure, tesseract and other OCR tools
  - The core objective of ocrpy is to let users perform OCR, archive, index and search any document with ease, providing an intuitive interface and a powerful Pipeline API to solve common OCR-based tasks.

- https://github.com/yuanjua/PaperStructure /apache2/202602/python
  - Convert scientific publications in PDF to structured Markdown via only lightweight ONNX OCR models
  - a lightweight CLI tool designed to transform academic papers into clean, structured Markdown.
  - Layout Detection -- YOLOX detects titles, sections, paragraphs, formulas, tables, figures
  - Text Recognition -- PP-OCRv5 ONNX pipeline
  - Formula Recognition -- Encoder-decoder LaTeX OCR
  - Parallel Processing -- multi-threaded PDF page processing

- https://github.com/Leisurelybear/ocr-bye /MIT/202604/js
  - 将文字转换成OCR无法轻易识别的图片
  - 文字单独随机旋转角度

- https://github.com/aiptimizer/turbo-ocr /MIT/202604/cpp/python
  - Fast GPU OCR server. C++ / CUDA / TensorRT.
  - Platform: Linux only. Requires NVIDIA GPU (tested on RTX 5090). AMD and Intel GPUs are not supported.
  - High-throughput text detection and recognition using PP-OCRv5 models. Fused CUDA kernels, zero per-request allocation, multi-stream pipeline concurrency. For when you need to process hundreds of images per second rather than one page at a time.
  - [Turbo-OCR for high-volume image and PDF processing : r/Rag _202604](https://www.reddit.com/r/Rag/comments/1sg5o33/turboocr_for_highvolume_image_and_pdf_processing/)
    - Running VLMs over a million pages is slow and expensive. PaddleOCR, in my opinion the best non-VLM open source OCR, only handled ~15 img/s on my RTX 5090, which was still too slow. PaddleOCR-VL was crawling at 2 img/s with vLLM.
    - The main bottleneck was GPU utilization. PaddleOCR wasn't using the hardware well, and PaddleOCR HPI isn't available for this architecture. 
    - So I built a C++/CUDA inference server around Paddle's PP-OCRv5 models with FP16 inference. It takes images and PDFs via HTTP/gRPC and returns bounding boxes and text.
    - Results: 100+ img/s on text-heavy pages, 1,000+ on sparse ones.
  - Trade-offs: this sacrifices layout fidelity for speed. If you need perfect layout detection, multi-column reading order, or complex table extraction, you're better off with VLM-based OCR like GLM-OCR or PaddleOCR-VL.
# ocr-visual-grounding 🆚
- qwen3-vl
  - qwenvl html 指令使用时，不能开thinking, 只支持图片，不支持pdf
    - 实测qwenvl html的输出质量不高(经常遗漏段落), 大多元素缺失bbox属性，而替代为 `<div class="image" data-bbox="130 106 947 450"><img data-bbox="130 106 947 450"/></div>`

- ocr-grounding
  - [Qwen VL](https://github.com/QwenLM/Qwen3-VL/blob/main/cookbooks/document_parsing.ipynb)
  - [Rex Omni demos](https://huggingface.co/spaces/Mountchicken/Rex-Omni)
  - [deepseek-ocr](https://github.com/deepseek-ai/DeepSeek-OCR)
  - [dots.ocr](https://github.com/rednote-hilab/dots.ocr)
  - [CogVLM](https://github.com/zai-org/CogVLM)
  - [Seed1.8/1.5-VL](https://github.com/ByteDance-Seed/Seed1.5-VL)
  - [MiniCPM-V Grounding](https://github.com/OpenSQZ/MiniCPM-V-CookBook/blob/main/inference/minicpm-v4_5_grounding.md)

- https://www.datalab.to/playground/documents/new /体验最好/marker/surya
  - [datalab-to/chandra · Hugging Face](https://huggingface.co/datalab-to/chandra)
  - 输出支持 blocks/json/html/markdown
  - blocks在hover时能高亮原文档/原图片中对应的bounding-box

- [Docling Visual grounding](https://docling-project.github.io/docling/examples/visual_grounding/)  
  - [Visual Grounding from Docling _202504](https://alain-airom.medium.com/visual-grounding-from-docling-74a0ee078981)

- https://github.com/hypothesis/pdf.js-hypothes.is /403Star/bsd/202501/js/专注于标注/inactive
  - https://web.hypothes.is/
  - This is a copy of Mozilla's PDF.js viewer with Hypothesis annotation tools added.
  - https://github.com/hypothesis/h /3.1kStar/bsd/202604/python
    - h is the web app that serves most of the https://hypothes.is/ website, including the web annotations API at https://hypothes.is/api/. 
  - https://github.com/hypothesis/client /bsd/202604/ts/mustache
    - The Hypothesis client is a browser-based annotator that is a client for h's API.
    - It’s used by the Hypothesis browser extension, and can also be embedded directly into web pages.

- https://github.com/allenai/pawls /apache2/202302/python/ts
  - https://pawls.apps.allenai.org/
  - https://www.youtube.com/watch?v=TB4kzh2H9og
  - PDF Annotations with Labels and Structure is software that makes it easy to collect a series of annotations associated with a PDF document. 
  - It was written specifically for annotating academic papers within the Semantic Scholar corpus, but can be used with any collection of PDF documents.
  - the ui, which renders the user interface that PAWLS uses
  - the api, which serves PDFs and saves/recieves annotations
  - 支持自动选中bbox及自由绘制bbox, 然后添加标注信息
  - you'll need to use the PAWLS CLI to preprocess and assign the PDFs you want to serve. 
    - ensure that the papers are pre-processed with grobid so that they have token information.
  - https://github.com/allenai/pdffigures2 /scala
    - Given a scholarly PDF, extract figures, tables, captions, and section titles.

- https://github.com/QwenLM/Qwen3-VL /17.4kStar/apache2/202511/jupyter
  - [Qwen3-VL 发布 _20250923](https://qwen.ai/blog?id=qwen3-vl)
  - https://huggingface.co/spaces/Qwen/Qwen3-VL-Demo
  - https://huggingface.co/spaces/Qwen/Qwen3-VL-Demo/tree/main
  - comprehensive upgrades across the board: superior text understanding & generation, deeper visual perception & reasoning, extended context length, enhanced spatial and video dynamics comprehension, and stronger agent interaction capabilities.
  - Expanded OCR: Supports 32 languages (up from 10); robust in low light, blur, and tilt; better with rare/ancient characters and jargon; improved long-document structure parsing.
  - [Qwen2.5 VL _202501](https://qwenlm.github.io/blog/qwen2.5-vl/)
    - Qwen2.5-VL has designed a unique document parsing format called QwenVL HTML format, which extracts layout information based on HTML. 
    - QwenVL HTML can perform document parsing in various scenarios, such as magazines, research papers, web pages, and even mobile screenshots
  - [PDF OCR MD格式的prompt · Issue · QwenLM/Qwen3-VL](https://github.com/QwenLM/Qwen3-VL/issues/749)
    - 评测CC-OCR使用的prompt在对应的仓库里，其中每个子任务对应一种输出类型的prompt。cookbook里的document parsing prompt主要针对QwenVL HTML格式，如果想让它输出markdown格式，同时让table保持HTML格式，公式latex格式，直接使用OmniDocBench中的prompt就能得到不错的效果，评测结果也较Qwen2-VL-72B高出不少。

- https://github.com/yeahhe365/InsightPDF /MIT/202601/ts
  - https://insightpdf.pages.dev/
  - 基于 AI 的 PDF 智能助手，支持见解提取、内容总结和智能文档搜索
  - 基于 Google Gemini 多模态模型构建的智能文档助手，支持精确的视觉定位与边框高亮。
  - 视觉定位 (Visual Grounding) AI 不仅回答问题，还会自动跳转到 PDF 对应页面，并用红框高亮显示答案来源（支持文本段落、图表、数据表格）
  - 聊天记录和设置均存储在浏览器本地（LocalStorage/IndexedDB），只需配置 Key，无需担心数据泄露。
  - PDF 渲染: React-PDF

- https://github.com/ankit1khare/doc-ext-visually-grounded /202504/python/inactive
  - A app that let's you chat with PDFs and provides evidence for the answers by visually grounding them into the PDF pages.
  - Multiple PDF Support: Upload several PDF files simultaneously
  - Document Analysis: Extracts text, tables, and figures from PDFs using Landing AI's agentic-doc SDK
  - Visual Evidence: See exactly where in the document the answers come from with highlighted bounding boxes
  - 依赖streamlit、PyMuPDF、Pillow
  - Efficiently processes documents with maximum parallelism
  - Large Document Support: Handles PDFs of any size through automatic chunking and reassembly

- https://github.com/populationgenomics/groundmark /MIT/202603/python
  - PDF to Markdown conversion and quote-to-bbox resolution.
  - Convert: Send PDF pages to a vision-capable LLM (via Pydantic AI) to produce clean Markdown with `<!--page-->` markers between pages.
  - Resolve: Given verbatim quote strings, locate them in the source PDF and return bounding box coordinates. 
  - Uses `pypdfium2` for per-character bbox extraction and `seq-smith` for Smith-Waterman alignment.
  - https://github.com/folded/gemini-ocr
    - gemini-ocr provides anchorite provider plugins that convert PDFs to traceable Markdown using Google Cloud APIs.

- https://github.com/google/langextract /apache2/202511/python/可参考ux/提交少
  - A Python library for extracting structured information from unstructured text using LLMs with precise source grounding and interactive visualization.
  - Precise Source Grounding: Maps every extraction to its exact location in the source text, enabling visual highlighting for easy traceability and verification.
  - [example - Romeo and Juliet Full Text Extraction](https://github.com/google/langextract/blob/main/docs/examples/longer_text_example.md)
    - This creates an interactive HTML visualization for exploring the extracted entities
    - 示例仅高亮关键词, 原文必须是文本

- https://github.com/PRITHIVSAKTHIUR/Super-OCRs-Demo /apache2/202511/python
  - A Gradio-based demo application for comparing state-of-the-art OCR models: DeepSeek-OCR, Dots. OCR, HunyuanOCR, and Nanonets-OCR2-3B. 
  - Users can upload images, select models, apply custom prompts, and generate recognized text or visual grounding results.
  - Switch between DeepSeek-OCR (with resolution and task options), Dots. OCR, HunyuanOCR, and Nanonets-OCR2-3B for flexible OCR workflows.
  - DeepSeek-Specific Tools: Resolution presets (Tiny to Gundam), task types (Free OCR, Markdown, Parse Figure, Locate Object), and bounding box visualization.
  - Streaming Output: Real-time text generation for Dots. OCR and Nanonets-OCR2-3B; non-streaming for others.
  - Visual Results: DeepSeek outputs annotated images with bounding boxes or grounding visuals.
  - CUDA-compatible GPU (recommended for bfloat16 models; falls back to CPU).

- https://github.com/kasuba-badri-vishal/dhrishtikon /apache2/202506/python
  - A Streamlit-based web application for visual grounding and document understanding.
  - This application allows users to upload images or PDFs and ask questions about their content, with the system providing answers along with visual grounding at different levels (block, line, word, and point).
    - OCR the Image to get the text regions
    - Match the Question and Answer with the text regions using Text Matching strategy
    - Return the Grounding(bbox, text) for the Question and Answer
  - Currently using `Doctr` OCR model
  - Word -level and Line -level Grounding Support
  - Multi-line Grounding Support
    - Since adding multi-line support for the engineering solution might reduce the accuracy of the Grounding
  - For annotating the images with bounding boxes at block, line, word and point levels for visual question-answering tasks.
  - https://github.com/text2knowledge/docTR-Labeler /apache2/202511/python
    - a tool to label OCR data for the docTR and OnnxTR projects.
    - Features like auto-annotation using OnnxTR and auto polygon adjustment
    - This project is based on the Form-Labeller project by Devarshi Aggarwal.

- https://huggingface.co/spaces/PaddlePaddle/PaddleOCR/tree/main 
  - Gradio demo for PaddleOCR. PaddleOCR demo supports Chinese, English, French, German, Korean and Japanese.
  - 识别后在图片上方画框突出有文本的位置, 最后输出带画框标记的图片
  - [PaddleOCR-VL Online Demo - a Hugging Face Space by PaddlePaddle](https://huggingface.co/spaces/PaddlePaddle/PaddleOCR-VL_Online_Demo)
    - 这个识别效果和dotsocr类似，提供md text/preview/位置图

- https://huggingface.co/spaces/gokaygokay/Florence-2/tree/main /python
  - `OCR with Region` 的任务会在图片上方画框突出有文本的位置, 最后输出带画框标记的图片
  - https://github.com/anyantudre/Florence-2-Vision-Language-Model
    - jupyter示例
- https://huggingface.co/spaces/prithivMLmods/Multimodal-OCR3/tree/main
  - https://prithivmlmods-multimodal-ocr3.hf.space/
  - 输出 markdown文本/html文本

- https://github.com/IDEA-Research/Rex-Omni /1kStar/IDAE/202512/python/华人作者
  - https://rex-omni.github.io/
  - https://huggingface.co/spaces/Mountchicken/Rex-Omni/tree/main
    - [Rex Omni demos](https://huggingface.co/spaces/Mountchicken/Rex-Omni)
  - Detect Anything via Next Point Prediction (Based on Qwen2.5-VL-3B)
  - 视觉效果是检测物体，不确定文本检测效果
  - Rex-Omni is a 3B-parameter Multimodal Large Language Model (MLLM) that redefines object detection and a wide range of other visual perception tasks as a simple next-token prediction problem.
  - Unified architecture for multiple vision tasks
  - Rex-Omni reformulates visual perception as a next point prediction problem, unifying diverse vision tasks within a single generative framework. It predicts spatial outputs (e.g., boxes, points, polygons) auto-regressively and is optimized through a two-stage training pipeline—large-scale Supervised Fine-Tuning (SFT) for grounding, followed by GRPO-based reinforcement learning to refine geometry awareness and behavioral consistency.
  - https://github.com/Mountchicken/Resophy /202512/python/js
    - Resophy is an HTML-based AI paper reader with: AI Translation & Analysis — instantly understand structure
    - modern paper reader that helps you quickly understand the core content of papers through a simple tech stack (HTML + JavaScript + Python Flask) and AI features
    - Main Service (Resophy Core): HTML + JavaScript + Python Flask backend service, providing core features such as paper management, classification, and search
    - LLM Server: LLM inference service for AI translation, interpretation, and arXiv paper analysis (optional, supports local deployment or remote API)
    - MinerU Server: Document parsing service for PDF to Markdown parsing (optional, for AI features)
  - https://github.com/alirzx/Auto-Labeling-Service-Based-on-RexOmni-Arcitecture- /202512/python/js
    - A modular FastAPI service leveraging the Rex-Omni multimodal framework, designed for automated dataset labeling across 14+ computer vision tasks.
    - Supports multi-model inference via a registry system, allowing flexible selection between RexOmni and Florence models for different tasks.
    - OCR with configurable output format (Box/Text) and granularity (Word/Line)

- 🌰 https://news.ycombinator.com/item?id=43189412
  - Bounding boxes. There still isn't really a model that gives super precise bounding boxes. Supposedly Gemini and Qwen were trained for it, but they don't perform as well as traditional models.
  - Visual grounding a.k.a. bounding boxes are definitely one of those things that VLMs aren't natively good at (partly because the cross-entropy losses used aren't really geared for bounding box regression). We're definitely making some strides here to improve that so you're going to get an experience that is almost as good as native bounding box regression (all within the same VLM).
  - there does not yet exist a multimodal vision LLM approach that is capable of identifying bounding boxes of where the text occurs.
  - https://github.com/vlm-run/vlmrun-cookbook/blob/main/notebooks/04_visual_grounding.ipynb
  - In this notebook, we'll walk through an example of extracting structured data from US driver licenses along with their "visual grounding" in the form of bounding boxes. 

- [Feat: Find bounding box for each section in the image · Pull Request · getomni-ai/zerox](https://github.com/getomni-ai/zerox/pull/44)
  - PyTesseract is very old and much worse at OCR than GPT (try with handwritten notes for example), so this PR would be a massive downgrade. I am not sure if it is even a good idea for finding bounding boxes. I'd suggest to look into topics such as "Layout Detection" or "Layout Analysis"
  - [Research: Add bounding boxes to response ](https://github.com/getomni-ai/zerox/issues/7)

- https://github.com/opendatalab/DocLayout-YOLO /AGPL/202504/python
  - https://huggingface.co/spaces/opendatalab/DocLayout-YOLO /gradio
  - Enhancing Document Layout Analysis through Diverse Synthetic Data and Global-to-Local Adaptive Perception
  - 视觉效果是画框显示布局
# labelling/annotation
- https://github.com/sai-prakash/pdf-ocr-annotation /MIT/202510/python/ts
  - A full-stack PDF annotation application built with FastAPI (Python) and React + Vite (TypeScript). 
  - This application supports both readable and scanned PDFs, with advanced text extraction, intelligent annotation, and powerful search capabilities.
  - Automatic detection of page type
  - PyMuPDF(AGPL) for native text-based PDFs
  - EasyOCR for scanned/image-based PDFs
  - Advanced PDF Viewer: Built with react-pdf
    - Custom canvas overlay for annotations
    - Text selection with bounding boxes
    - 🐛 对于图片pdf，在ocr后只能选择识别出整行或半行，不能拖动选择任意文本

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

- https://github.com/CVHub520/X-AnyLabeling /7.6kStar/GPL/202512/python
  - a powerful annotation tool that integrates an AI engine for fast and automatic labeling. 
  - It's designed for multi-modal data engineers, offering industrial-grade solutions for complex tasks.
  - https://github.com/CVHub520/X-AnyLabeling-Server /apache2/202512/python
    - lightweight and extensible serving framework for AI model inference, specifically designed for X-AnyLabeling.
    - It provides a production-ready solution with pluggable architecture and flexible configuration for various auto-labeling scenarios.
    - Decoupled Design: Framework handles service management and resource scheduling without interfering with model implementation details
    - Pluggable Architecture: Rapidly integrate custom models without modifying core framework code
    - Flexible Configuration: All parameters are configurable with sensible defaults, adaptable to different deployment scenarios

- https://github.com/PFCCLab/PPOCRLabel /369Star/NALic/202510/python
  - a semi-automatic graphic annotation tool suitable for OCR field, with built-in PP-OCR model to automatically detect and re-recognize data.
  - written in Python3 and PyQT5, supporting rectangular box, table, irregular text and key information annotation modes.
  - Annotations can be directly used for the training of PP-OCR detection and recognition models.
  - https://github.com/Evezerest/PPOCRLabel /legacy

- https://github.com/advent259141/Auto_Labeling /202512/python/js
  - 一个基于视觉语言模型（VLM）的自动图片标注工具，支持 YOLO 格式输出。
  - 使用 OpenAI 格式 API 调用视觉语言模型
  - 自动输出标准 YOLO 格式标注文件
  - 手动模式：逐张标注，可确认或跳过
  - 自动模式：批量自动标注
  - 可上传参考图片帮助 VLM 理解标注需求

- https://github.com/muratcanlaloglu/moonlabel /apache2/202509/python/ts
  - Moondream VLM labeler for object detection and image captions with one‑click YOLO, COCO, VOC, and Captions export.
  - MoonLabel is both a Python library and a tiny web UI to generate object-detection and image-caption datasets quickly.
  - Backends supported: Moondream Cloud, Moondream Station, or fully local (Hugging Face).
  - FastAPI server — Served by a single moonlabel-ui command.
  - Image caption datasets — Export captions as captions.jsonl alongside images.
  - https://github.com/KoDelioDa/moonlabel /202507/python/ts
    - Moondream VLM-powered labeler one-click YOLO export

- https://github.com/klassif-ai/react-pdf-ner-annotator /MIT/202305/ts/inactive
  - https://react-annotator-demo.netlify.app/
  - Annotate entities directly onto a PDF with automatic OCR for scanned PDFs
  - OCR on scanned PDFs
  - 需要指定entity后，才会高亮出ocr后符合entity语义的文本
# exampels

# utils

# more
