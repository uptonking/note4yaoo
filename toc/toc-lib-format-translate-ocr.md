---
title: toc-lib-format-translate-ocr
tags: [format, image, ocr, pdf, translation]
created: 2025-12-19T12:42:18.519Z
modified: 2025-12-19T12:43:21.150Z
---

# toc-lib-format-translate-ocr

# guide
- tips-ocr
  - 文档的使用频率不如图片, ocr/translation的方案要考虑图片场景
  - 批量执行ocr的架构可参考papermerge/paperless
  - vlm流式输出的方案配合编辑器流式构建内容的ux体验会很好

- tips-translations
  - 翻译类型产品的形态需要根据场景进行设计，可双栏/上下紧邻/点击切换原文和译文
# popular
- https://github.com/PDFMathTranslate-next/PDFMathTranslate-next /2kStar/AGPLv3/202512/python
  - https://pdf2zh-next.com/zh/index.html
  - PDF 科学论文翻译与双语对照。基于 BabelDOC
  - 🐛 翻译图片pdf的异常 'Translation error: Babeldoc translation error: The document contains no paragraphs 
  - [接入paddleocr vl呀 _202511](https://github.com/PDFMathTranslate-next/PDFMathTranslate-next/issues/285)
    - 要吃饭的，基于OCR翻译闭源搞了
  - [关于扫描版PDF & 图片的说明 _202508](https://github.com/PDFMathTranslate-next/PDFMathTranslate-next/issues/166)
    - 目前 BabelDOC 技术路线 暂无计划支持扫描版 PDF
    - 位图：方案仍在探索中，大概率会依赖闭源服务，优先级较低。
    - 矢量图：最新版本的 BabelDOC 已经可以识别并翻译图中的文字。
    - 不同 OCR 服务的输出格式差异较大，需要大量适配工作。
  - [支持pdf图片中文字翻译 _202507](https://github.com/PDFMathTranslate-next/PDFMathTranslate-next/issues/118)
    - 本项目不想接受涉及修改pdf的pr。修改pdf会有许多cornercase，我暂时没有精力维护。好心人想搞的话可以自行fork
  - [OCR功能不可用 _202506](https://github.com/PDFMathTranslate-next/PDFMathTranslate-next/issues/39)
    - 此功能是处理已ocr好的文件的，还请自行做一下ocr处理。
  - https://github.com/PDFMathTranslate/PDFMathTranslate-next /AGPLv3
    - pdf2zh 2.0 does not currently provide an online demo
- https://github.com/PDFMathTranslate/PDFMathTranslate /29.8kStar/AGPLv3/202511/python 
  - https://pdf2zh.com/
  - 基于 AI 完整保留排版的 PDF 文档全文双语翻译，支持 Google/DeepL/Ollama/OpenAI 等服务，提供 CLI/GUI/MCP/Docker/Zotero
  - Preserve formulas, charts, table of contents, and annotations
  - Support multiple languages, and diverse translation services.
  - ✨ 可参考翻译后pdf布局不变的实现方式, 特别是表格中英文变中文但布局不变
  - 支持双栏布局显示原文和翻译，体验非常好
  - 🐛 [supports ocr on scanned document ](https://github.com/PDFMathTranslate/PDFMathTranslate/issues/19)
    - 图片型的 PDF 文档暂时还没办法翻译，目前主要还是在优化电子书和论文的翻译效果
    - 对于扫描版的pdf文件的翻译效果咋样呢？ 压根不支持
    - sayura 就是 marker 的作者做的开源多国语言和表格的 OCR 模型，我只测试了 PaddleOCR 高精度模型，Sayura 效果比它好很多，而且支持多国语言效果很好。缺点就是 Sayura 对 GPU 显存要求有点高，头疼，不太会量化模型
    - 💡 扫描件可以直接理解为图片，实际上是保持排版的图片翻译功能，可以参考微信的实现，长按图片点翻译可以自动翻译
    - 👷 202505: 遇到此问题时，请尝试使用 2.0 预览版 并启用高级选项中的 OCR Workaround 来翻译。
  - [为什么会出现完全重影？ ](https://github.com/PDFMathTranslate/PDFMathTranslate/issues/942)
    - 重影用2.0，开ocr workaround就行
  - 🎯 [pdf2zh 2.0 _202502](https://github.com/PDFMathTranslate/PDFMathTranslate/issues/586)
    - Core: I am completely rewriting it, related code is at funstory-ai/BabelDOC
  - https://github.com/funstory-ai/BabelDOC /6.2kStar/AGPL/202512/python
    - https://funstory-ai.github.io/BabelDOC/
    - Yet Another Document Translator
    - Provides a simple command line interface.
    - Provides a Python API.
    - Mainly designed to be embedded into other programs, but can also be used directly for simple translation tasks.
    - 目前 BabelDOC 技术路线 暂无计划支持扫描版 PDF。
    - This project hopes to promote a standard pipeline and interface to solve the problem.
      - We offer an intermediate representation of the results from parser and can be rendered into a new pdf or other format. The pipeline is also a plugin-based system which everybody can add their new model, ocr, renderer, etc.
    - 📡 [请问会支持图片里内容的翻译吗 _202503](https://github.com/funstory-ai/BabelDOC/issues/179)
      - 会，还请耐心等待
    - [一个很奇怪的扫描件 ](https://github.com/funstory-ai/BabelDOC/issues/523)
      - 这个文件确实是比较奇怪，用wps office打开能选取到文字，但是放大500倍后能看到文字失真，想了解下babel doc判断扫描件的标准是啥
      - 判定依据是移除所有文本绘制指令后转图像 与原始页面的图像相似度>0.95就认为是扫描版页面。文件包含的扫描版页面>80%就判定文件为扫描版。
      - 此文件确实是扫描件。虽然他能复制文本（是个双层PDF），但是也是扫描件。 建议启用 auto-enable-ocr-workaround 功能。这样会在检测到扫描版时自动启用对应的workaround。
    - [部署 Babel DOC 到家用 NAS，PDF 自动翻译 _202504](https://zhuanlan.zhihu.com/p/1899886272828379973)
    - [科研论文翻译神器！BabelDOC：开源AI工具让PDF论文秒变双语对照，公式图表全保留 - 知乎](https://zhuanlan.zhihu.com/p/1892003359227089736)

- https://github.com/CBIhalsen/PolyglotPDF /2.1kStar/GPL/202509/python/js
  - A multilingual eBook processing tool supporting all eBook formats. 
  - Features online and offline translation while preserving original layouts.
  - Compatible with both scanned and digital PDFs. 
  - 目前效果，对于基于文本的pdf, polyglotpdf的解析方式依旧是最优解。 ocr和布局分析并不总是完美。
  - 对于报告型表格文档，polyglotpdf效果相当完美，当然表格中的复杂矢量数学公式依旧无法正确处理
  - 本项目采用与 Adobe Acrobat DC 编辑 PDF 类似的基本原理，基于 PyMuPDF 识别和处理 PDF 文本块, 这种方式直接处理 PDF 文本块，保持原有布局不变，实现高效的文本提取和修改
  - 🛝
    - 实测图片pdf在ocr后底部是原文, 文字散乱排布在上方, 视觉上是重影, 但分栏布局可以还原, 且识别后的每行文本和原文位置基本都一致
    - 💡🤔 更合理的流程是生成2个pdf image > text-pdf > translated-pdf, 这样就能既保持原有布局，又能无重影展示干净的译文pdf
  - [关于·ocr识别 ](https://github.com/CBIhalsen/PolyglotPDF/issues/6)
    - 请问考虑·添加·paddle作为OCR模型吗？ 文字PDF的翻译速度是我用过最快的，比pdfmathtran快几倍

- https://github.com/ocrmypdf/OCRmyPDF /32kStar/MPLv2/202512/python
  - http://ocrmypdf.readthedocs.io/
  - OCRmyPDF adds an OCR text layer to scanned PDF files, allowing them to be searched or copy-pasted.
  - Generates a searchable PDF/A file from a regular PDF
  - Distributes work across all available CPU cores
  - Uses `Tesseract` OCR engine to recognize more than 100 languages
  - Battle-tested on millions of PDFs.
  - https://github.com/ocrmypdf/OCRmyPDF-EasyOCR /MIT/python
    - This is plugin to run OCRmyPDF with the EasyOCR engine instead of Tesseract OCR, the default OCR engine for OCRmyPDF. 
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

- https://github.com/oomol-lab/pdf-craft /4.1kStar/AGPL > MIT/202512/python
  - https://pdf.oomol.com/
  - 将 PDF 文件转换为各种其他格式，本项目专注于处理扫描版书籍的 PDF 文件
  - 本项目基于 DeepSeek OCR 进行文档识别。支持表格、公式等复杂内容的识别。通过 GPU 加速，pdf-craft 能够在本地完成从 PDF 到 Markdown 或 EPUB 的完整转换流程。
    - 依赖 DeepSeek OCR 模型，首次运行时会自动从 Hugging Face 下载。
  - 从 v1.0.0 正式版开始，pdf-craft 全面拥抱 DeepSeek OCR，不再依赖 LLM 进行文本矫正。这一改变带来了显著的性能提升：整个转换流程在本地完成，无需网络请求，告别了旧版本中漫长的等待和偶发的网络失败。
  - Starting from the official v1.0.0 release, pdf-craft fully embraces DeepSeek OCR and no longer relies on LLM for text correction.
    - removing the previous AGPL-3.0 dependency, allowing the entire project to be released under the more permissive MIT license
    - Note that pdf-craft has a transitive dependency on `easydict` (LGPLv3) via DeepSeek OCR.
  - [PDF Craft：一个更懂技术的开源 PDF 转换工具 _202512](https://linux.do/t/topic/1322118)
    - 我们基于 DeepSeek-OCR 重写了一个转换引擎：pdf-craft
    - 更智能的布局还原：特别优化了双栏和图文混排，目标是转成 Markdown 或 EPUB 后，还能有接近纸质书的阅读体验。
    - 更完美的 LaTeX 公式支持：无论是行内公式还是独立公式，都能精准识别并还原
    - 本地免费跑（我们最推荐的）
  - https://github.com/oomol-lab/epub-translator
    - uses AI large language models to automatically translate EPUB e-books while 100% preserving the original book's format, illustrations, table of contents, and layout. 
# solutions/vendors
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

- https://github.com/tesseract-ocr/tesseract /71.5kStar/apache2/202512/cpp
  - https://tesseract-ocr.github.io/
  - Tesseract Open Source OCR Engine
  - Tesseract has unicode (UTF-8) support, and can recognize more than 100 languages "out of the box".
  - Tesseract supports various image formats including PNG, JPEG and TIFF.
  - Tesseract supports various output formats: plain text, hOCR (HTML), PDF, invisible-text-only PDF, TSV, ALTO and PAGE.
  - Tesseract was originally developed at Hewlett-Packard Laboratories Bristol UK in 1985. From 2006 until August 2017 it was developed by Google.

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

- https://github.com/datalab-to/surya /19kStar/GPL/202510/python
  - https://www.datalab.to/
  - OCR, layout analysis, reading order, table recognition in 90+ languages
  - Works with PDF, images, word docs, and powerpoints
  - Our model weights use a modified AI Pubs Open Rail-M license (free for research, personal use, and startups under $2M funding/revenue) and our code is GPL. 
  - I've included a streamlit app that lets you interactively try Surya on images or PDF files. 

- https://github.com/JaidedAI/EasyOCR /28.6kStar/apahce2/202409/python/cpp/inactive
  - https://www.jaided.ai/
  - Ready-to-use OCR with 80+ supported languages and all popular writing scripts including: Latin, Chinese, Arabic, Devanagari, Cyrillic, etc.
  - In case you do not have a GPU, or your GPU has low memory, you can run the model in CPU-only mode by adding gpu=False.

- https://github.com/junhoyeo/BetterOCR /597Star/MIT/202311/python/inactive
  - Better text detection by combining multiple OCR engines with LLM.
  - OCR Engines Currently supports EasyOCR (JaidedAI), Tesseract (Google), and Pororo (KakaoBrain).
- https://github.com/wolfmanstout/screen-ocr /apache2/202510/python
  - screen-ocr package makes it easy to perform OCR on portions of the screen
  - WinRT is a Windows-only backend that is very fast and reasonably accurate.
  - Tesseract is a cross-platform backend that is much slower and slightly less accurate than WinRT
  - EasyOCR is a very accurate but slow backend and only runs on Python 64-bit
# ocr
- https://github.com/AKSarav/pdfstract /apache2/202511/python/js
  - web application for converting PDFs to multiple formats using various state-of-the-art extraction libraries. Built with FastAPI backend and React frontend
  - [Built a small tool to compare PDF → Markdown libraries (for RAG / LLM workflows) : r/Rag _202507](https://www.reddit.com/r/Rag/comments/1m1j10e/built_a_small_tool_to_compare_pdf_markdown/)
    - I’ve been exploring different libraries for converting PDFs to Markdown to use in a Retrieval-Augmented Generation (RAG) setup.
    - But testing each library turned out to be quite a hassle — environment setup, dependencies, version conflicts, etc.
    - Currently, it supports: docling pymupdf4llm markitdown marker

- https://github.com/readur/readur /MIT/202512/rust/ts/Axum
  - Quick, painless, intuitive OCR platform written in Rust and TypeScript. 
  - Tesseract OCR for text extraction
  - Axum for the web framework
  - Drag-and-drop support for PDF, images, text files, and Office documents (DOCX, XLSX, DOC*)
  - Automatic text extraction using Tesseract and Office document parsing
  - WebDAV, Local Folders, and S3-compatible storage integration
  - Beautiful React frontend with Material-UI components and responsive design
  - Document tagging and categorization
  - OIDC Setup - Single Sign-On integration

- https://github.com/rdumasia303/deepseek_ocr_app /1.5kStar/MIT/202511/python/js
  - A quick vibe coded app for deepseek OCR
  - React frontend and FastAPI backend

- https://github.com/ihatecsv/deepseek-ocr-client /713Star/MIT/202510/python/js
  - A real-time Electron-based desktop GUI for DeepSeek-OCR
  - GPU acceleration (CUDA)
  - Flask backend manages the model, Electron frontend for the UI.
  - [A quickly put together a GUI for the DeepSeek-OCR model that makes it a bit easier to use : r/LocalLLaMA _202510](https://www.reddit.com/r/LocalLLaMA/comments/1ocx27p/a_quickly_put_together_a_gui_for_the_deepseekocr/)

- https://github.com/th1nhhdk/local_ai_ocr /apache2/202512/python/ts
  - An local, offline (after initial setup), portable OCR software that can process images and PDF files, using DeepSeek-OCR AI (running directly on your machine).
  - Queue system: Allows processing multiple files sequentially.

- https://github.com/fufankeji/DeepSeek-OCR-Web /202510/python/ts
  - a multimodal document parsing tool based on DeepSeek-OCR with React frontend and FastAPI backend.
- https://github.com/neosun100/DeepSeek-OCR-WebUI /MIT/202512/python/html
  - Ready-to-use DeepSeek-OCR Web U
  - v3.3 brings native Apple Silicon support, enabling Mac users to run high-performance OCR locally with: Native MPS Backend
  - 与 Knowledge-Base-Self-Hosting-Kit/streamdown 示例ui类似
  - https://github.com/newlxj/DeepSeek-OCR-Web-UI

- https://github.com/miaoxutao123/deepseek-ocr-translate /MIT/202511/python/ts/vue
  - 使用 DeepSeek-OCR 和 AI 模型实现 PDF 文档的准确翻译
  - 后台异步翻译，实时显示进度和结果，支持暂停/继续/停止
  - OCR 流程: PDF → 图片转换 → DeepSeek-OCR 识别 → 跨页句子合并 → 标签清理 → 存储
  - 翻译流程: 加载文本 → 智能分句 → 后台逐句翻译 → 应用纠错 → 实时显示 → 保存结果

- https://github.com/tmzncty/dots_ocr_suite /202512/python/js
  - 一个基于 DotsOCR 库开发的 OCR（光学字符识别）处理工具箱，包含 PDF 转 Word (DOCX) 的完整应用。
  - PDF 转 DOCX 转换器 (完整版): 自动进行拆图、OCR 识别、版面分析, 利用多核 CPU 并行处理，大幅提升长文档的转换速度, 实时进度：清晰展示拆图、识别、生成的每一个步骤进度, 支持下载 Word 文档 (.docx) 或包含 Markdown、JSON 数据的 ZIP 压缩包
  - 在“批量处理”标签页，您可以一次性拖入多个 PDF 文件。 自动排队：文件会自动进入队列逐个处理。您可以在下方列表中查看每个文件的实时进度

- https://github.com/Dogacel/deepseek-ocr-client-macos /MIT/202511/python/js
  - A real-time Electron-based desktop GUI for DeepSeek-OCR
  - [Dogacel/DeepSeek-OCR-Metal-MPS · Hugging Face](https://huggingface.co/Dogacel/DeepSeek-OCR-Metal-MPS)
    - This repository uses the weights from the original DeepSeek-OCR and modifies model to support MPS and CPU inference
- https://github.com/matica0902/MLX-Video-OCR-DeepSeek-Apple-Silicon /AGPL/202512/python/js
  - 影片/PDF/圖片 三合一 OCR, 專為 Apple Silicon 優化的全功能 OCR 解決方案

- https://github.com/Cross2pro/DeepSeek-OCR-Dashboard /202512/python/ts/vue
  - FastAPI + Vite/Vue wrapper around the DeepSeek-OCR model for quick local testing.
  - Progress visualization during uploads/inference so you know it’s working.
  - Bounding-box overlay for layout/annotation visualization.

- https://github.com/benedict2310/DeepSeekOCR-Cli /202511/python
  - A quick test to get deepseek ocr to run on a Mac with either images or pdfs
  - Runs natively on Apple Silicon (M1-M4) using PyTorch MPS acceleration
  - https://github.com/r-uben/deepseek-ocr-cli
    - CLI tool for OCR using DeepSeek-OCR model via Ollama. Local processing with zero cloud dependencies.
  - https://github.com/wcpsoft/deepseek-ocr-cli /apache2/202511
    - 基于 DeepSeek-OCR 项目改造，提供了增强功能，增加了对多种文档格式的支持，包括 Word、PPT、Excel 等，并提供统一的命令行接口和Web界面进行处理。
    - 双引擎支持：支持vLLM和Transformers两种推理引擎
    - 模块化架构：采用工厂模式设计，vLLM和Transformers引擎解耦，易于扩展和维护
    - 为了支持办公文档格式转换（Word、PPT、Excel等），需要安装LibreOffice
  - https://github.com/benedict2310/DeepSeekOCR-Cli /202511/python
    - Offline OCR and hybrid search for images and PDFs on macOS (Apple Silicon).

- https://github.com/Moskize91/doc-page-extractor /MIT/202512/python
  - Document page extraction tool powered by DeepSeek-OCR.
  - This package requires PyTorch with CUDA support (GPU Required).

- https://github.com/ikantkode/hunyuan-1b-ocr-app /202511/python
  - [HunyuanOCR-1B - Dockerized Streamlit OCR App - Quite Amazing. : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1p6wios/hunyuanocr1b_dockerized_streamlit_ocr_app_quite/)
  - https://github.com/neosun100/HunyuanOCR-WebUI /apahce2/python
    - 基于腾讯混元OCR的完整Web界面解决方案
    - This project uses Gradio to build the web interface and supports one-click Docker deployment

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

- https://github.com/atorhub/anj-dual-ocr-parser /202512/js
  - https://atorhub.github.io/anj-dual-ocr-parser/
  - Advanced client-side invoice OCR, parsing, export, and history system — powered entirely by browser technologies, no backend required.
  - ANJ Dual OCR Parser — AI-powered invoice/bill extractor featuring dual-pass OCR (quick + enhanced), smart parsing, automatic field detection, and multi-format export (JSON, CSV, XLSX, PDF, ZIP)
  - Tesseract.js, IndexedDB, html2canvas, jsPDF
  - If Image → processed with Tesseract.js

- https://github.com/am009/LLM-online-tool /202512/python/js
  - http://tool.latexdiff.cn/
  - 基于大语言模型（LLM）API的 Markdown/Latex 文章翻译工具
  - 逐段翻译与校对：点击蓝色箭头按钮即可翻译当前段落，然后可以在右侧实时编辑，
  - 纯静态网页：完全在浏览器中运行
  - 分块翻译：将 Markdown 内容分割为可管理的段落进行翻译
  - 问：为什么没有按照我想要的方式分割段落？段落分割方式是什么？
    - 答：根据 “连续的两个换行” 分割段落。只有空格和tab的行也看作单独的空行。
  - https://github.com/am009/dots.ocr
    - 本Fork提供Docker容器重新封装的API，支持20系等旧的 Turing GPU，以float32格式运行。测试机型：单2080ti 22GB。

## utils-ocr

- https://github.com/anonNo2/deepseek-ocr-server /202511/python
  - 使用Deepseek-OCR 的异步并发pdf处理服务
  - Asynchronous Processing - Non-blocking task queue with status tracking

- https://github.com/CatchTheTornado/text-extract-api /3kStar/MIT/202512/python
  - https://demo.doctractor.com/
  - Convert any image, PDF or Office document to Markdown text or JSON structured document with super-high accuracy, including tabular data, numbers or math formulas.
  - The API is built with FastAPI and uses Celery for asynchronous task processing. Redis is used for caching OCR results.
  - No Cloud/external dependencies all you need: PyTorch based OCR (EasyOCR) + Ollama are shipped and configured via docker-compose no data is sent
  - PDF/Office to Markdown conversion with very high accuracy using different OCR strategies including llama3.2-vision, easyOCR, minicpm-v, remote URL strategies including marker-pdf
  - LLM Improving OCR results LLama is pretty good with fixing spelling and text issues in the OCR text
  - Distributed queue processing using Celery
  - Storage Strategies switchable storage strategies (Google Drive, Local File System ...)
  - CLI tool for sending tasks and processing results

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

- https://github.com/yigitkonur/llm-based-ocr /876Star/AGPL/202511/python
  - High-accuracy PDF-to-Markdown OCR API using LLMs with vision capabilities.
  - Parallel Processing: Multi-page PDFs in seconds
  - Accept a PDF file upload OR a URL to a PDF. Returns beautifully formatted Markdown.
  - This project uses `PyMuPDF` for PDF processing, which requires the GNU AGPL v3.0 license.

- https://github.com/fufankeji/vllm-ocr-server /202511/python/ts
  - multimodal OCR system built with LangChain 1.0 and vLLM. 
  - Integrates MinerU, PaddleOCR‑VL, and DeepSeek‑OCR with a unified REST API and frontend UI
  - Unified parsing interface: pluggable selection of MinerU, PaddleOCR‑VL, and DeepSeek‑OCR
  - Batch parsing: supports batch processing for PDFs and images; auto-splits multi‑page documents
  - Standardized outputs: unified format with Markdown/JSON and image exports
  - Multimodal support: extract text, tables, formulas, images, and more

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

- https://github.com/jbaiter/ocr-parser /MIT/202309/ts
  - This library provides a simple interface to parse OCR data from a stream, buffer or string. 
  - It does not rely on any DOM APIs and can therefore be used in contexts where there is no built-in support for XML parsing, most notably in Web Workers and Service Workers.
  - Currently the library supports hOCR and ALTO OCR markup.

- https://github.com/athrael-soju/Snappy /66Star/MIT/202512/python/ts
  - Snappy implements region-level document retrieval by unifying vision-language models with OCR through spatial coordinate mapping. 
  - Unlike traditional systems that return entire pages (VLMs) or lack semantic grounding (OCR-only), Snappy uses ColPali's patch-level similarity scores as spatial relevance filters over OCR-extracted regions; operating entirely at inference time without additional training.

- https://github.com/Qianxia666/ocr /GPL/202511/python
  - 利用 OpenAI API 进行图片和 PDF 文档的 OCR 识别，支持异步任务处理、实时通信和完整用户机制的任务管理系统。

- https://github.com/Fusyong/recover-layout-from-ocr /202509/python/inactive
  - PDF OCR Utils and Examples, especially for workbook text extraction, layout recovery, and conversion to Markdown.
  - 使用PyMuPDF进行PDF转换为图片
  - 使用RapidOCR进行OCR识别
  - 将OCR结果转换为文本行，过滤不需要的box和row
    - 兼容 有道OCR/pymupdf/RapidOCR 的JSON格式
  - 给文本行中的标题标出Markdown标记
  - 保存为jpg后OCR效果比png好，不知何故

## utils-tesseract

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

- https://github.com/robertknight/tesseract-wasm /349Star/BSD/202510/ts/wasm
  - https://robertknight.github.io/tesseract-wasm/
  - A WebAssembly build of the Tesseract OCR engine for use in the browser and Node.
  - Using WebAssembly SIMD when available (Chrome >= 91, Firefox >= 90, Safari >= 16.4) to improve text recognition performance.
  - 在线示例可输出 文本 和 hocr的html
# translation
- https://github.com/aikilan/Babel-Markdown /MIT/202511/ts
  - provides real-time translation previews for VS Code, synchronizing the original Markdown and AI-translated content in a single view to help you efficiently proofread multilingual documents.
  - Progressive translation preview: streams segments as they finish translating.
  - Markdown fidelity: preserves headings, lists, tables, and code blocks exactly.
  - OpenAI-compatible API support: customize base URL, model, language, and timeout for any compatible provider.

- https://github.com/ogkalu2/comic-translate /2.3kStar/apache2/202512/python
  - Desktop app for automatically translating comics - BDs, Manga, Manhwa, Fumetti and more in a variety of formats (Image, Pdf, Epub, cbr, cbz, etc) and in multiple languages.
  - Many Automatic Manga Translators exist. Very few properly support comics of other kinds in other languages. This project was created to utilize the ability of State of the Art (SOTA) Large Language Models (LLMs) like GPT-4 and translate comics from all over the world.

- https://github.com/meangrinch/MangaTranslator /apache2/202512/python/Gradio
  - Web application for automating the translation of manga/comic page images using AI. 
  - Targets speech bubbles and text outside of speech bubbles. 
  - Supports 54 languages and custom font pack usage.
  - Speech bubble detection, segmentation, cleaning (YOLO + SAM 2.1)
  - LLM-powered OCR and translations (supports 54 languages)
  - Upscaling (2x-AnimeSharpV4)
  - Two interfaces: Web UI (Gradio) and CLI

- https://github.com/huangusaki/PicLingo /MIT/202512/python
  - AI-powered image translator with visual editing - Transform images with intelligent OCR and translation
  - 智能 OCR 与翻译：基于大语言模型的文字识别与翻译
  - 可视化编辑器：选中、移动、缩放、旋转文本块
  - 依赖PyQt6、Pillow

- https://github.com/zyddnys/manga-image-translator /9.1kStar/GPL/202512/python
  - https://cotrans.touhou.ai/
  - 一键翻译各类图片内文字
  - This project aims to translate images that are unlikely to be professionally translated, such as comics/images on various group chats and image boards, making it possible for Japanese novices like me to understand the content
  - It mainly supports Japanese, but also supports Simplified and Traditional Chinese, English and 20 other minor languages.
  - https://github.com/hgmzhn/manga-translator-ui /GPL/python/js
    - 一款开源的漫画翻译工具，基于 manga-image-translator 核心引擎开发。支持日漫、韩漫、美漫的自动翻译，提供 5 种翻译引擎（包括 OpenAI、Gemini 等 AI 翻译），内置可视化编辑器可自由调整文本框和样式。

- https://github.com/dmMaze/BallonsTranslator /4.4kStar/GPL/202512/python
  - 深度学习辅助漫画翻译工具，支持一键机翻和简单的图像/文本编辑
  - 译文回填参考对原文排版的估计，包括颜色，轮廓，角度，朝向，对齐方式等
  - 最后效果取决于文本检测，识别，抹字，机翻四个模块的整体表现
  - 英译中，日译英排版已优化，文本布局以提取到的背景泡为参考，中文基于 pkuseg 进行断句，日译中竖排待改善
  - 本项目重度依赖 `manga-image-translator`，所有 mit 模型来自 manga-image-translator，支持日英汉识别和颜色提取
- https://github.com/MashiroSaber03/Saber-Translator /GPL/202512/python/js
  - AI 漫画/图像翻译与编辑神器，支持多种模型、手动标注、精细编辑、会话管理和插件扩展
  - 移植自 manga-image-translator 项目 只保留模型推理核心逻辑

- https://github.com/Bistutu/FluentRead /6.2kStar/GPL/202509/ts/vue/inactive
  - https://fluent.thinkstu.com/
  - 开源的沉浸式翻译，一款革命性的浏览器翻译插件
  - 支持 20+ 种翻译引擎，包括传统翻译和 AI 大模型。如：微软翻译、谷歌翻译、DeepL翻译、OpenAI、DeepSeek、Kimi、Ollama、自定义引擎等。
  - 支持原文与译文并列显示，让阅读更轻松。
  - 所有数据本地存储，代码开源透明。
  - 支持chrome/edge/firefox
- https://github.com/mengxi-ream/read-frog /GPL/202512/ts
  - https://readfrog.app/
  - 陪读蛙 - 开源沉浸式翻译

- https://github.com/PantsuDango/Dango-Translator /8.3kStar/LGPL > close/202510/python
  - https://translator.dango.cloud/
  - 基于OCR的生肉翻译软件
  - 通过OCR识别屏幕特定范围内的文字，然后将识别到的文字调取各种翻译源，并实时输出翻译结果。
  - 配置有常规翻译、在线AI翻译、本地AI翻译
  - 另有图片翻译功能, 实现对生肉漫画图片自动识别、翻译、消字、嵌字
  - 自 4.5.8 版本后, 团子翻译器换成了 Golang 完全重构了，因为完全换语言重写了，因此 Python 版本的代码不再更新。
  - PaddleOCR 在线&本地OCR均基于此框架搭建
  - QPT打包工具 本地OCR基于此工具打包
  - [软件是否已经不再开源? 核心文件停留在4.5.8版本 _202510](https://github.com/PantsuDango/Dango-Translator/issues/175)
    - 4.5.8之后没再开源是因为，换成Go语言完全重构了，所以没把后面的放上来。4.5.8是python版本的最后一个版本

- https://github.com/nextai-translator/nextai-translator /24.8kStar/AGPL/202512/ts/rust
  - 基于 ChatGPT API 的划词翻译浏览器插件和跨平台桌面端应用

## utils-translation

- https://github.com/mozilla/firefox-translations
  - a webextension that enables client side translations for web browsers.
  - 不支持中文
  - [Support Chinese translations](https://github.com/mozilla/firefox-translations/issues/583)

- https://github.com/jelmervdl/translatelocally-web-ext
  - https://translatelocally.com/
  - a web-extension that enables client side in-page translations for web browsers.
  - 不支持中文
  - Differences from Firefox Translations
    - Uses models from https://github.com/browsermt/students
    - Translation engine and memory is shared among all tabs and webpages
  - [Google Chrome](https://github.com/jelmervdl/translatelocally-web-ext/issues/10)

- https://github.com/Byaidu/PDFMathTranslate
  - 一款可以保留原排版的PDF文档翻译工具：PDFMathTranslate，可以完整保留原文档中的公式、图表，支持双语对比
  - 支持多种翻译服务，Google、DeepL、Ollama、OpenAI等

- 使用Google翻译（Translate）的离线翻译功能？有前提：你必须先在联网状态下将需要且支持离线翻译的语言下载。
  - 而离线翻译的结果会与联网翻译的结果存在结果差距。特别是翻译同一个字词语句下

- 全文翻译比较期待类似firefox做的这种离线本地翻译
  - [Firefox Translations – Get this Extension for 🦊 Firefox (en-US)](https://addons.mozilla.org/en-US/firefox/addon/firefox-translations/)

## translate-api/server

- https://github.com/kanweiwei/translate-server
  - 对接的是百度翻译api，需要 appid 和对应的密钥

- https://github.com/xxnuo/MTranServer /3.7kStar/apache2/202512/go/ts
  - 一个超低资源消耗超快的离线翻译服务器，无需显卡。单个请求平均响应时间 50 毫秒。支持全世界主要语言的翻译。
  - 主要是面向服务器使用环境，所以目前只有命令行服务和 Docker 部署，之后有空会完善 MTranDesktop 供桌面端使用。

- https://github.com/LibreTranslate/LibreTranslate /13.3kStar/AGPL/202512/python
  - https://libretranslate.com/
  - Open Source Machine Translation API, entirely self-hosted. 
  - its translation engine is powered by the open source Argos Translate library.
  - 依赖flask

- https://github.com/argosopentech/argos-translate /5.3kStar/MIT/202510/python
  - https://www.argosopentech.com/
  - Open-source offline translation library written in Python
  - Argos Translate uses OpenNMT for translations and can be used as either a Python library, command-line, or GUI application. 
  - 支持中日韩
# examples
- https://github.com/xushengfeng/eSearch /6.2kStar/GPLv3/202512/ts
  - https://esearch-app.netlify.app/
  - 截屏+OCR+搜索+翻译+贴图+屏幕翻译+以图搜图+滚动截屏+录屏
  - eSearch 是Information-portal的:electron: 重写版(顺便加了亿些功能)
  - 主要是想在 Linux 上(win 和 mac 上也能用)实现锤子大爆炸或小米传送门这样的屏幕搜索功能，当然也是一款方便的截屏软件。
  - 截屏 离线OCR 搜索翻译 以图搜图 贴图 录屏 滚动截屏 
  - 本地 OCR 由`PaddleOCR`的模型提供支持。

- https://github.com/001kenji/document-ai-translator /apache2/202507/js/inactive
  - https://document-ai-translator.netlify.app/
  - An AI-powered document translation tool that converts text from images or PDFs into multiple languages with high accuracy using OCR and advanced machine translation.
  - Tesseract.js-based text extraction
  - Real-time preview of extracted text
  - 提取出的text放在一个普通textarea中, 体验不是很好
  - 上传图片/pdf后，手动点击 extract/translate 按钮来执行操作

- https://github.com/adiKhan12/PDF-AnnotateAI /CC-NC/202507/js/inactive
  - Advanced browser-based PDF annotation tool with AI capabilities. 
  - Features drawing tools, text annotations, translation, summarization, OCR for scanned documents, and responsive design. 
  - Built with HTML, CSS, and JavaScript, and leveraging the PDF.js library for rendering and jsPDF for generating PDF documents.
  - OCR for scanned documents (via Tesseract.js)
  - Docker support for easy deployment and consistency

- https://github.com/Crivella/ocr_translate /GPL/202509/python
  - Django based web server for running OCR + Translation of incoming images
  - This is a Django app for creating back-end server aimed at performing OCR and translation of images received via a `POST` request.
  - The server is designed to be used together with this browser extension, acting as a front-end providing the images and controlling the languages, models and plugins being used.
  - The server is designed to only offer the basic functionalities, while the models that can be used and how they are used are defined by plugins.
  - Different plugins will make different types of models available:
    - BOX Model: EasyOcr, PaddleOCR
    - OCR Model: PaddleOCR, Tesseract, HuggingFace
    - Translation Model: HuggingFace, GoogleTranslate, Ollama
  - https://github.com/Crivella/ocr_extension /GPL/202509/js
    - Firefox browser extension for running in-place translation of images in an active tab

- https://github.com/aayushmishramechatronics/ocr-translator /MIT/202506/ts
  - https://image-text-extractor-seven.vercel.app/
  - An API based Image-to-Text Converter and Translator Website. 
  - Extract Text from Images and Translate it into any Language of your Convenience
  - Create a Google Cloud Project: Enable Cloud Vision/Translation API

- https://github.com/boysugi20/python-image-translator /202506/python/cli/inactive
  - This project utilizes optical character recognition (OCR) and translation to translate text within images from one language to another. 
  - The project extracts text and its bounding boxes from input images using the `EasyOCR` library.
  - Translation: It translates the extracted text using the Google Translator API.
  - Text Replacement: The translated text is then overlaid onto the image, replacing the original text while maintaining its position and style.
  - Output: Finally, the modified image with translated text is saved to an output folder.
- https://github.com/marcostolosa/OCRack /MIT/202509/python/cli
  - Advanced PDF translation engine with OCR capabilities, intelligent chunking, and automated image extraction/reinsertion.
  - Default Behavior: Automatic image extraction + translation + PDF generation
  - Rich UI: Professional terminal interface with detailed progress tracking
  - Tesseract OCR

- https://github.com/KuoCT/BeeSeeR /GPL/202508/python/inactive
  - A versatile OCR and LLM-powered GUI tool for instant text extraction, translation, and interaction.
  - 支援多語言 OCR：整合 Surya OCR（90+ 種語言）、Manga OCR（日文漫畫專用）、 Google Vision API（輕量雲端辨識），靈活應對不同需求
  - 依赖pyautogui
  - PyAutoGUI通过Tkinter实现了4种纯Python的消息弹窗函数，和JavaScript类似

- https://github.com/SystemVll/Montscan /202511/python
  - https://systemvll.github.io/Montscan/
  - Automated scanner document processor with OCR, AI-powered naming, and Nextcloud integration.
  - FTP Server - Receives documents from network scanners
  - Async Processing Queue - `ThreadPoolExecutor` with worker pool for non-blocking uploads
  - SHA256 checksum tracking in SQLite to prevent duplicate processing
  - Extracts text from scanned PDFs using Tesseract
  - Automatically uploads processed documents via WebDAV
  - Easy deployment with Docker Compose
  - Configure your network scanner to send scans via FTP

- https://github.com/Paullllllllllllllllll/ChronoTranscriber /MIT/202511/python
  - A Python-based tool for researchers and archivists to transcribe historical documents from PDFs, EPUB ebooks, or image folders. 
  - ChronoTranscriber supports multiple AI providers (OpenAI, Anthropic, Google, OpenRouter) via LangChain, local OCR with Tesseract, and provides structured JSON outputs with scalable batch processing for large-scale document digitization projects.
  - designed to integrate with ChronoMiner and ChronoDownloader for a complete historical document retrieval, transcription, and data extraction pipeline.
  - https://github.com/Paullllllllllllllllll/ChronoDownloader /MIT
    - A Python tool for discovering and downloading digitized historical sources from 14+ major digital libraries worldwide
  - https://github.com/Paullllllllllllllllll/ChronoMiner /MIT
    - ChronoMiner leverages multiple LLM providers through LangChain with schema-based extraction to transform unstructured text into well-organized, analyzable datasets in multiple formats (JSON, CSV, DOCX, TXT).

- https://github.com/Max-Lee-explore/agentic-ai-translation-company /CC-NC/202511/python/js
  - Agentic AI Translation System with Specialized Translators and Editors
  - Specialized Translation Agents: 不同类型的内容翻译所用大模型配置不同，特别是temperature
# proofreading
- tips
  - 校对的流程和交互可参考code review的现有工具的最佳实践

- https://github.com/chrisgrieser/obsidian-proofreader /30Star/MIT/202512/ts
  - AI-based proofreading and stylistic improvements for your writing. 
  - Changes are inserted as suggestions directly in the editor, similar to suggested changes in word processing apps.
  - Suggested changes are inserted directly into the text: Additions as ==highlights== and removals as ~~strikethroughs~~.
  - https://github.com/lucasmelin/red-pen /MIT/202308/ts/inactive
    - Red Pen is implemented as a retext-based plugin for the Obsidian note-taking app.
    - Red Pen acts as a proofreader for your writing.
    - It highlights phrases that could use simplifying, identifies weasel words, hedges, filler, and many more.
  - https://github.com/SahandMalaei/ai-writing-tools-obsidian /GPL/202511/ts
    - A suite of AI-powered writing tools for Obsidian, including dictionary lookup, proofreading, and context-aware explainer
    - 交互在弹窗

- https://github.com/CZ600/AutoDocxProofread /MIT/202511/ts/vue
  - 基于大模型的文档校对软件
  - 基于 Electron、Vue 3 和 TypeScript 构建的智能长文档校对桌面应用程序
  - 检测 Word 文档中的错别字、标点符号错误、语法问题和文本一致性问题，并提供修改建议。
  - 采用了并行处理架构，显著提升大模型处理长文档的速度。新版本引入了本地知识库功能，支持RAG功能给模型校对参考
  - Electron + Vue 3 + Element Plus + LanceDB(vector)
  - 文档处理：Mammoth + Docxtemplater
  - 多种校对模式：
    - 逐句精校：适合需要高精度校对的短文本
    - 逐段校正：适合长篇文献的校对
  - 支持PDF、word和txt文档导入作为参考材料
  - 兼容openai接口，支持多种大语言模型 API
  - 软件会将校对的结果显示在右边栏，并在文本中高亮展示，以方便查看。然后可以选择是否接受这些修改，可以导出接受修改后的文档
  - https://github.com/woniu9524/book-proofreading /202211/js/inactive
    - [校对工具使用文档](https://www.yuque.com/woniu-avesf/tvyxhx/sg007f)
    - 针对古籍的古籍校勘的工具；也可以用于普通的文本的校勘
    - Vue3+Electron+lowdb+express+element plus
    - 要命，烂代码太多，加新需求时候要崩溃了
    - 上传支持txt和docx两种格式,第一次上传的是底稿，第二次上传的是校对稿

- https://github.com/jack91620/AI-DocProofreader /MIT/202507/python/inactive
  - 一个基于AI的中文文档校对工具，支持Microsoft Word文档的智能校对和修正。
  - docx文档处理: 支持读取和写入Microsoft Word文档
  - AI智能校对: 使用大语言模型进行语法、错别字、术语检查
  - ✨ 多种校对模式: 支持批注、修订、跟踪更改和增强模式
  - 专业领域优化: 针对计算机领域术语特别优化
  - 配置管理: 支持自定义校对规则和术语词典

- https://github.com/Inc44/CoFlu /MIT/202512/js
  - https://inc44.github.io/CoFlu/
  - CoFlu is a powerful text manipulation, generation, and comparison tool. It's designed for tasks like proofreading, editing, content creation, version control, and ensuring text consistency. 
  - As of February 2025, CoFlu is the only website offering Microsoft Word (.docx) translation that fully preserves the original document's layout (fonts, styles, tables, images, and other elements) while using LLMs for superior translation quality.
  - File Upload: Supports .epub, .txt, .html, .htm, .css, .xml, .json, and .docx.
  - Calculates Levenshtein distance and percentage differences.
  - Diff Views: Single-column (insertions/deletions highlighted) or double-column (side-by-side).
  - Converts Markdown to HTML, including math (KaTeX or MathJax).
  - Upload & Translate . DOCX, CoFlu maintains the exact original formatting (fonts, styles, tables, images), Download Translated . DOCX
  - Local Storage: Saves text, chat, API keys, settings, and custom prompts in your browser.

- https://github.com/not-implemented/hocr-proofreader /101Star/MIT/201701/js/NoDeps/inactive
  - http://www.not-implemented.de/hocr-proofreader/
  - Web based JavaScript GUI library for proofreading/editing hOCR.
  - Two view concept: Original layout vs. hOCR text – linked together (i.e. hovering words etc. on both sides)
  - Pure JavaScript without dependencies just using current browser features
- https://github.com/milahu/hocr-editor-qt /MIT/202510/python
  - graphical HOCR editor to produce minimal diffs for proofreading of tesseract OCR output

- https://github.com/onderceylan/proofly /MIT/202511/ts
  - Private AI Writing, Proofreading & Grammar Assistant
  - Your privacy-first writing assistant powered by Chrome on-device AI
  - open-source Chrome extension that brings professional-grade writing assistance directly to your browser—without compromising your privacy
  - Unlike cloud-based alternatives like Grammarly, LanguageTool, or QuillBot, Proofly uses Chrome's Built-in AI APIs to proofread your writing entirely on-device

- https://github.com/Fusyong/editor-assistant /202510/ts/inactive
  - AI辅助图书编辑工具
  - 一个基于VSCode扩展的多智能体AI应用，专门用于辅助编辑人员整理、编辑、校对图书稿件。
  - 支持批量处理多个Markdown章节文件
  - 本地AI模型：使用Ollama本地模型
  - 前端：VSCode扩展 + TypeScript
- https://github.com/Fusyong/ai-proofread-vscode-extension /MIT/202512/ts
  - 一个用于文档和图书校对、基于大语言模型服务的VS Code扩展，支持选中文本直接校对和长文档切分后批量校对两种工作流，并集成了一些跟校对相关的辅助功能
  - [大语言模型校对工具AI Proofreader - 嬉戏实验室](https://blog.xiiigame.com/2025-12-07-%E5%A4%A7%E8%AF%AD%E8%A8%80%E6%A8%A1%E5%9E%8B%E6%A0%A1%E5%AF%B9%E5%B7%A5%E5%85%B7AI%20Proofreader%EF%BC%9A%E7%BC%96%E8%BE%91%E5%88%9B%E6%96%B0%E5%B7%A5%E4%BD%9C%E4%BB%8B%E7%BB%8D/)
  - 本扩展与相应的Python校对工具库的功能大致相同。
  - https://github.com/Fusyong/ai-proofread /
    - 一个校对中文书稿的工具集。
    - 主要功能是使用Deepseek、阿里云百炼和Google Gemini（后者测试不充分）平台的大语言模型服务，对文本进行一般语言文字和知识性校对。该主要功能、更新的功能已经做成vscode插件： ai-proofread-vscode-extension
    - 直接使用vscode提供的比较工具，视觉清晰，操作方法。唯一的缺陷是无法保存为文档，作为审稿记录。
    - PyMuPDF转换: pymupdf2md.py - 基于PyMuPDF的PDF转Markdown工具
  - [比较AI模型用于中文校对的效果 - 嬉戏实验室 _202502](https://blog.xiiigame.com/2025-02-07-%E6%AF%94%E8%BE%83AI%E6%A8%A1%E5%9E%8B%E6%A0%A1%E5%AF%B9%E6%95%88%E6%9E%9C/)
    - 最近这一年，我用生成式大语言模型校对了4本书稿，以及一些短篇文字。其间常用几个固定的文段来测试各模型，以选用效果最好的。
    - Deepseek推出V3后用V3，其中文知识超过了Claude 3.5 sonnet。同时我也发现，谷歌的预览版Gemini 2.0 Pro与它不相上下，但速度比较慢
    - 推理类模型的校对效果通常不佳，未作测试；在某些专项校对中也许值得尝试。
    - 在以上测试中，gemini-2.0-pro-exp-02-05有明显优势，改正的知识性错误、文字性错误最多，优化处也相当有益，没有误改和冗余输出。老实说，就通常所能投入的精力而言，它肯定比我改得好很多。
    - deepseek v3对指令的遵守度稍差。claude-3.5-sonnet-20241022也有错误转换引号这个老问题，此外还是比较遵守指令的。
    - 以上测试自然是相当片面的。但参考以往经验，在用于中文校对这个使用场景中，我觉得结果还是蛮有参考价值。
  - https://github.com/Fusyong/compare-image /python
    - 一个用于比较两组图像差异的 Python 工具，特别适用于图书文档页面的比较。
    - 该工具提供了多种比较模式，可以帮助用户快速发现图像之间的差异。
    - 像素比较：直接比较两张图片的像素差异
    - 叠置比较：将两张图片叠加显示，支持透明度调节
    - OCR文字比较：识别并比较图片中的文字内容，生成差异报告
    - 使用 OpenCV 进行图像处理
    - 使用 RapidOCR 进行文字识别
    - 使用 Tkinter 构建图形界面
    - 使用 NumPy 进行数值计算
  - https://github.com/Fusyong/LLM-prompts-from-a-book-editor
    - 提示词，主要跟教育图书编辑、出版相关

- https://github.com/Everydaaaaaaaaaaaaaaay/Auto-proofread /202510/python
  - 这是一个双语翻译校对项目。可以将复杂的，不规则的双语文本对齐，并借助AI进行校对，最后自由选取是否应用AI的校对建议，生成导出正确的、整齐的文本。
  - 示例的输入输出都是纯文本txt

- https://github.com/apanly/proofreadv1 /201309/python/inactive
  - 中文文本自动纠错

- https://github.com/nalgeon/vscode-proofread /MIT/202511/js
  - This extension offers Proofread, Translate and Check Grammar commands in VS Code. 
  - It's a simple alternative to DeepL, Grammarly, and other similar tools.
  - Uses Copilot, Ollama, or OpenAI for proofreading.
# spellchecking
- https://github.com/languagetool-org/languagetool /13.6kStar/LGPL/202509/java
  - https://languagetool.org/
  - Open Source proofreading software for English, Spanish, French, German, Portuguese, Polish, Dutch, and more than 20 other languages

- https://github.com/sonnyp/Eloquent /183Star/GPL/202512/js
  - Eloquent is a proofreading software for English, Spanish, French, German, Portuguese, Polish, Dutch, and more than 20 other languages.
  - It works fully offline, powered by LanguageTool standalone server.
# more
- https://github.com/leplusorg/docker-pdf /apache2/202512/docker
  - Multi-platform Docker container with utilities to process PDF files (pdftk, ghostscript, ocrmypdf, pdfgrep, qpdf...).

- https://github.com/scambier/obsidian-text-extractor /GPL/202512/ts
  - A (companion) plugin to facilitate the extraction of text from images (OCR) and PDFs.
  - I unfortunately can't dedicate much time anymore on Text Extractor. It's mostly feature-complete
  - https://github.com/MohrJonas/obsidian-ocr
  - https://github.com/diegomarzaa/pdf-ocr-obsidian
