---
title: lib-office-docling-examples
tags: [docling, examples, format, office]
created: 2025-09-21T13:58:28.944Z
modified: 2025-09-21T13:58:46.548Z
---

# lib-office-docling-examples

# guide

- tips
  - 还可以在 ocr benchmark/leaderboard 中寻找参考和代码
# popular
- https://github.com/docling-project/docling /39.3kStar/MIT/202509/python
  - https://github.com/DS4SD/docling
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

- https://github.com/docling-project/docling-agent /MIT/202604/python
  - Docling-agent simplifies agentic operation on documents, such as writing, editing, summarizing, etc.
  - Targeted editing: Load an existing Docling JSON and apply focused edits with natural-language tasks.
  - Schema-guided extraction
  - Model-agnostic: Plug in different backends via Mellea model_ids
  - [Docling just announced Docling Agent + Chunkless RAG : r/Rag _202604](https://www.reddit.com/r/Rag/comments/1smeh2j/docling_just_announced_docling_agent_chunkless_rag/)

- https://github.com/scub-france/Docling-Studio /MIT/202604/python/vue
  - https://scub-france.github.io/Docling-Studio/
  - A visual document analysis studio powered by Docling. 
  - Upload a PDF, configure the extraction pipeline, and visualize the results — text, tables, images, formulas, bounding boxes — all from your browser.

- https://huggingface.co/spaces/ibm-granite/granite-docling-258M-WebGPU/tree/main /apache2/202510/html/vanillajs
  - a demo which showcases the model running entirely in your browser with WebGPU acceleration
  - ✨ 此类demo可考虑实现类似图片对比的新旧对比滑块
  - [Granite Docling WebGPU: State-of-the-art document parsing 100% locally in your browser. : r/LocalLLaMA _202510](https://www.reddit.com/r/LocalLLaMA/comments/1o0php3/granite_docling_webgpu_stateoftheart_document/)
    - I had a very good experience with granite-docling as my goto pdf processor for RAG knowledge base.
    - Love this. WebGPU seems to be underutilized in general and could provide a better alternative to BYOK + cloud inference.
    - If someone could add translation feature on top of this, it would be perfect
    - It is first time I am seeing someone using Transformers.js
  - https://github.com/PDFMathTranslate/PDFMathTranslate /29.8kStar/AGPLv3/202511/python 
    - ✨ 可参考翻译后pdf布局不变的实现方式, 特别是表格中英文变中文但布局不变
    - 支持双栏布局显示原文和翻译，体验非常好
    - [Upload your documents and see how OmniAI reads scans, PDFs](https://getomni.ai/ocr-demo)
  - https://github.com/pdfme/pdfme /MIT
    - 提供了机遇json模版生成pdf的方案

- https://huggingface.co/spaces/mozilla-ai/document-to-markdown/tree/main
  - https://huggingface.co/spaces/mozilla-ai/document-to-markdown
  - 可选: easyocr, tesseract, rapidocr, ocrmac

- https://huggingface.co/spaces/PaddlePaddle/PaddleOCR/tree/main /apache2/202504/python
  - and i tested handwritten text for english. it got the numbers right...

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
  - [Nanonets-OCR2: An Open-Source Image-to-Markdown Model with LaTeX, Tables, flowcharts, handwritten docs, checkboxes & More : r/LocalLLaMA _202510](https://www.reddit.com/r/LocalLLaMA/comments/1o5nlli/nanonetsocr2_an_opensource_imagetomarkdown_model/)
    - models designed for advanced image-to-markdown conversion and Visual Question Answering (VQA).
    - 1.5b--apache2, 3b--Qwen2.5-VL-3B-research-only-lic

- https://github.com/docling-project/docling-serve /725Star/MIT/202509/python
  - Running Docling as an API service.
  - The server is available at http://127.0.0.1:5001
  - An image for AMD ROCm 6.3 (docling-serve-rocm) is supported but not published due to its large size.

- https://github.com/drmingler/docling-api /693Star/MIT/202503/python/inactive
  - a highly scalable and lightweight backend for docling.
  - deployable and scalable backend server that efficiently converts various document formats (pdf, docx, pptx, html, images, etc) into Markdown. 
  - it offers text/table extraction, OCR, and batch processing with sync/async endpoints.
  - Powered by Docling (IBM's advanced document parser), this service is built with FastAPI, Celery, and Redis, ensuring fast, efficient processing.
  - Optimized for both CPU and GPU modes, with GPU highly recommended for production environments

- https://github.com/docling-project/docling-mcp /210Star/MIT/202508/python
  - Making docling agentic through MCP
  - a service that provides tools for document conversion, processing and generation. 
  - It uses the Docling library to convert PDF documents into structured formats and provides a caching mechanism to improve performance.
  - The service exposes functionality through a set of tools that can be called by client applications.
  - Local document caching for improved performance
  - Support for local files and URLs as document sources
  - RAG applications with Milvus upload and retrieval
  - https://github.com/microsoft/markitdown/tree/main/packages/markitdown-mcp

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

- https://github.com/DCC-BS/docling-glm-ocr /MIT/202604/python
  - https://dcc-bs.github.io/documentation/
  - A docling OCR plugin that delegates text recognition to a remote GLM-OCR model served by vLLM.
  - a docling plugin that replaces the built-in OCR stage with a call to a remote GLM-OCR model hosted on a vLLM server.
  - Each page crop is sent to the vLLM OpenAI-compatible chat completion endpoint as a base64-encoded image. The model returns Markdown-formatted text which docling merges back into the document structure.
# examples
- https://github.com/mozilla-ai/document-to-markdown /MIT/202506/python/inactive
  - Convert unstructured documents to markdown using the Docling.
  - This blueprint guides you to convert various unstructured documents (PDFs, DOCX, HTML, etc.) to markdown, or other, formats using the Docling CLI or a locally-hosted demo UI
  - We have built a simple Graphical Interface demo of Docling to showcase some basic functionality 

- https://huggingface.co/spaces/AmineAce/pdf-tables-rag-demo/tree/main /202512/python/单文件
  - https://amineace-pdf-tables-rag-demo.hf.space/
    - I built a free demo using IBM's Docling – it handles merged cells and footnotes way better than most open-source options.
    - Built with Gradio
  - [Free PDF-to-Markdown demo that finally extracts clean tables from 10-Ks (Docling) : r/Rag](https://www.reddit.com/r/Rag/comments/1pupkkf/free_pdftomarkdown_demo_that_finally_extracts/)

- https://github.com/paazmaya/docling-japanese-books /MIT/202511/python
  - A streamlined document processing tool that uses Docling to extract, process, and store Japanese books and documents for LLM training workflows.
  - Extract and annotate images with SHA-256 hashing for deduplication
  - Vector Storage: Milvus database with enhanced metadata
  - LLM Ready: Multiple embedding models (Jina v4, BGE-M3, Snowflake Arctic, MiniLM) with Late Chunking optimization

- https://github.com/AI-Engineer-Skool/booktutor-ai /AGPL/202507/python/单文件
  - https://www.skool.com/ai-engineer/
  - Using Docling to create an AI assistant out of any PDF book in minutes
  - 依赖langchain
  - 可使用本地llm
- https://github.com/fahdmirza/doclingwithollama /apache2/单文件
  - Docling with Ollama - RAG on Local Files with Local Models

- https://github.com/HossamEldinx/docling-in-action /202411
  - This is a simple Question-Answering system using Retrieval Augmented Generation (RAG) with Groq's LLM.

- https://github.com/genieincodebottle/parsemypdf /MIT/202508/python
  - A Comprehensive example codes for extracting content from complex PDFs with mixed elements, including text and image data extraction

- https://github.com/lesteroliver911/docling-pdf-processor /MIT/202412/python/inactive
  - A simple UI wrapper around Docling for document processing. 
  - I built this to make document analysis more accessible and thought others might find it useful.
  - Presents results in a clean Streamlit interface

- https://github.com/AIAnytime/SmolDocling-OCR-App /MIT/202503/python/inactive
  - SmolDocling OCR App built using SmolDocling 256M Model and Streamlit.
  - https://github.com/bibekpdl/SmolDocling-Document-Processor

- https://github.com/Abdoulaye-Sayouti/Secure-Offline-RAG-System /MIT/202412/python/inactive
  - A RAG system designed for efficient processing of diverse content types with minimal computational overhead.
  - This solution won 1st place in the Secure RAG Challenge by UnderstandTech

- https://github.com/kv1830/fast_pdf_trans
  - 基于`MinerU`实现pdf转markdown的功能，接着对markdown进行分割， 送给大模型翻译，最后组装翻译结果并由`pypandoc`生成结果pdf。
# utils
- https://github.com/messkan/rag-chunk /MIT/202511/python
  - A Python CLI to test, benchmark, and find the best RAG chunking strategy for your Markdown documents.
  - Multiple chunking strategies: fixed-size, sliding-window, paragraph
  - Recall-based evaluation with test JSON files
  - [Roadmap Discussion: Is LangChain's "RecursiveCharacterSplitter" actually better? I'm building v0.3.0 to find out. : r/Rag](https://www.reddit.com/r/Rag/comments/1p2xhjq/roadmap_discussion_is_langchains/)

- https://github.com/2dogsandanerd/smart-ingest-kit /202511/python
  - [I extracted my production RAG ingestion logic into a small open-source kit (Docling + Smart Chunking) : r/Rag](https://www.reddit.com/r/Rag/comments/1p4ku3q/i_extracted_my_production_rag_ingestion_logic/)
  - Most tutorials tell you to use `RecursiveCharacterTextSplitter(chunk_size=1000)`. That's fine for demos, but in production, it breaks
    - PDF tables get shredded into nonsense.
    - Code blocks get cut in half.
    - Markdown headers lose their hierarchy.
  - I stripped out all the business logic from my app and left just the "Smart Loader".
  - It uses Docling (by IBM) for layout-aware parsing and applies heuristics to choose the optimal chunk size based on file type.
    - PDFs: Uses semantic splitting with larger chunks (800 chars) to preserve context.
    - Code: Uses small chunks (256 chars) to keep functions intact.
    - Markdown: Respects headers and structure.
    - Output: Clean Markdown that your LLM actually understands.

- https://github.com/ghodsizadeh/pdf2csv /MIT/202501/python
  - https://pdf2csv-py.streamlit.app/
  - This project provides a tool to convert tables from PDF files into CSV or XLSX format using the Docling library. 
  - It extracts tables from PDFs and saves them as CSV or XLSX files, optionally reversing text for right-to-left languages.
  - This project heavily depends on the Docling library for PDF table extraction, it will be installed automatically when you install this package.

- https://github.com/shoryasethia/markdrop /GPL/202507/python/inactive
  - A Python package for converting PDFs to markdown while extracting images and tables, generate descriptive text descriptions for extracted tables/images using several LLM clients.
  - PDF to Markdown conversion with formatting preservation using Docling
  - Automatic image extraction with quality preservation using XRef Id
  - Table detection using Microsoft's Table Transformer

- https://github.com/docling-project/docling-eval /MIT/python
  - Evaluation framework for document processing models and services.
  - Evaluate Docling on various datasets.

- https://github.com/docling-project/docling-core /MIT/python
  - A python library to define and validate data types in Docling.
  - a library that defines core data types and transformations in Docling.
  - Docling Core provides the foundational `DoclingDocument` data model and API, as well as additional APIs for tasks like serialization and chunking
  - Docling Core defines the `DoclingDocument` as a Pydantic model, allowing for advanced data model control, customizability, and interoperability.
# ocr/vlm
- https://github.com/emcf/thepipe /1.5kStar/MIT/202510/python/inactive
  - a package that can scrape clean markdown, multimodal media, and structured data from complex documents.
  - It can extract well-formatted data from a wide range of sources, including PDFs, URLs, Word docs, Powerpoints, Python notebooks, videos, audio, and more.
  - Uses VLM for OCR in text-only mode
  - Accepts a wide range of sources, including PDFs, URLs, Word docs, Powerpoints, Python notebooks, GitHub repos, videos, audio, and more
  - The default install only pulls in CPU-friendly dependencies so it is suitable for constrained environments and CI systems. 
    - GPU-enabled libraries such as PyTorch and Triton are left as optional extras.
  - 👾 By default, thepipe uses the OpenAI API, so VLM features will work out-of-the-box provided you pass in an OpenAI client.
    - If you wish to use a local vision-language model or a different cloud provider, you can provide a custom OpenAI client
  - structured extraction is being deprecated and will be removed in future releases. The current implementation is a simple wrapper around OpenAI's chat API, which is not ideal for structured data extraction. We recommend OpenAI's structured outputs for structured data extraction, or using Trellis AI for automated workflows with structured data.

- https://github.com/aitomatic/ai-vision-capture /apache2/202601/python
  - A Python library for extracting and analyzing content from PDF, Image, and Video files using VLM
  - Supports multiple providers including OpenAI, Anthropic Claude, Google Gemini, and Azure OpenAI.
  - Async Processing: Configurable concurrency for batch operations
  - Structured Output: Template-based data extraction to JSON
  - Pluggable Architecture: Provider abstraction with auto-detection
  - PDF-to-image conversion using PyMuPDF (fitz)
  - VisionCapture: Used for extracting specific fields from documents (e.g., forms, technical diagrams)
    - 似乎只提取字段, 不提取插图

- https://github.com/Aquos06/reader-vl /MIT/202503/python/inactive/提交少
  - a tool that transforms various document formats, like PDFs and DOCX files, into a unified structure.
  - Process PDFs and DOCX (for now).
  - Uses multimodal LLMs to extract meaning from diagrams, images, chart, and etc.
  - Structured Output: Converts documents into a well-defined schema, preserving relationships between text and visuals.
  - Fast & Efficient: Leverages YOLO for object detection and Tesseract OCR.
  - Extensibility: Designed for easy integration into AI pipelines for customization and scalability.
  - I am not solely using OCR to parse the pdf. I am using both OCR for normal text (we called it section) and VLM for the more abstract one like Table, Chart, Diagram, and etc
  - [Introducing Reader VL: A Tool for Unified Document Processing with VLM Integration : r/LocalLLaMA _202503](https://www.reddit.com/r/LocalLLaMA/comments/1j2m6m7/introducing_reader_vl_a_tool_for_unified_document/)
    - I'm developing a RAG system for enterprise (B2B) and noticed that many company documents contain charts, images, and other non-text elements. Our current parsers (Docling, Unstructured) struggle to process these formats. While searching for a solution, I couldn't find any parser leveraging modern VLMs—so I decided to build one myself.
    - Currently, Reader VL processes entire documents in a single pass. I'm actively working on implementing chunking and batching functionalities to better support very large documents, such as those spanning hundreds or thousands of pages.

- https://github.com/PRITHIVSAKTHIUR/Doc-VLMs-exp /apache2/202507/python/inactive
  - document-focused Vision-Language Model application that provides advanced document analysis, text extraction, and multimodal understanding capabilities.
  - This application features a streamlined Gradio interface for processing both images and videos using state-of-the-art vision-language models specialized in document understanding.
  - Document-Specialized Models: Three cutting-edge VLM models optimized for document processing
  - Image Processing: Advanced document analysis and text extraction from images
  - Video Processing: Frame-by-frame video analysis with temporal understanding
  - Real-time Streaming: Live output generation with immediate feedback
  - Dual Output Format: Raw text stream and formatted markdown results
  - Canvas-Style Interface: Clean, professional output display
# code-rag
- https://github.com/starthackHQ/contextinator /apache2/202511/python
  - Turning messy repos into weapons of mass structured context.
  - It uses Abstract Syntax Tree (AST) parsing to extract semantic code chunks, generates embeddings, and stores them in a vector database-enabling AI agents to understand, navigate, and reason about codebases with unprecedented precision.
  - AST-Powered Chunking - Extract functions, classes, and methods from 23+ programming languages
  - Semantic Search - Find relevant code using natural language queries
  - Full Pipeline Automation - One command to chunk, embed, and store
  - 🛢️ Docker (for ChromaDB)
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

- https://github.com/magicyuan876/mineru-tianshu /apache2/202601/python/ts/vue
  - 天枢 - 企业级 AI 数据预处理平台，将非结构化数据转换为 AI 可用的结构化格式
  - 支持文档、图片、音频等多模态数据处理 | GPU 加速 | MCP 协议
  - 后端：FastAPI、LitServe、MinerU、PaddleOCR、SenseVoice、SQLite、Loguru
  - 前端：Vue 3、TypeScript、Vite、TailwindCSS、Pinia、Vue Router
  - 多解析引擎: MinerU、PaddleOCR-VL、MarkItDown、格式引擎
    - pipeline: MinerU 标准流程，通用文档解析
    - vlm-transformers/vlm-vllm-engine: MinerU VLM 模式
    - paddleocr-vl: 109+ 语言，自动方向矫正, 仅支持 GPU: PaddleOCR-VL 目前不支持 CPU 及 Arm 架构
  - 文档: PDF、Word、Excel、PPT → Markdown/JSON（MinerU、PaddleOCR-VL 109+ 语言、水印去除）
  - 视频: MP4、AVI、MKV → 语音转写 + 关键帧 OCR🧪（FFmpeg + SenseVoice）
  - 音频: MP3、WAV、M4A → 文字转写 + 说话人识别（SenseVoice 多语言）
  - 大文件并行处理: PDF 自动拆分功能：超过阈值（默认 500 页）的 PDF 自动拆分为多个子任务并行处理
    - 并发安全: 原子操作防止任务重复，支持多 Worker 并发
    - Worker 主动拉取: 0.5秒响应，无需调度器触发
  - RustFS 对象存储：所有解析结果的图片自动上传到对象存储, S3 兼容 API，基于 minio-py 实现
  - GPU 负载均衡: LitServe 自动调度，避免显存冲突，多 GPU 隔离
  - 企业特性: GPU 负载均衡、任务队列、JWT 认证、MCP 协议、现代化 Web 界面
  - Tianshu 支持完全离线部署，提供两种部署模式：
    - 方式 1：Linux 服务器（有 GPU 则加速，无 GPU 自动降级 CPU）
    - 方式 2：CPU 专用版（Mac/无 GPU 环境）

- https://github.com/wzdavid/mineru-api /MIT/202601/python
  - [只需 4 步搞定！开源文档解析服务 MinerU-API 最新安装指南 - 知乎](https://zhuanlan.zhihu.com/p/1999940036863492525)
  - 基于 Celery 的异步文档解析服务
  - 异步处理：基于分布式任务队列，支持高并发
  - 支持任务重试和故障恢复
  - 实时监控：任务状态跟踪和队列统计。你可以随时查看任务的进度和状态
  - 模块化设计，易于添加新的解析引擎。如果你需要处理新的文档格式，只需要添加一个新的解析引擎即可。

- https://github.com/firecrawl/mineru-api /AGPL/202512/python
  - Fork of neka-nat/mineru-api - API server for MinerU.
  - designed for running MinerU on serverless platforms such as Runpod.
  - https://github.com/neka-nat/mineru-api /AGPL/202512/python
    - API server for MinerU.
# extraction
- https://github.com/VikParuchuri/tabled /GPL/202501/python/archived
  - Detect and extract tables to markdown and csv
  - deprecated. The functionality here has been migrated to marker. 
  - Tabled is a small library for detecting and extracting tables. It uses `surya` to find all the tables in a PDF, identifies the rows/columns, and formats cells into markdown, csv, or html.

- https://github.com/camelot-dev/excalibur /1.8kStar/MIT/202501/python/js
  - https://excalibur-py.readthedocs.io/
  - A web interface to extract tabular data from PDFs. powered by Camelot.
  - Note: Excalibur only works with text-based PDFs and not scanned documents
  - control over your data. All file storage and processing happens on your own local or remote machine.
  - Excalibur can be configured with MySQL and Celery for parallel and distributed workloads. By default, sqlite and multiprocessing are used for sequential workloads.
  - Upload a PDF and enter the page numbers you want to extract tables from.
  - Go to each page and select the table by drawing a box around it. (You can choose to skip this step since Excalibur can automatically detect tables on its own. )
  - Click on "View and download data" to see the extracted tables.
  - https://github.com/camelot-dev/camelot /MIT/202508/python/inactive
    - https://camelot-py.readthedocs.io/
    - A Python library to extract tabular data from PDFs

- https://github.com/microsoft/table-transformer /2.8kStar/MIT/202309/python/inactive
  - Table Transformer (TATR) is a deep learning model for extracting tables from unstructured documents (PDFs and images). 
  - This is also the official repository for the PubTables-1M dataset and GriTS evaluation metric.

- https://github.com/ronnywang/pdf-table-extractor /202511/js
  - https://ronnywang.github.io/pdf-table-extractor/
  - Extractor tables from PDF

- https://github.com/datalab-to/pdftext /644Star/apache2/202506/python
  - Text extraction like `PyMuPDF`, but without the AGPL license. PDFText extracts plain text or structured blocks and lines. 
  - It's built on `pypdfium2`, so it's fast, accurate, and Apache licensed.
  - It first uses pypdfium2 to extract characters in order, along with font and other information. Then it uses a simple decision tree algorithm to group characters into lines and blocks. It does some simple postprocessing to clean up the text.
  - built on some amazing open source work, including:  pypdfium2, scikit-learn

- https://github.com/KatherLab/llmaixlib /MIT/202508/python/inactive
  - a Python toolkit for automated document preprocessing (including OCR) and information extraction using large language models
  - Preprocessing: Extracts human-readable Markdown or plain text from a wide range of document types, automatically falling back to OCR for scanned or image-based files.
  - Uses a large language model (LLM) to transform unstructured or semi-structured text into structured data—validated by Pydantic models or JSON Schema—via an OpenAI-compatible API.
  - OCR tools: Tesseract (for OCRmyPDF), a GPU for faster OCR (Marker and PaddleOCR)
  - OpenAI-compatible API endpoint: Required for information extraction

- https://github.com/nanonets/hands-on-vision-language-models /202409/python/inactive
  - [Best Vision Language Models for Document Data Extraction _202409](https://nanonets.com/blog/vision-language-model-vlm-for-data-extraction/)
  - [Benchmarking vision language models for document data extraction : r/computervision _202409](https://www.reddit.com/r/computervision/comments/1fv0ns5/benchmarking_vision_language_models_for_document/)
    - Models tested : Qwen2, MiniCPM, Bunny, GPT-4o mini, Gemini 1.5 flash,  Claude 3.5
    - I have chosen these models because they fit on a consumer GPU (less than 24GB VRAM)
  - Datasets used: SROIE and CORD receipt datasets - i’ve explained why these in the blog, but tldr is that they are 
    - standardized (and hence simpler to benchmark)
    - complex enough to present a challenge to all the VLMs
    - no MLLM benchmarks focussing on extracting structured data from documents
    - Both fields and tables are present in the datasets
  - Takeaways
    - QWEN is the superior OS model, and Claude is the best among closed source

- https://github.com/yyy-OPS/SciDataExtractor /202601/python/js
  - 一款开源的科学图表数据提取工具，专为科研人员设计。基于 FastAPI 和 React 开发，它结合计算机视觉与 AI 技术，将静态图表图片精准转换为可编辑 Excel 数据
  - 支持交互式坐标校准、HSV 颜色提取，并具备 AI 数据清洗与断点修复功能，能有效去除噪点并补全曲线，辅助高效科研分析。
  - 结合了计算机视觉与 AI 技术，旨在将论文、报告中的2D科研数据图表通过精确的交互式操作转换为可编辑的 Excel 数据。
  - 颜色分割提取: 基于 OpenCV 的 HSV 颜色空间分割算法，精准提取指定颜色的曲线数据点。
  - 数据清洗: 利用 AI 视觉能力，自动识别并剔除提取数据中的网格线干扰、噪点和文字遮挡。
  - 精确校准: 采用交互式手动校准（三点/四点法），确保像素坐标到物理坐标的转换精度，完全由用户掌控。
  - 交互式操作: 现代化 React 前端，支持框选删除、手动加点、实时预览和撤回/重做。
  - 前端 (Frontend): React 18, Vite, Konva, TailwindCSS
  - 后端 (Backend): Python 3.11+, FastAPI, OpenCV, OpenAI API, Pandas
  - [[开源]科研图表(曲线图)数据提取工具(导出excle数据) _202601](https://linux.do/t/topic/1435502)
    - 主要功能就是：基于 OpenCV (HSV 颜色空间) 做分割，提取图片中该颜色的曲线数据，然后描点，最后输出excle。加了AI数据清洗/修复/平滑的功能，效果不理想，还不如使用手工绘制。
    - 亮点可能就是支持手工绘制，如果实在不行，自己手动描一下，设置一下平滑度，出来的数据也堪堪能用。我测试下来，50的颜色容差一般可以把大体轮廓绘制出来了，再不济自己手动点几个点。
    - 也可以在origin中复现，工具可以识别改颜色的RGB，在origin中直接设置一样的颜色
  - 🤔 支持大佬，只能是曲线吗？其他类型的图表能识别吗
    - 目前只做了2D曲线，后面考虑考虑做更多类型的数据图

- https://github.com/whyhow-ai/knowledge-table /MIT/202411/python/ts/inactive
  - open-source package designed to simplify extracting and exploring structured data from unstructured documents. 
  - It enables the creation of structured knowledge representations, such as tables and graphs, using a natural language query interface. 
# resources
- https://github.com/PSPDFKit/pdf-to-markdown /cli/NonOpen
  - Standalone CLI wrapper and docs for Nutrient's PDF-to-Markdown extractor
  - https://x.com/jdrhyne/status/2039750394587591150
    - We are shipping it as a closed source, free to use for up to 1,000 documents per month, no license key required, and your documents stay completely local. 
# more
