---
title: toc-office-pdf-etl-extraction
tags: [etl, ocr, pdf]
created: 2026-04-07T11:47:22.073Z
modified: 2026-04-07T12:53:02.538Z
---

# toc-office-pdf-etl-extraction

# guide

# popular
- https://github.com/run-llama/liteparse /686Star/apache2/202603/python/ts
  - https://developers.llamaindex.ai/liteparse/
  - https://github.com/jerryjliu/liteparse_samples
  - LiteParse is a standalone OSS PDF parsing tool focused exclusively on fast and light parsing. 
  - It provides high-quality spatial text parsing with bounding boxes, without proprietary LLM features or cloud dependencies.
  - Everything runs locally on your machine.
  - Fast Text Parsing: Spatial text parsing using PDF.js
    - use a typescript wrapper called `pdfium` to simplify pdf.js integration
  - Flexible OCR System:
    - Built-in: Tesseract.js (zero setup, works out of the box!)
    - HTTP Servers: Plug in any OCR server (EasyOCR, PaddleOCR, custom)
    - Standard API: Simple, well-defined OCR API specification
  - Screenshot Generation: Generate high-quality page screenshots for LLM agents
  - 🐛
    - 仅导出文本， 丢失了文本格式， 是否丢失语义?
    - 需要支持扫描版pdf
  - Standalone Binary: No cloud dependencies, runs entirely locally
  - Multi-platform: Linux, macOS (Intel/ARM), Windows
  - https://github.com/run-llama/liteparse/tree/main/packages/python
    - Python wrapper for LiteParse 
  - https://x.com/jerryjliu0/status/2034665976428724267
    - Introducing LiteParse - the best model-free document parsing tool for AI agents 
  - [PDF Parsing With Bounding Boxes: The Step That Takes Document AI From Demo to Production  _202604](https://themindfulai.dev/articles/parsing-pdfs-with-bounding-boxes)
    - [Draw bounding box highlights on PDF page screenshots. Visualize LiteParse textItem positions with colored rectangles.](https://gist.github.com/satish860/fc7fc5665d864f9f6f0267006a750652)
  - https://github.com/axa-group/Parsr /apache2/202210/ts/inactive
    - a minimal-footprint document (image, pdf, docx, eml) cleaning, parsing and extraction toolchain which generates readily available, organized and usable data in JSON, Markdown (MD), CSV/Pandas DF or TXT formats.
    - 依赖Tesseract、Pdfminer.six、ImageMagick、QPDF
    - Consider using an alternative such as LiteParse
# extraction-pdf
- https://github.com/CatchTheTornado/text-extract-api /3.1kStar/MIT/202512/python/inactive
  - https://github.com/CatchTheTornado/pdf-extract-api /renamed
  - https://demo.doctractor.com/
  - Convert any image, PDF or Office document to Markdown text or JSON structured document with super-high accuracy, including tabular data, numbers or math formulas.
  - built with FastAPI and uses Celery for asynchronous task processing. Redis is used for caching OCR results.
  - No Cloud/external dependencies all you need: PyTorch based OCR (EasyOCR) + Ollama 
  - different OCR strategies including llama3.2-vision, easyOCR, minicpm-v, remote URL strategies including marker
  - Removing PII This tool can be used for removing Personally Identifiable Information out of document 
  - Storage Strategies switchable storage strategies (Google Drive, Local File System ...)
  - CLI tool for sending tasks and processing results: The project includes a CLI for interacting with the API. 

- https://github.com/ispras/dedoc /655Star/apache2/202512/python/inactive
  - converting documents to a unified output format. It extracts a document’s logical structure and content: tables, text formatting and metadata. 
  - The document’s content is represented as a tree storing headings and lists of any level. 
  - Dedoc can be integrated in a document contents and structure analysis system as a separate module.
# extraction-vlm
- https://github.com/NameetP/pdfmux /MIT/202604/python
  - https://pdfmux.com/
  - Universal PDF extraction orchestrator. 
  - Routes each page to the best backend, audits the output, re-extracts failures. 
  - 5 rule-based extractors + BYOK LLM fallback. 
  - One CLI. One API. Zero config.
  - Router, not extractor. pdfmux does not compete with PyMuPDF or Docling. It picks the best one per page.
  - multi-pass. Extract, audit confidence, re-extract failures with a stronger backend.
  - Segment-level detection. Each page is classified by content type (text, tables, images, formulas, headers) before routing.
  - 4-signal confidence. Dynamic quality scoring from character density, OCR noise ratio, table integrity...
  - Document cache. Each PDF is opened once, not once per extractor. Shared across the full pipeline.
  - Data flywheel. Local telemetry tracks which extractors win per document type. Routing improves with usage.
  - supports any LLM via 5 lines of YAML: ollama, gpt
  - Integrations: LangChain, LlamaIndex
  - Tested on opendataloader-bench: #2 overall, #1 among free tools

- https://github.com/yuvaraj-kannan/preocr /apache2/202604/python
  - https://preocr.io/
  - library for OCR detection and document extraction. Detect if PDFs need OCR before expensive processing—save 50–70% on OCR costs.
  - CPU-only, no GPU required
  - It analyzes PDFs, Office documents (DOCX, PPTX, XLSX), images, and text files to detect if they're already machine-readable—helping you skip OCR for 50–70% of documents and cut costs.
  - Use PreOCR to filter documents before Tesseract, AWS Textract, Google Vision, Azure Document Intelligence, or MinerU. 
  - Works offline, CPU-only, with 100% accuracy on validation benchmarks.
  - Structured Extraction: Tables, forms, images, semantic data—Pydantic models, JSON, or Markdown

- https://github.com/oidlabs-com/Lexoid /apache2/202604/python
  - https://oidlabs-com.github.io/Lexoid
  - efficient document parsing library that supports both LLM-based and non-LLM-based (static) PDF document parsing.
  - Automatic parsing strategy selection: LLM-based and static parsing
  - Support for multiple LLM providers (OpenAI, Google, Meta/Llama, Together AI)
  - Table detection and markdown conversion
  - Parallel processing support
  - Reference highlighting and bounding box extraction

- https://github.com/mindsdb/aipdf /MIT/202604/python
  - a stand-alone, minimalistic, yet powerful pure Python library that leverages multi-modal gen AI models (OpenAI, llama3 or compatible alternatives) to extract data from PDFs and convert it Markdown.
  - By default, AIPDF attempts to determine which pages to send to the LLM based on their content and whether they can be processed using traditional text parsing. This is done to improve performance
  - Every call to the LLM is made in parallel, so the processing time is significantly reduced. 
    - 提供了2个api, 支持sync 和 async
  - Any file system: pass a file object, because that way it is flexible for you to use this with any type of file system, s3, localfiles, urls etc
  - only 2 required libraries: openai, PyMuPDF

- https://github.com/Curiosity-Ai-BV/localOCR /MIT/202604/python
  - A streamlined Streamlit app that uses local AI vision models (via Ollama) to analyze images and PDFs. 
  - Upload multiple files, choose a model, get detailed descriptions or extract structured fields, and export the results to CSV.
  - Upload multiple images (JPG, PNG) and PDF documents
  - Modular architecture: core pipeline, adapters, and UI components fully separated
  - Hardened Ollama adapter: exact‑match model resolution, TTL‑cached model listing, typed errors (ModelUnavailable, ParseError, PDFError), and streaming support
  - Session‑isolated results in Streamlit (safe for shared deployments)
  - Optional system prompt, adjustable image resize, JPEG quality, PDF render scale
  - uses Streamlit for the interface, Ollama for local model serving, Pillow for image processing, and PyMuPDF for PDF pages. 
  - webapp or CLI usage (headless)

- https://github.com/quest-bih/quest-pdf-tools /AGPL/202512/python
  - FastAPI-based web application and API service for processing PDF documents
  - The service can be deployed either as a full web application with an intuitive interface or as a standalone API.
  - PDF Layout Analysis: Detects and annotates different document elements including titles, text blocks, figures, tables, and formulas
  - Automatically identifies and removes headers, footers, and other irrelevant content from PDFs
  - 🖼️ Figure Extraction: Extracts and exports figures from PDFs into separate image files
    - The bounding box computation happens in `src/doc_layout.py` during `YOLO` detection. YOLO runs inference on the rendered image (internally resized to 1024x1024). 
    - Each cropped figure is saved as a PNG file with a naming convention like {pdf_name}_page{N}_figure{M}.png 
    - the cropped figures are saved to the filesystem
    - the figure extraction uses `PyMuPDF`'s `get_pixmap()` method. This method renders the PDF page as an image at 300 DPI, regardless of the original PDF format
    - `PyMuPDF` handles the conversion internally - you get the same rendered image output for both types
  - Table Extraction: Identifies and exports tables from PDFs into separate files
  - Text Extraction: Extracts plain text content from PDFs with preserved formatting
  - YOLO-based Detection: Utilizes DocLayout-YOLO model for accurate document layout analysis
- https://github.com/huridocs/pdf-document-layout-analysis /1.1kStar/apache2/202601/python
  - A Docker-powered microservice for intelligent PDF document layout analysis, OCR, and content extraction
  - The service offers both a user-friendly Gradio web interface for interactive use and a comprehensive REST API
  - Export to JSON, Markdown, HTML, and visualize PDF segmentations
  - Extract tables as HTML and formulas as LaTeX
  - Apply OCR to scanned documents: uses Tesseract OCR with support for 150+ languages
  - Visual & Fast Models - Choose between VGT (Vision Grid Transformer) for accuracy or LightGBM for speed
  - Translate documents to multiple languages using Ollama models
  - https://github.com/huridocs/pdf-table-of-contents-extractor
    - extract Table of Contents (TOC) information from PDF files using the outputs generated by the pdf-document-layout-analysis service
  - https://github.com/huridocs/pdf-text-extraction
    - extract text from PDF files

- https://github.com/Flopsky/MarkThat /MIT/202601/python
  - A Python library for converting images and PDFs to Markdown or generating rich image descriptions using state-of-the-art multimodal LLMs.
  - Multiple Provider Support: OpenAI, Anthropic, Google Gemini, Mistral, and OpenRouter
  - Advanced Figure Extraction: Automatically detect, extract, and process figures from PDFs
    - 💡 可参考插图提取的流程逻辑 👇 
    - Detection: Analyzes document content to identify pages with figures
    - Coordinate Mapping: Overlays coordinate grids and identifies figure boundaries
    - Extraction: Crops figures using precise coordinate mapping
    - Integration: Embeds figure paths into the final markdown output
  - Robust Retry Logic: Intelligent retry with fallback models and failure feedback
  - Async Support: Concurrent processing for improved performance
  - Clean architecture: Type-safe, well-documented, and thoroughly tested
  - 实测可运行的模型包括, gpt-4o-mini, mistral-medium, nemotron-12b-vl, 🤔 但效果都很差

- https://github.com/tatevik-t/pdf_visual_extraction /MIT/202509/python/inactive
  - A Python library for extracting text and visual elements (tables, figures) from PDF document
  - Use OpenAI's GPT-4o-mini to detect and extract tables and figures
    - 🧊 返回bbox数据, 需要手动裁剪图片
  - Convert extracted tables to CSV format using LLM

- https://github.com/AdemBoukhris457/Doctra /apache2/202511/python
  - https://ademboukhris457.github.io/Doctra/
  - Parse, extract, and analyze documents with ease
  - Doctra requires `Poppler` for PDF processing
  - `StructuredPDFParser` is a comprehensive PDF parser that extracts all types of content from PDF documents
    - Uses `PaddleOCR` for accurate document layout analysis
    - Supports both `PyTesseract` (default) and `PaddleOCR` PP-OCRv5_server for text extraction
    - Visual Element Extraction: Saves figures, charts, and tables as images
    - VLM Integration: Optional conversion of visual elements to structured data
    - Multiple Output Formats: Generates Markdown, Excel, and structured JSON
  - https://github.com/AdemBoukhris457/Documents-Parsing-Lab /202511/jupyter
    - Jupyter notebooks testing different OCR models for document parsing (Dolphin, MonkeyOCR, Marker, Nanonets, ...)
    - This repository enables easy benchmarking and practical usage of the latest open-source and cloud-based solutions for document image processing.
    - a quick start guide for getting started with Doctra, a powerful tool for structured document parsing without Vision Language Models (VLM).

- https://github.com/aitomatic/ai-vision-capture /apache2/202601/python
  - A Python library for extracting and analyzing content from PDF, Image, and Video files using VLM
  - Supports multiple providers including OpenAI, Anthropic Claude, Google Gemini, and Azure OpenAI.
  - Async Processing: Configurable concurrency for batch operations
  - Structured Output: Template-based data extraction to JSON
  - Pluggable Architecture: Provider abstraction with auto-detection
  - PDF-to-image conversion using `PyMuPDF` (fitz)
  - VisionCapture: Used for extracting specific fields from documents (e.g., forms, technical diagrams)
    - 似乎只提取字段, 不提取插图

- https://github.com/daviden1013/vlm4ocr /MIT/202604/python/js
  - Python package and Web App for OCR with vision language models
    - A drag-and-drop web application 经典示例, 特色缺乏
    - Python package supports concurrent batch processing for large amount of documents. 
    - CLI provides lightweight access to most OCR features
  - extraction with JSON: instead of OCR the entire document, extract only the key information and output as JSON.
  - concurrent batch processing of multiple images
  - Stream OCR resuts in real-time
  - OpenAICompatible VLM engines: Qwen3-VL, LLaVa-1.5, gpt-4o
  - 依赖poppler

- https://github.com/iamarunbrahma/vision-parse /457Star/MIT/202509/python
  - Parse PDFs into markdown using Vision LLMs
    - 实测本地模型不好用, 很多小图片
  - Intelligently identifies and extracts text, tables, and LaTeX equations from scanned documents into markdown-formatted content with high precision
  - Multi-LLM Support: Seamlessly integrates with multiple Vision LLM providers such as OpenAI, Gemini, and Llama for optimal accuracy and speed
  - Supports local model hosting with Ollama for secure, no-cost, private, and offline document processing
  - 🛝
    - VisionParserError: Failed to convert page 1 to base64-encoded PNG: Ollama Model processing failed: timed out

- https://github.com/getomni-ai/zerox /12.2kStar/MIT/202505/python/ts/inactive
  - https://docs.getomni.ai/zerox
  - https://getomni.ai/ocr-demo
  - OCR & Document Extraction using vision models
  - Convert that file into a series of images, Pass each image to GPT and ask nicely for Markdown
  - supports structured data extraction from documents using a schema.
  - Concurrent Processing
  - Zerox is available as both a Node and Python package.
    - nodejs uses `graphicsmagick` and ghostscript for the PDF => image processing step
    - python uses `poppler` and pdf2image
  - [Research: Add bounding boxes to response _202407](https://github.com/getomni-ai/zerox/issues/7)
    - I would love to have some bounding boxes come back with the text response. Primarily for highlighting locations in the original document where the text got pulled. Not sure exactly how I would proceed with this one

- https://github.com/EsmaeilNarimissa/SciDOCX /MIT/202511/python/inactive
  - scientific document conversion and multimodal RAG pipeline powered by DeepSeek-OCR and Qwen2-VL.
  - DeepSeek-OCR: pdf > markdown > pandoc > docx
  - Dual Output:
    - Markdown and DOCX for editing and publishing.
    - JSONL elements (paragraphs, tables, figures) for multimodal retrieval.
  - Embedded Figures: Extracts, deduplicates, and embeds figures with correct captions in both DOCX and JSONL outputs.
  - optionally use Qwen2-VL-2B-Instruct to generate concise, factual figure descriptions.
  - PyMuPDF for PDF processing

- https://github.com/gsmatheus/pdf-image-extractor /202511/python
  - a Python script designed to process PDF files, specifically extracting and saving images embedded within the pages of the document. 
  - Automatically resizes the extracted images to 60% of their original size, ensuring consistent output and potentially reducing file size.
  - Text Extraction: For each processed page, the script also extracts and prints the textual content.
  - pdfplumber, fitz (PyMuPDF), PIL (Pillow)

- https://github.com/linjc16/PDF-Extraction /MIT/202303/python
  - A tool for extracting tables and figures from PDF files.
  - Pipeline for Table and Figure Extraction from Papers
  - First, use `PaddleOCR` to extract text, tables and figures from each paper.
    - We first convert PDF to images page by page by using `PyMuPDF`. To improve the performance of the following OCR operation, these images are unpsamped 8x to get high resolution inputs.
    - Then, use the results from the last step to output the final extracted samples.

- https://github.com/EvilFreelancer/img2md-vlm-ocr /MIT/202509/python/js
  - service for extracting document structure and content from images using advanced computer vision and vision-language models (VLM). 
  - The system combines YOLO-based document layout segmentation with OpenAI-compatible VLM models to accurately detect, classify, and extract text content from document images, converting them to structured Markdown format
  - Document Layout Segmentation: Uses YOLOv8-based models to detect and classify document elements (text blocks, tables, images, headers, etc.)
  - Vision-Language Model Integration: Leverages OpenAI-compatible VLM models (default: Qwen2.5-VL) for intelligent text extraction
  - CLI Tools: Command-line utilities for batch PDF processing and document analysis
  - Image Processing: Drag-and-drop upload, real-time preview, and bounding box visualization
    - Overlay detected elements on the original image
    - Cropped image extraction for tables and images
  - Core: FastAPI, Uvicorn, Pydantic, Pydantic-settings
  - Computer Vision: Pillow, OpenCV, Ultralytics (YOLO)
  - Document Processing: pdf2image
  - 🛝
    - uv run python process_pdf.py -i ~/Documents/01files/testpdf/html5canvas1pages-pic-figure.pdf -o output

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

- https://github.com/katanaml/sparrow /5.1kStar/GPL/202601/python
  - https://sparrow.katanaml.io/
  - Structured data extraction and instruction calling with ML, LLM and Vision LLM
  - Pluggable Architecture: Mix and match different pipelines (Sparrow Parse, Instructor, Agents)
  - Multiple Backends: MLX (Apple Silicon), Ollama, vLLM, Docker, Hugging Face Cloud GPU
  - Multi-format Support: Images (PNG, JPG) and multi-page PDFs
  - API-First Design: RESTful APIs for easy integration
  - Built-in dashboard and agent workflow tracking
  - Local Vision LLMs: Mistral, QwenVL, DeepSeek OCR, etc.
  - Usage Analytics: Track API calls, success rates, performance
  - Real-time Monitoring: Live processing statistics
  - Pipeline Comparison
    - Sparrow Parse: Use for structured data extraction from documents
    - Sparrow Instructor: Use for text analysis, summarization, Q&A
    - Sparrow Agents: Use for complex multi-step document processing workflows
  - 💰 Licensed under GPL 3.0. Free for open source projects and organizations under $5M revenue.

- https://github.com/Tro-fish/ChartEye-all_in_one-figure-VQA /202407/pythoh/js/inactive
  - ChartEye: Multi Modal QA Chatbot for Scientific Figure Images
  - This repository contains the code for ChartEye, including its implementation and execution instructions, for the Figure-to-Caption and QA Chatbot for Chemistry and Materials Science documents.
  - Extract Chart(figure) image from PDF, PPTX, WORD files --> Image Extraction
    - ❓ 似乎不支持图片版pdf
    - PDF: Extracting images with pymupdf
    - WORD: Extracting images with python-docx
    - PPTX: Extracting images with python-pptx
  - Convert Chart(figure) image to text explanation --> Chart Captioning
  - Convert imformation in a Chart(figure) image to a number --> Chart Derendering
  - Answer Question about the information in a Chart(figure) imge --> Question Answering

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

- https://github.com/pengyuanli/PDFigCapX /apache2/202411/python/inactive
  - https://www.eecis.udel.edu/~compbio/PDFigCapX
  - For each document in the input_path, the main function will generate a corresponding folder with the same name as the original document in the output_path. All extracted figures (in jpg format), captions (in text format) and their coordinate information (in json format) will be saved in the corresponding folder.
  - PDF parsing using xpdf 

- https://github.com/morkev/vlm-yolo-detector /MIT/202601/python
  - VLM-powered image extraction and semantic search for equipment manuals. This repository provides the image data pipeline for the agentic-rag system.
  - Extract images from PDF documents (embedded images + rendered pages with diagrams)
  - Generate VLM descriptions for each image using LLaVA via Ollama
  - Create semantic embeddings for intelligent image search
  - Integrate with agentic-rag for visual content retrieval
  - PyMuPDF (for PDF processing)
  - sentence-transformers (for embeddings)
  - Pillow (for image processing)
  - Optional Dependencies (for YOLO training): ultralytics, torch, torchvision
  - 🛝 
    - uv sync时 there are no versions of yologen[vlm]
  - https://github.com/ahmetkumass/yolo-gen /MIT/202601/python
    - Train YOLO + VLM with one command. No extra labeling
    - Train object detection and natural language description models from a standard YOLO dataset. VLM training data is auto-generated from YOLO labels.
    - Why YOLO + VLM?
      - YOLO alone: Fast but not enough for production-level accuracy
      - VLM alone: Smart but too slow for production
      - YOLO + VLM: Fast detection + VLM adds detailed descriptions, classification, and false positive filtering

- https://github.com/longhoag/vlm-prototype /MIT/202601/python
  - Simple VLM pipeline prototype for object detection with proprietary model
  - The system processes traffic images, identifies vehicles (cars, motorcycles, mopeds, trucks, buses), and outputs annotated images with green bounding boxes.
  - Images are analyzed via API, vehicle coordinates are extracted, and bounding boxes are rendered on the output images.
  - Opens input images using Pillow (PIL), Draws green (#00FF00) bounding boxes

- https://github.com/landing-ai/vision-agent /5.3kStar/apache2/202508/python/deprecated
  - VisionAgent is the Visual AI pilot from LandingAI. Give it a prompt and an image, and it automatically picks the right vision models and outputs ready‑to‑run code—letting you build vision‑enabled apps in minutes. 
  - The VisionAgent library includes a set of tools, which are standalone models or functions that complete specific tasks. When you prompt VisionAgent, VisionAgent selects one or more of these tools to complete the tasks outlined in your prompt.
  - This tool has been deprecated. Use Agentic Document Extraction instead.
  - https://github.com/landing-ai/ade-python
    - A Python library for interacting with the LandingAI Agentic Document Extraction REST API, designed for flexibility, reliability, clarity, and performance.

- https://github.com/deepdoctection/deepdoctection /3.1kStar/apache2/202603/python
  - https://deepdoctection.readthedocs.io/
  - https://huggingface.co/spaces/deepdoctection/deepdoctection
  - a Python library that orchestrates Scan and PDF document layout analysis, OCR and document and token classification. 
  - Build and run a pipeline for your document extraction tasks, develop your own document extraction workflow, fine-tune pre-trained models and use them seamlessly for inference.
  - Document layout analysis and table recognition in PyTorch with Detectron2 and Transformers, 
  - OCR with support of Tesseract, DocTr and AWS Textract, 
  - Text mining for native PDFs with pdfplumber, 
  - Deskewing and rotating images with jdeskew or Tesseract.
# extraction-office
- https://github.com/QuivrHQ/MegaParse /apache2/202408/python/inactive
  - https://pypi.org/project/megaparse/
  - a powerful and versatile parser that can handle various types of documents with ease
  - Parse PDFs, Docx, PPTx in a format that is ideal for LLMs
  - Files: ✅ PDF ✅ Powerpoint ✅ Word
  - Content: ✅ Tables ✅ TOC ✅ Headers ✅ Footers ✅ Images
# feat-elements

# feat-layout
- https://github.com/RapidAI/RapidLayoutRecover /apache2/202409/python
  - 针对文档类图像，整合版面分析、文字识别、表格识别和公式识别结果，还原版面布局信息。
  - 输入：文档类图像, 输出：TXT或Word
  - A[/文档图像/] --> B([文档方向分类 rapid_orientation]) --> C([版面分析 rapid_layout])

- https://github.com/muna-ai/nomic-layout /202604/python/ts
  - https://pdflayout.ai/
  - Web demo and agent skill for the Nomic Layout v1 document parsing model.
  - Empower your AI agents to find specific information in large, complex PDF documents using Nomic's layout model.
  - a web demo, allowing users to upload PDFs and ask questions. The web demo runs layout detection, OCR, text embeddings, and LLM-based generation directly in the browser
  - Ask your AI agent natural-language questions about your PDF documents and get precise, cited answers. The skill uses layout detection, OCR, and text embeddings to index every text region across your PDFs, then performs vector search to find the most relevant passages.
  - It works equally well with born-digital PDFs and scanned documents.
  - reading-pdf
    - layout detection
    - embedding
    - ocr: rapid-ocr
    - smol
  - 点击底部引用附件能显示原文pdf, 高亮引用所有chunk的bbox, 未能高亮具体的文本range
# examples
- https://github.com/PragmaticMachineLearning/docai /MIT/202409/python
  - Extract structured data from unstructured documents using Answer. AI's Byaldi, OpenAI gpt-4o, and Langchain's structured output.
  - 基于Answer. AI的Byaldi、OpenAI的gpt-4o和Langchain 做结构化数据输出
  - 支持从PDF等非结构化文档中提取结构化信息，比如损失历史记录、基本应用程序信息等
# utils

# more
