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
  - https://github.com/getomni-ai/zerox /MIT/202505/python/ts/inactive
    - OCR & Document Extraction using vision models
    - Convert that file into a series of images, Pass each image to GPT and ask nicely for Markdown
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
# examples
- https://github.com/mozilla-ai/document-to-markdown /MIT/202506/python/inactive
  - Convert unstructured documents to markdown using the Docling.
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

- https://github.com/AKSarav/pdfstract /apache2/202511/python/js
  - web application for converting PDFs to multiple formats using various state-of-the-art extraction libraries. Built with FastAPI backend and React frontend
  - [Built a small tool to compare PDF → Markdown libraries (for RAG / LLM workflows) : r/Rag _202507](https://www.reddit.com/r/Rag/comments/1m1j10e/built_a_small_tool_to_compare_pdf_markdown/)
    - I’ve been exploring different libraries for converting PDFs to Markdown to use in a Retrieval-Augmented Generation (RAG) setup.
    - But testing each library turned out to be quite a hassle — environment setup, dependencies, version conflicts, etc.
    - Currently, it supports: docling pymupdf4llm markitdown marker
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
- https://github.com/Aquos06/reader-vl /202503/python/inactive
  - a tool that transforms various document formats, like PDFs and DOCX files, into a unified structure.
  - Process PDFs and DOCX (for now).
  - Uses multimodal LLMs to extract meaning from diagrams, images, chart, and etc.
  - Structured Output: Converts documents into a well-defined schema, preserving relationships between text and visuals.
  - Fast & Efficient: Leverages YOLO for object detection and Tesseract OCR.
  - Extensibility: Designed for easy integration into AI pipelines for customization and scalability.
  - I am not solely using OCR to parse the pdf. I am using both OCR for normal text (we called it section) and VLM for the more abstract one like Table, Chart, Diagram, and etc
  - [Introducing Reader VL: A Tool for Unified Document Processing with VLM Integration : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1j2m6m7/introducing_reader_vl_a_tool_for_unified_document/)
    - I'm developing a RAG system for enterprise (B2B) and noticed that many company documents contain charts, images, and other non-text elements. Our current parsers (Docling, Unstructured) struggle to process these formats. While searching for a solution, I couldn't find any parser leveraging modern VLMs—so I decided to build one myself.
    - Currently, Reader VL processes entire documents in a single pass. I'm actively working on implementing chunking and batching functionalities to better support very large documents, such as those spanning hundreds or thousands of pages.
# code-rag
- https://github.com/starthackHQ/contextinator /apache2/202511/python
  - Turning messy repos into weapons of mass structured context.
  - It uses Abstract Syntax Tree (AST) parsing to extract semantic code chunks, generates embeddings, and stores them in a vector database-enabling AI agents to understand, navigate, and reason about codebases with unprecedented precision.
  - AST-Powered Chunking - Extract functions, classes, and methods from 23+ programming languages
  - Semantic Search - Find relevant code using natural language queries
  - Full Pipeline Automation - One command to chunk, embed, and store
  - 🛢️ Docker (for ChromaDB)
# more
