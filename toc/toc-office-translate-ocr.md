---
title: toc-office-translate-ocr
tags: [image, ocr, pdf, translation]
created: 2025-12-19T12:42:18.519Z
modified: 2026-04-07T11:52:43.122Z
---

# toc-office-translate-ocr

# guide

- tips-translations
  - 翻译类型产品的形态需要根据场景进行设计，可双栏/上下紧邻/点击切换原文和译文
  - mt llm comparison/playground
# popular
- https://github.com/xunbu/docutranslate /747Star/MPLv2/202601/python
  - 文档（小说、论文、字幕）翻译工具（支持 pdf/word/excel/json/epub/srt...）
  - 基于大语言模型的轻量级本地文件翻译工具
  - Support Multiple Formats: Translates pdf, docx, xlsx, md, txt, json, epub, srt, ass, and more
  - PDF Table, Formula, Code Recognition: Leverages `docling` and `mineru` PDF parsing engines
  - 自动生成术语表：支持自动生成术语表实现术语的对齐。
  - JSON Translation: Supports specifying values to translate within JSON using paths (jsonpath-ng syntax).
  - Supports docx and xlsx files (currently does not support doc or xls) while maintaining original formatting.
  - 异步支持：专为高性能场景设计，提供完整的异步支持，实现了可以多任务并行的服务接口
  - 局域网、多人使用支持：支持在局域网中多人同时使用。
  - Provides an out-of-the-box Web UI and RESTful API for easy integration and usage.
  - Windows and Mac portable packages under 40MB (versions that do not use docling for local PDF parsing).
  - 👀 在翻译pdf时会先转换为markdown，这会丢失原先的排版，对排版有要求的用户请注意
  - 对于希望快速上手的用户，我们在 GitHub Releases 上提供整合包。
    - DocuTranslate: 标准版，使用 minerU（在线或本地部署）解析PDF文档，支持调用本地部署的 minerU API
    - DocuTranslate_full: 完整版，内置 docling 本地PDF解析引擎，无需 minerU 即可进行离线PDF解析时选择此版本
  - DocuTranslate 使用 工作流 (Workflow) 系统，每个工作流都是针对特定文件类型的完整翻译管道。
    - 根据文件类型选择工作流, 配置工作流（LLM、解析引擎、输出格式）, 执行翻译,保存结果
  - 如果您选择 mineru作为文档解析引擎（convert_engine="mineru"），则需要申请一个免费的 Token
    - 如果您选择 docling 作为文档解析引擎（convert_engine="docling"），它会在首次使用时从 Hugging Face 下载所需的模型
    - 更好的选择是在github releases下载docling_artifact.zip解压到工作目录下
  - 支持 PDF 扫描件？ A: 支持，使用 mineru 引擎具备 OCR 能力。
  - Q: 内网/离线环境使用？ A: 可以。使用本地 LLM（Ollama/LM Studio）和本地 minerU 或 docling。
  - Q: PDF 缓存机制？ A: MarkdownBasedWorkflow 在内存中缓存解析结果（最近 10 次）。可通过 DOCUTRANSLATE_CACHE_NUM 配置。

- https://github.com/gyunggyung/docling-translate /apache2/202512/python
  - https://gyunggyung.github.io/docling-translate/
  - Advanced PDF/Document Translator with interactive comparison. Built on IBM Docling.
  - 双栏对比布局, 能高亮同一段文本, 翻译悬浮显示

- https://github.com/chaosen315/AIwork4translator /MIT/202512/python
  - 一个专业的文档翻译工具，通过专有名词识别和正则过滤方法，确保大模型翻译时准确使用专业术语。它能够智能处理各种格式的技术文档，保留原文格式和专有名词，提供高质量的翻译结果
  - 实现了全新的并发翻译架构，Queue + Worker Pool模式：采用asyncio. Queue + 工作池架构，支持6并发工作线程
  - 统一翻译核心：新增TranslationCore模块，统一CLI和WebUI的翻译逻辑，消除代码重复
  - 专有名词识别与保护：使用 Aho-Corasick 自动机高效匹配术语，支持复数归一化与冠词智能处理，确保术语在翻译中保持一致。
  - 支持.txt和.md格式文件的翻译，通过`MarkItDown`工具还可以支持PDF、PowerPoint、Word、Excel、HTML等更多格式
    - 推荐的使用方式：输入 Markdown 原文与 CSV 词表，输出为 Markdown 译文。
    - 对于非 Markdown 文件，该程序会自动识别并使用 MarkItDown 转换后再翻译。感谢 MarkItDown 的贡献；目前 PDF（非 OCR）表现良好，OCR PDF 仍待进一步验证。
  - 支持多种API翻译引擎，包括OpenAI、Kimi、DeepSeek、Ollama等
  - 提供命令行和Web界面两种使用方式，满足不同场景需求
    - WebUI 使用 FastAPI 框架开发
  - 双栏Markdown编辑器：WebUI中提供左右分栏的原文/译文实时展示功能
    - 左侧编辑器：显示原文内容，默认为只读模式
    - 右侧编辑器：实时显示翻译结果，支持编辑
  - 实时翻译进度展示：翻译过程中实时显示当前处理的段落数/总段落数
    - 系统采用5秒间隔的轮询机制，实时从后端获取翻译进度和新内容
  - 中断保护与恢复：支持 Ctrl+C 安全中断，自动保存进度与未翻译内容
  - 文件大小不应超过10MB
  - roadmap
    - 通过MinerU增强对Markdown文件的解析性能
    - 实现传统CAP软件的交互模式，例如表格形式的翻译界面，原文与译文逐句对应

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
  - https://github.com/aidayang/PDFMathTranslate-OneClick
    - PDFMathTranslate一键启动整合包，基于 AI 完整保留排版的 PDF 文档全文双语翻译
  - https://github.com/QxJai/PDFMathTranslate-next-qx
    - PDFMathTranslate-next 改成http api
  - https://github.com/nsmao-com/pdf_translate2pdf_api /202511
    - 基于 Byaidu/PDFMathTranslate 改造的 FastAPI REST API 版本，用于科学文献PDF翻译，保留公式、图表和排版。
  - https://github.com/YANG-Haruka/LinguaHaru /GPL/202512/python
    - Next-Gen AI Translation Tool Powered by LLM. Support Office documents, PDF, TXT, and more format with just one click.
  - https://github.com/AaronGIG/pdf2zh-desktop /python
    - pdf2zh 桌面版, Win + Mac 双平台
    - 公式排版完美保留 · Zotero 深度联动
    - OnnxRuntime 8 秒超时机制

- https://github.com/wxyhgk/retain-pdf /MIT/202604/python/rust/js
  - [RetainPDF：PDF 保留排版翻译工具 - LINUX DO _202604](https://linux.do/t/topic/1891990)
  - RetainPDF 做的事: 上传 PDF，一键拿到保留原始排版的中文译文。
  - 首次运行需要填写两个 API Key：MinerU（用于 PDF 解析，每天 2000 页免费）和 DeepSeek（用于翻译，需要自己充值 API ）。
  - 不建议一次丢几百页的 PDF 进去。翻译是按页调 API 的，万一中间断了，前面已经翻完的那些页的费用就回不来了。 建议拆成几十页一批，翻完一批再翻下一批，稳一点。
  - 社区内有类似的项目： PDF2zh ，是否参考过呢。功能几乎一样的
  - 不走传统“先粗切块、再分别识别”的老路，而是尽量基于文字坐标和结构信息做原位回填
  - 面向扫描型 PDF、复杂行内公式、双栏论文、教材类长文档
  - 提供仍在持续打磨的高精度模式，目标是在复杂科研文档、混排页面和疑难结构场景下进一步逼近甚至超越常见 OCR 方案的效果上限, 高精度模式也是我后续最核心的演进方向之一

- https://github.com/CBIhalsen/PolyglotPDF /2.1kStar/GPL/202509/python/js
  - A multilingual eBook processing tool supporting all eBook formats. 
  - Features online and offline translation while preserving original layouts.
  - Compatible with both scanned and digital PDFs. 
  - 目前效果，对于基于文本的pdf, polyglotpdf的解析方式依旧是最优解。 ocr和布局分析并不总是完美。
  - 对于报告型表格文档，polyglotpdf效果相当完美，当然表格中的复杂矢量数学公式依旧无法正确处理
  - 本项目采用与 Adobe Acrobat DC 编辑 PDF 类似的基本原理，基于 PyMuPDF 识别和处理 PDF 文本块, 这种方式直接处理 PDF 文本块，保持原有布局不变，实现高效的文本提取和修改
  - 🛝
    - 实测图片pdf在ocr后下层是原文, 文字散乱排布在上层, 视觉上是重影, 但分栏布局可以还原, 且识别后的每行文本和原文位置基本都一致
    - 💡🤔 更合理的流程是生成2个pdf image > text-pdf > translated-pdf, 这样就能既保持原有布局，又能无重影展示干净的译文pdf
  - [关于·ocr识别 ](https://github.com/CBIhalsen/PolyglotPDF/issues/6)
    - 请问考虑·添加·paddle作为OCR模型吗？ 文字PDF的翻译速度是我用过最快的，比pdfmathtran快几倍
  - https://github.com/saurabhhbansal/polyglot-pdf /202507/inactive
    - PDF translation tool that preserves document formatting while translating content using state-of-the-art AI models. 

- https://github.com/Dicklesworthstone/llm_aided_ocr /2.8kStar/NALic/202408/python/代码少/inactive
  - Enhance Tesseract OCR output for scanned PDFs by applying Large Language Model (LLM) corrections
  - Uses LLM to fix OCR-induced errors
  - Converts text to proper markdown format
  - [Show HN: LLM-aided OCR – Correcting Tesseract OCR errors with LLMs | Hacker News _202408](https://news.ycombinator.com/item?id=41203306)

- https://github.com/discus0434/pdf-translator /CC-NC/202405/python/inactive
  - translates English PDF files into Japanese, preserving the original layout
  - This repository offers an WebUI and API endpoint that translates English PDF files into Japanese, preserving the original layout.
  - For PDF layout analysis, using DiT.
  - For PDF to text conversion, using `PaddleOCR` model.
  - For text translation, using FuguMT(CC-SA) model from HuggingFace.
  - https://github.com/ppisljar/pdf_translator /202409/与上面架构类似
    - offers an WebUI and API endpoint that translates PDF files using openai GPT, preserving the original layout.
  - https://github.com/poppanda/LLM_PDF_Translator /202512/python
    - inspired by ppisljar/pdf-translator and adds the following features:
    - [GUI] Add support for download-save-translation process on the server (better for mobile devices)
    - Support of Ollama and QWEN for translation (by api)
    - Support multi threading for translation
    - Use single process for ocr / layout model to save vram

- https://github.com/oomol-lab/pdf-craft /4.1kStar/AGPL > MIT/202512/python
  - https://pdf.oomol.com/
  - 将 PDF 文件转换为各种其他格式，本项目专注于处理扫描版书籍的 PDF 文件
  - 本项目基于 DeepSeek OCR 进行文档识别。支持表格、公式等复杂内容的识别。通过 GPU 加速，pdf-craft 能够在本地完成从 PDF 到 Markdown 或 EPUB 的完整转换流程。
    - 依赖 DeepSeek OCR 模型，首次运行时会自动从 Hugging Face 下载。
  - 从 v1.0.0 正式版开始，pdf-craft 全面拥抱 DeepSeek OCR，不再依赖 LLM 进行文本矫正。这一改变带来了显著的性能提升：整个转换流程在本地完成，无需网络请求，告别了旧版本中漫长的等待和偶发的网络失败。
    - 新版本也移除了 LLM 文本矫正功能。如果你的使用场景仍然需要这一特性，可以继续使用 v0.2.8 旧版本
  - 要真正使用 pdf-craft，你需要安装 `Poppler` 用于 PDF 解析（所有使用场景都需要）以及配置 CUDA 环境用于 OCR 识别（实际转换时需要）
  - ❓ 原文中的插图会提取为单独图片吗
  - 效果是直接输出新的pdf文件
  - Starting from the official v1.0.0 release, pdf-craft fully embraces DeepSeek OCR and no longer relies on LLM for text correction.
    - removing the previous AGPL-3.0 dependency, allowing the entire project to be released under the more permissive MIT license
    - Note that pdf-craft has a transitive dependency on `easydict` (LGPLv3) via DeepSeek OCR.
  - [PDF Craft：一个更懂技术的开源 PDF 转换工具 _202512](https://linux.do/t/topic/1322118)
    - 我们基于 DeepSeek-OCR 重写了一个转换引擎：pdf-craft
    - 更智能的布局还原：特别优化了双栏和图文混排，目标是转成 Markdown 或 EPUB 后，还能有接近纸质书的阅读体验。
    - 更完美的 LaTeX 公式支持：无论是行内公式还是独立公式，都能精准识别并还原
    - 本地免费跑（我们最推荐的）
  - https://github.com/oomol-lab/epub-translator /MIT/202601/python
    - uses AI large language models to automatically translate EPUB e-books while 100% preserving the original book's format, illustrations, table of contents, and layout. 
  - https://github.com/jarodise/pdf2epub-paddle /MIT
    - vibe code了一个扫描版电子书转换工具，打包了PaddleOCR的API，然后在代码层面做了一些工程优化处理, 确保扫描版的PDF文件能够转化成排版优雅的Epub格式电子书，去除PDF文件中不必要的页眉，页脚，页码等杂乱元素的同时，最大程度保留原书内的插图，表格等内容。

- https://github.com/gavrielc/Nano-PDF /903Star/MIT/202512/python/gemini
  - A CLI tool to edit PDF slides using natural language prompts, powered by Google's Gemini 3 Pro Image ("Nano Banana") model.
  - Natural Language Editing: "Update the graph to include data from 2025", "Change the chart to a bar graph".
  - Add New Slides: Generate entirely new slides that match your deck's visual style.
  - Non-Destructive: Preserves the searchable text layer of your PDF using OCR re-hydration.
  - Multi-page & Parallel: Edit multiple pages in a single command with concurrent processing.
    - The tool processes multiple pages in parallel for speed, with configurable resolution (4K/2K/1K) to balance quality vs. cost.
  - 💡 How It Works
    - Converts target PDF pages to images using Poppler
    - Style References: Optionally includes style reference pages with generation request to understand visual style (fonts, colors, layout)
    - Sends images + prompts to Gemini 3 Pro Image, which generates edited versions
    - OCR Re-hydration: Uses Tesseract to restore searchable text layer to generated images
    - PDF Stitching: Replaces original pages with AI-edited versions while preserving document structure
  - https://x.com/GithubProjects/status/1995953642772500850
    - Most PDFs can be converted to an editable formats. This feels like over engineering lowkey

- https://github.com/WildDataX/suppr-mcp /202510/ts/仅云端?
  - https://suppr.wilddata.cn/
  - 超能文献|AI驱动的文档翻译与学术搜索服务。支持PDF、DOCX、PPTX等多格式文档的高质量翻译（支持11种语言），特别优化了数学公式翻译。同时提供PubMed学术文献智能搜索功能。
  - 翻译时间取决于文档大小，通常几分钟到十几分钟不等。可以使用 `get_translation` 查询进度。
  - https://github.com/WildDataX/PDFMathTranslate-vs-Suppr.ai-PDFtranslate
    - 🆚 PDFMathTranslate vs Suppr.ai 超能文献 对比

- https://github.com/phkhanhtrinh23/translation_layoutrecovery /110Star/NALic/202308/python/ts/inactive
  - This is a project that translates a .pdf file, preserving the original layout of that .pdf file. [UPDATED] We have achieved the Second Prize of the Cinnamon AI Bootcamp 2023.
  - Translation with Layout Recovery is a cutting-edge approach in the field of natural language processing that goes beyond traditional machine translation methods
  - Frontend: NextJS, TailwindCSS, NodeJS, Yarn.
  - Backend: Django REST Framework.
  - Database: PostgreSQL.
  - Storage: Firebase Cloud Storage.
  - Layout Recovery: MaskRCNN.
  - OCR: EasyOCR.
  - NMT: envit5-translation.
  - Spelling Correction (Japanese): JGEC

- https://github.com/chaodreaming/layover-pdf /49Star/apache2/202503/python/代码少/inactive
  - 一个使用layout overlay方式实现PDF英文翻译为中文的免费工具，使用智普api来完成ocr和翻译功能
  - glm-4v-flash免费并且10QPS, 实测速度约为10s/页
  - 启动gradio服务: python3 app.py
  - uses `PyMuPDF` to achieve advanced functionality.
  - DocLayout-YOLO
  - 🛝
    - 本地运行时, onnxruntime-gpu只支持linux/win

- https://github.com/LunarTechAI/babel-extreme /202512/python
  - Translate image-only PDFs while preserving layout, tables, diagrams, and formulas. 
  - Built for engineering books and technical documents where existing tools fail.
  - ocr-mineru > TRANSLATE-mistral > ReportLab-pdf-gen

- https://github.com/tomorrow9913/PDF-Dual-Translate-Viewer /202506/python/PySide6/inactive
  - a desktop application that provides a dual-view (original/translated) PDF viewer, page navigation, highlight synchronization, translation integration, and style/layout preservation. 
  - It is built with PySide6, PyMuPDF, and follows a clean architecture design.
  - Main View: Default dual PDF viewer and translator screen.
  - Thumbnail Preview: When clicking the bottom-left thumbnail, shows a preview of page 10.
  - Table of Contents View: Main view with the left-side table of contents (outline) panel open.
  - Synchronized highlighting (both views)
  - PySide6 (Qt-based GUI), PyMuPDF

- https://github.com/zishengwu/vlm-ocr-webui /MIT/202508/python/ts/inactive
  - using vlm to ocr pdf with user friendly ui
  - a powerful document processing tool that utilizes advanced Vision Language Model (VLM) technology to intelligently recognize and extract various elements from PDF documents, including text, paragraphs, headings, tables, charts, and formulas, converting them into structured Markdown format.
  - parallel processing with multiple models to ensure high-precision recognition of diverse document content, including complex layouts
  - Not only extracts standard text but also accurately recognizes and converts tables and mathematical formulas into LaTeX format
  - Automatically organizes the extracted document content into clear, readable Markdown format, preserving the original layout and semantic structure
  - Streaming Processing: Features advanced concurrent processing where multiple APIs work in parallel, while each API processes pages sequentially. Results are displayed immediately after each page is processed, eliminating the need to wait for the entire PDF to complete.
  - OCR/VLM: OpenAI API (extensible)
  - Backend: Python, FastAPI, Uvicorn
  - Frontend: Next.js, React, TypeScript, Tailwind CSS

- https://github.com/PRITHIVSAKTHIUR/Multimodal-VLM-v1.0 /apache2/202512/python
  - vision-language model application supporting image inference and visual question answering. 
  - This repository hosts a Gradio-based demo that integrates several specialized models for document processing, OCR, spatial reasoning, and object/point detection.
  - Interactive web UI built with Gradio that supports streaming text output and image-based model tasks.
  - Streaming generation using TextIteratorStreamer for real-time text display while the model generates.
  - The demo is optimized for a single CUDA device but will fall back to CPU if no GPU is available.

- https://github.com/PRITHIVSAKTHIUR/VLM-Parsing /apache2/202512/python
  - a Gradio-based web application for parsing documents and images into structured HTML and Markdown formats using advanced Vision Language Models (VLMs)
  - Upload and process PDF or image files (PNG, JPEG, JPG).
  - Select between two VLMs: Logics-Parsing and Gliese-OCR-7B-Post1.0.

- https://github.com/PhysicsNR/pdfcraft /MIT/202509/python/inactive
  - A Python-based PDF viewer & toolkit with OCR, compression, and annotation features.
  - lightweight, open-source alternative to Acrobat
  - Built with PySide6, PyMuPDF, and Tesseract OCR.
  - OCR scanned PDFs (make image-based PDFs searchable)

- https://github.com/3ai92/3AIDoc /apache2/202509/python/ts
  - A full-stack web application that combines OCR (Optical Character Recognition) technology with interactive document annotation capabilities. 
  - The platform allows users to upload images or documents, automatically extract text using PaddleOCR, and create interactive form overlays for data extraction and annotation.
  - 仅支持图片上传
  - https://github.com/RapidAI/PaddleOCRModelConvert /apache2/202507/python/inactive
    - This repository is mainly to convert Inference Model in PaddleOCR into ONNX format.

- https://github.com/Tansuo2021/OCRPDF-TO-PPT /314Star/MIT/202601/python
  - 这是一个功能强大的PPT编辑器，支持OCR识别、AI图片编辑、背景去除、多页面管理等专业功能。本版本（v2.0）经过全面优化，在代码质量、性能、可维护性等方面都有显著提升。
  - 多页面支持 - 批量导入PDF/图片，支持页面管理
  - OCR识别 - 智能文字识别，自动生成文本框
  - AI图片编辑 - AI驱动的图片替换和生成
  - 背景去除 - 智能涂抹去除背景
  - 图层系统 - 类似Photoshop的图层管理
  - 项目管理 - 保存/加载项目，支持自动保存
  - 多格式导出 - 导出为PPT/PDF/图片
  - 托管线程池 - 高效的并发任务管理, 多线程并发控制，消除竞态条件
  - PaddleOCR - OCR识别引擎
  - IOPaint - 图片修复功能
  - PIL/Pillow - 图片处理
  - python-pptx - PPT生成
  - [大香蕉生成图片转换为可编辑PPT的速度直接质变！飞升了！GPU加持下无敌  ](https://linux.do/t/topic/1410288)
  - [【开源】全新的图片/PDF一键转换生成可编辑PPT，让你的Gemini大香蕉猛猛用 ](https://linux.do/t/topic/1523411)
    - 主要页面优化更新了，之前的页面难懂，现在应该简单明了一点
    - 佬友你这个tk实现ui有点过于原生导致的庞大了，看你代码逻辑应该是先识别文字然后和涂抹修复。但是你字体这块处理解决不了，L站我前天看过一个项目，好像是做本子翻译的，逻辑大概是利用大模型的多模态能力来对图片（你的项目对应大香蕉的PPT）文字识别，给出文字的原文，x、y、w、d、倾斜、粗体、字体、翻译等多个选项，我感觉挺适合你的项目。 如果追求MPV，我的思路是直接再利用大香蕉生成一张带文字的无字底图（大香蕉可以输出文本+图片），直接少了两个模型调用过程。
      - 我这个是要做到纯本地运行的，你说的这个功能之前版本是有AI识别这个，直接用gemimi大香蕉来进行背景还原修改的
    - 当然，你这个两个模型都是部署在本地上的，只是你这个快上万行的UI文件有点吓到我了，后面的MPV相当于一个新的项目开发方向了。 L站开发的项目我确实习惯性All in AI了，不过字体位置识别这块LLM确实效果会好点，就是需要额外的API。
    - 已经做到office插件运行了?
      - 还没有，只是可以在ppt中预览
  - [大香蕉直出PPT底图和文字 ](https://linux.do/t/topic/1523689)

- https://github.com/baoyudu/paper-burner /244Star/GPL/202506/js/单文件/inactive
  - https://baoyu.space/paper-burner/
  - PDF文档OCR与翻译工具
  - Paper Burner能够从PDF文档中提取文本（OCR），将其转换为Markdown格式，并支持使用多种AI模型进行高质量翻译，完美保留公式、图表、格式，最大限度地保持语意连贯通顺
  - 本工具完全在浏览器中运行。
  - PDF文本提取：使用Mistral AI的OCR技术从PDF文档中精确提取文本内容
  - 自动将提取的内容转换为规范的Markdown格式
  - 自动提取并保存PDF中的图片
  - 支持多种顶级AI大模型进行翻译
  - 长文档翻译：自动按照文章小节分段处理长文档，避免段落中出现断点，确保翻译质量和内容一致性
  - 翻译过程中完美保留原文档的格式、公式和结构
  - 本项目保持轻量化，不再增加新功能，但可能继续维护新的API端点。如果您的需求不止于文档处理，希望在浏览器中继续体验阅读、分析等功能，欢迎大家继续关注本项目的分支 Paper Burner X，由 Feather-2 继续保持维护与更新
  - https://github.com/Feather-2/Burner-X /1.3kStar/AGPL/202511/js/inactive
    - https://paperburner.viwoplus.site/views/landing/landing-page.html
    - https://paperburner.viwoplus.site/
    - 浏览器即开即用，AI文献识别、文档批量翻译、阅读与智能分析工具
    - 支持 PDF/DOCX/PPTX/EPUB 等多种格式，能够进行 OCR 识别、高质量翻译、智能分析，完美保留公式、图表和格式。
    - 在前端实现了一个 Agentic RAG 系统。通过赋予 AI 全局的文章结构 和一系列工具（如 grep, vector search, fetch等等），AI 能够自主决策、多步推理，并在长文本中实现复杂的分析和信息提取任务。
      - 在纯前端环境中，实现了一个长文本Agent。少量文本下，将使用全量的策略；而当提供长文本时候，使用长文本Agent。
    - 批量处理： 支持多种文档格式（PDF/DOCX/EPUB 等）和代码库的直接导入。利用并发 OCR 和翻译，并结合术语库（支持数万词条快速匹配），显著提升了文献处理效率。
    - 目前所有数据均在浏览器本地，支持用户接入自定义 AI 模型端点，并提供了配套的 OCR Server 和 Docker 部署选项
    - 不仅支持本地文件上传，更可一键从 GitHub 仓库或任意 URL 导入内容，自动完成解析。
    - PDF可以使用OCR (支持`mineru/doc2x`等) 与翻译引擎，并实现保留原文格式翻译功能（基于mineru，目前优化中，并会支持更多模型）。
    - 术语备择库： 进行了性能优化，支持一次性导入数万条术语并进行快速匹配。
    - 沉浸式对照阅读： 提供智能对齐的段落级原译文对照、文档结构目录（TOC）、高亮与标注功能，先进行无障碍的阅读，再进行AI总结。
    - 结构化信息提取： 内置了“文献矩阵”等实用工具，能够将非结构化的论文内容，智能提取为清晰的结构化数据，方便进行横向对比和分析
    - 给予 AI 一系列工具，如精确匹配的 grep、向量搜索 vector search、内容抓取 fetch 等。AI 会根据你的问题，自主分析并决定调用哪种工具组合来寻找最佳答案。
    - 下一个里程碑是将能力从分析单篇文献，扩展到处理多篇文献，并基于此开发能自动生成文献综述的 综述 Agent
    - [Agent伴读🤖！专为学术/工作打造，您的一站式AI翻译/阅读/分析工作站 _202510](https://linux.do/t/topic/1007281)
    - [Paper Burner X 自定义：手把手教你用 cf worker 加入更多OCR引擎/学术搜索功能 _202510](https://linux.do/t/topic/1009321)
      - 看到了很多佬友对多种OCR方式的需求， 因为项目是纯前端的，所以使用cf worker来代理。
      - 有反馈大文件会出现failed to fetch，这里新增分块机制
- https://github.com/AuroraPixel/MarkMuse /MIT/202505/python/inactive
  - an innovative tool developed using Python that elegantly converts PDF files to Markdown format.
  - 公司正在建设基于 RAG 的知识库，急需高质量的文档预处理与数据清洗方案
  - 基于Celery、Redis和PostgreSQL的通用任务队列Web API，提供异步任务的提交、执行和状态查询功能。
  - 提供基于FastAPI的RESTful API接口
  - 高精度 PDF→Markdown：基于 Mistral AI OCR，精确提取文本与结构。
  - 模板化提示词：内置 Jinja2 与 LangChain，灵活自定义转换规则。
  - [新项目pdf转md : MarkMuse _202504](https://linux.do/t/topic/610328)

- https://github.com/yyy-OPS/slidedeconstruct-ai /113Star/MIT/202512/ts
  - 基于 AI 视觉能力的智能演示文稿反向工程工具。它利用 Google Gemini (或 OpenAI Compatible) 模型，将一张静态的 PPT 截图“拆解”为可编辑的图层（背景、文字、视觉元素），并支持将其转化为矢量形状，最终导出为可编辑的 .pptx 源文件。
  - 图片拆解：自动移除图片中的文字（保留背景），并提取视觉元素。
  - 矢量化重构：尝试将图像中的视觉元素转化为 PPT 原生的矢量形状（如矩形、圆形、箭头等），而非简单的图片贴图。
  - 支持批量上传 PDF、PNG、JPG 格式的幻灯片（PPT/PPTX 建议先导出为 PDF）。
  - 使用 AI 视觉模型精确识别页面中的文本块、视觉元素和背景颜色。
  - 🤔 智能背景修复: 也可用于pdf ocr的场景，能使文档视觉整洁
    - 自动去字：在提取文本后，AI 会自动“擦除”原图上的文字，并根据周围纹理修复背景，生成干净的底图。
    - 手动擦除：提供“橡皮擦”模式，用户可手动框选区域让 AI 移除多余元素。
    - 背景
  - 矢量化转换 (Beta)：尝试将识别到的简单几何图形（矩形、圆形、箭头等）转换为 PPT 原生形状，而非仅仅粘贴图片。
  - 一键导出 PPT：将拆解后的所有元素（文本、背景、图片、形状）按原位置重组，导出为可编辑的 .pptx 文件
  - AI Integration: Google GenAI SDK (@google/genai), OpenAI API Compatible
  - File Handling: pptxgenjs (PPT生成), pdfjs-dist (PDF解析)
  - [开源了一个 PPT“逆向”工具，图片直接转可编辑 PPT _202512](https://linux.do/t/topic/1368469)
    - 代码都是AI写的！我也不咋能看懂，慢慢学习嘛
# translation
- https://github.com/michaelbeijer/Supervertaler /16Star/MIT/202512/python/PyQt6
  - https://supervertaler.com/
  - AI-powered translation workbench with multi-LLM support (GPT-4, Claude, Gemini, Ollama).
  - AI Providers - OpenAI GPT-4o/5, Claude 3.5 Sonnet, Google Gemini 2.0
  - Local LLM (Ollama) - Run AI translation offline, no API keys needed, complete privacy
  - Google Cloud Translation API integration
  - Translation Results Panel - All match types (Termbase, TM, MT, LLM) in one view
  - Bilingual Review Interface - Grid, List, and Document views
  - Multiple Termbases - Glossary support per project
  - Document Support - DOCX, bilingual DOCX, PDF, Markdown, plain text
  - OS: Windows, macOS, Linux
  - Database: SQLite (built-in)
  - Two Editions Available
    - Qt Edition (Modern) - Recommended
    - Tkinter Edition (Classic) - Stable

- https://github.com/wuwangzhang1216/DocTrans /MIT/202511/ts
  - A powerful document translation system powered by Google Gemini AI, with both CLI and Web Application support. 
  - Features dynamic parallel processing with up to 256 workers for high-performance translation.
  - Smart Allocation: Up to 16 pages/slides concurrently, 64 workers per page
  - Supports multiple file formats including PDF, Word, PowerPoint, Excel, and more.

- https://github.com/aikilan/Babel-Markdown /MIT/202511/ts
  - provides real-time translation previews for VS Code, synchronizing the original Markdown and AI-translated content in a single view to help you efficiently proofread multilingual documents.
  - Progressive translation preview: streams segments as they finish translating.
  - Markdown fidelity: preserves headings, lists, tables, and code blocks exactly.
  - OpenAI-compatible API support: customize base URL, model, language, and timeout for any compatible provider.

- https://github.com/zstar1003/FreePDF /300Star/AGPL/202512/js
  - 一个免费的PDF文献阅读器，支持将各语言的PDF文献转成中文，并支持接入大模型基于文献内容进行问答。
  - 翻译完的PDF文件，会在其对应目录下生成-mono.pdf(翻译文件)
  - 支持图片型PDF吗，比如扫描件？
    - 回答： 不支持，本质上是借助`pdf2zh`检测文本块内容，再进行翻译替换，图片型无法直接替换，会导致内容重合叠加。
  - 使用大模型翻译时，有些内容没有翻译？
    - 回答： 低参数量的大模型本身的指令遵循能力很差，让它翻译，它可能不会完全听话，就会造成此现象。因此，本地用大模型翻译，必须保证大模型本身具备一定参数规模，建议7B以上
  - 表格中的内容没有翻译？
    - 回答: `pdf2zh`暂不支持表格内容翻译，如需翻译表格，可查看本仓库的dev分支，采用`pdf2zh_next`进行翻译，但由于速度较慢

- https://github.com/am009/LLM-online-tool /202512/python/js
  - https://tool.latexdiff.cn/
  - 基于大语言模型（LLM）API的 Markdown/Latex 文章翻译工具
  - 👀 上传markdown/latex文件，不支持pdf
  - 逐段翻译与校对：点击蓝色箭头按钮即可翻译当前段落，然后可以在右侧实时编辑，
  - 纯静态网页：完全在浏览器中运行
  - 分块翻译：将 Markdown 内容分割为可管理的段落进行翻译
  - 问：为什么没有按照我想要的方式分割段落？段落分割方式是什么？
    - 答：根据 “连续的两个换行” 分割段落。只有空格和tab的行也看作单独的空行。
  - https://github.com/am009/dots.ocr
    - 本Fork提供Docker容器重新封装的API，支持20系等旧的 Turing GPU，以float32格式运行。测试机型：单2080ti 22GB。

- https://github.com/ogkalu2/comic-translate /2.3kStar/apache2/202512/python
  - Desktop app for automatically translating comics - BDs, Manga, Manhwa, Fumetti and more in a variety of formats (Image, Pdf, Epub, cbr, cbz, etc) and in multiple languages.
  - Many Automatic Manga Translators exist. Very few properly support comics of other kinds in other languages. This project was created to utilize the ability of State of the Art (SOTA) Large Language Models (LLMs) like GPT-4 and translate comics from all over the world.

- https://github.com/meangrinch/MangaTranslator /60Star/apache2/202512/python/Gradio
  - Web application for automating the translation of manga/comic page images using AI. 
  - Targets speech bubbles and text outside of speech bubbles. 
  - Supports 54 languages and custom font pack usage.
  - Speech bubble detection, segmentation, cleaning (YOLO + SAM 2.1)
  - LLM-powered OCR and translations (supports 54 languages)
  - Upscaling (2x-AnimeSharpV4)
  - Two interfaces: Web UI (Gradio) and CLI

- https://github.com/SUSYUSTC/MathTranslate /1.3kStar/apache2/202309/python/latex/inactive
  - This is a project to translate LaTeX documents, especially scientific papers, from any language to any language. 
  - LaTeX expressions like math expressions are perfectly kept unchanged. 
  - it can be directly applied to translate arXiv papers since it provides the LaTeX source code of most of the papers.
  - [submodule: extract text from pdf and translate ](https://github.com/SUSYUSTC/MathTranslate/issues/76)
    - 如果您想翻译仅有 pdf 版本的论文，可以先通过 [mathpix](https://mathpix.com/) 将 pdf 转换为 latex 
  - [使用 mathpix 将 PDF 转换成 latex 后，通过 Web Server 上传 zip 进行翻译，结果排版格式会有问题 ](https://github.com/SUSYUSTC/MathTranslate/issues/73)
    - 这个情况我们目前也知道，主要是表格和图片大小的问题。我们也没有什么好的解决方法，只能参考原文或者手动调一下代码改大小。Latex语言过于flexible导致很难兼容所有的情况。

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

- https://github.com/yunshaochu/mangatype-live /202601/ts
  - 一款提供了AI自动嵌字功能的漫画编辑器
  - [搓了一个AI全自动翻译、嵌字的漫画编辑器，单纯的对话模型（Gemini、kimi 2.5），不使用大小香蕉  ](https://linux.do/t/topic/1523120)
    - 给有视觉能力的 AI 开个接口让它们自己找文本框、自己嵌字岂不美哉？这样也能节省大香蕉的资源
    - 不代表 2.5p 和 2.5f 就不能用了，因为我们还有文本探测技术，可以检测到日文文本的坐标信息
    - 假如提前把坐标告诉 AI，能否让嵌字质量上升？ 我在给项目加上了 dmMaze 的 comic-text-detector 之后，再尝试了一次, 虽然还是比不上 gemini 3 flash，但能用了
  - https://github.com/dmMaze/comic-text-detector /GPL/python
    - Manga&Comic text detection
    - scripts to train a text detector based on manga-image-translator which can extract bounding-boxes, text lines and segmentation of text from manga or comics to help further comics translation procedures such as text-removal, recognition, lettering, etc.

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

- https://github.com/jiananlan/PDFreformertool /AGPL/202507/python/inactive
  - pdf文档翻译并重排版软件，支持利用llm-api进行翻译
  - 利用 LLM 的高级语义处理能力，结合 pymupdf 和 pdfplumber 等库，提取 PDF 内容并生成高质量翻译结果。翻译数据存储在 MongoDB 中，同时实验性支持 HDF5（T5.py）作为替代存储方案。
  - 格式保留：基于 `python-docx` 和 docxtpl 重构文档格式，确保翻译后文档格式一致。

- https://github.com/NEKOparapa/AiNiee /4.8kStar/AGPL/202512/python
  - 一款专注于 AI 翻译的工具， 一键自动翻译游戏、书籍、字幕、文档等复杂长文本内容

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

- https://github.com/yihong0618/bilingual_book_maker /9kStar/MIT/202511/python
  - an AI translation tool that uses ChatGPT to assist users in creating multi-language versions of epub/txt/srt files and books.
  - This tool is exclusively designed for translating epub books
  - [未来是否支持pdf格式 要是可以用这个看论文也会很快 ](https://github.com/yihong0618/bilingual_book_maker/issues/20)
    - 核心还是 pdf 是不是可读的文版，而不只是图片？

- https://github.com/realtek1990/rebook /MIT/202604/python/ts
  - Translate and convert e-books with state-of-the-art AI
  - PDF → EPUB, EPUB → EPUB/Markdown/HTML
  - PDF OCR — Marker OCR extracts text from scans (optional)
  - Native macOS GUI — Cocoa/AppKit, drag & drop
  - 30 parallel threads — translate entire books in minutes

- https://github.com/windingwind/zotero-pdf-translate /10.6kStar/AGPLv3/202401/ts
  - Translate PDF, EPub, webpage, metadata, annotations, notes to the target language. 
  - Support 20+ translate services.

- https://github.com/transkit-app/transkit-desktop /GPL/202604/rust/js
  - https://transkit.app/
  - a cross-platform translation & OCR app, originally based on Pot
  - https://github.com/pot-app/pot-desktop /GPL

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
- https://github.com/xushengfeng/eSearch /6.2kStar/GPLv3/202512/ts/electron
  - https://esearch-app.netlify.app/
  - 截屏+OCR+搜索+翻译+贴图+屏幕翻译+以图搜图+滚动截屏+录屏
  - eSearch 是Information-portal的:electron: 重写版(顺便加了亿些功能)
  - 主要是想在 Linux 上(win 和 mac 上也能用)实现锤子大爆炸或小米传送门这样的屏幕搜索功能，当然也是一款方便的截屏软件。
  - 截屏 离线OCR 搜索翻译 以图搜图 贴图 录屏 滚动截屏 
  - 本地 OCR 由`PaddleOCR`的模型提供支持。

- https://github.com/MrAMS/Smart-Search-PDFs /MIT/202601/python/qt5
  - 🔍 智能 PDF 搜索引擎 - 基于语义向量(embeddings)和 BM25 的混合搜索系统，可用于开卷考试离线搜索PDF课件
    - 一个基于语义向量（Embeddings）和 BM25 算法的本地化 PDF 混合搜索工具。
  - 全部在本地运行，无需 API Key，保护隐私。
    - 本地端侧：无需 GPU/API，使用 FastEmbed 和轻量级模型，CPU 也能流畅运行，无需 OpenAI API Key。
  - ux交互是双栏布局，左侧是文本，右侧是pdf原文，左侧搜索出的文本，右侧不会高亮
  - 混合搜索（智能推荐）： 结合了语义理解和关键词匹配。不仅能搜到字面一样的，还能搜到意思相近的。结果自动按相关度排序。
    - 语义搜索： 哪怕你输入的词文中没出现，只要意思对，就能搜到。（基于 Jina AI 的 Embeddings 模型）。
    - BM25 关键词： 经典的倒排索引算法，不仅是精确匹配，还能处理词频权重。
    - 大文件支持：动态加载机制，几百页的文档滚动流畅不卡顿。
  - [[开源自荐] 开卷考试/论文搜索神器 - 基于语义向量和BM25的PDF文件搜索软件 ](https://linux.do/t/topic/1408107)
    - 不管是开卷考试需要在几百页的 PPT 里瞬间定位知识点，还是写论文时需要在几十篇参考文献中寻找佐证，传统的 Ctrl+F 往往力不从心

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
  - Extracts text from scanned PDFs using `Tesseract`.
  - Automatically uploads processed documents via WebDAV
  - Easy deployment with Docker Compose
  - Configure your network scanner to send scans via FTP

- https://github.com/Paullllllllllllllllll/ChronoTranscriber /MIT/202511/python
  - A Python-based tool for researchers and archivists to transcribe historical documents from PDFs, EPUB ebooks, or image folders. 
  - ChronoTranscriber supports multiple AI providers (OpenAI, Anthropic, Google, OpenRouter) via LangChain, local OCR with `Tesseract`, and provides structured JSON outputs with scalable batch processing for large-scale document digitization projects.
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
  - [The Proofreader API  |  AI on Chrome ](https://developer.chrome.com/docs/ai/proofreader-api)

- https://github.com/chrisgrieser/obsidian-proofreader /30Star/MIT/202512/ts
  - AI-based proofreading and stylistic improvements for your writing. 
  - Changes are inserted as suggestions directly in the editor, similar to suggested changes in word processing apps.
  - Suggested changes are inserted directly into the text: Additions as ==highlights== and removals as ~~strikethroughs~~ .
  - https://github.com/lucasmelin/red-pen /MIT/202308/ts/inactive
    - Red Pen is implemented as a retext-based plugin for the Obsidian note-taking app.
    - Red Pen acts as a proofreader for your writing.
    - It highlights phrases that could use simplifying, identifies weasel words, hedges, filler, and many more.
  - https://github.com/SahandMalaei/ai-writing-tools-obsidian /GPL/202511/ts
    - A suite of AI-powered writing tools for Obsidian, including dictionary lookup, proofreading, and context-aware explainer
    - 交互在弹窗

- https://github.com/CZ600/AutoDocxProofread /MIT/202511/ts/vue
  - 基于大模型的文档校对软件, 校对结果列表显示在右侧面板
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

- https://github.com/hotchpotch/open_provence /MIT/202511/python
  - Open-Source, Efficient, and Robust Context Pruning for Retrieval-Augmented Generation
  - Lightweight Provence-style rerankers that keep the answers and drop the noise for retrieval-augmented generation.

- apps
  - [Refine - AI Powered Offline Grammar Checker for Mac | Privacy-First Grammarly Alternative](https://refine.sh/)
# spellchecking
- https://github.com/languagetool-org/languagetool /13.6kStar/LGPL/202509/java
  - https://languagetool.org/
  - Open Source proofreading software for English, Spanish, French, German, Portuguese, Polish, Dutch, and more than 20 other languages
  - [100% Open source alternative for Grammarly : r/opensource](https://www.reddit.com/r/opensource/comments/x9sc53/100_open_source_alternative_for_grammarly/)
    - 202512: LanguageTool is no more available, as of today they limit their extension to paid only users.
- https://github.com/kiriharu/lango /202601/ts
  - https://lango.kiriha.ru/
  - simple frontend alternative for LanguageTool compatible API
  - A modern frontend interface for the LanguageTool API, built with React, TypeScript, and Material UI.
  - Text grammar and style checking using LanguageTool API
  - Real-time text analysis
  - Higlight potential issues in text
  - Lango was created especially to use with custom selfhosted LanguageTool backend like https://github.com/meyayl/docker-languagetool /docker

- https://github.com/sonnyp/Eloquent /183Star/GPL/202512/js
  - Eloquent is a proofreading software for English, Spanish, French, German, Portuguese, Polish, Dutch, and more than 20 other languages.
  - It works fully offline, powered by LanguageTool standalone server.
  - Eloquent is also able to run as a service in the background to make your local/offline LanguageTool server available to Firefox, LibreOffice and more.

- https://github.com/automattic/harper /9kStar/apache2/202601/rust/ts/svelte
  - https://writewithharper.com/
  - Offline, privacy-first grammar checker. Fast, open-source, Rust-powered
  - LanguageTool is great, if you have gigabytes of RAM to spare and are willing to download the ~16GB n-gram dataset. Besides the memory requirements, I found LanguageTool too slow: it would take several seconds to lint even a moderate-size document.
  - That's why I created Harper: it is the grammar checker that fits my needs. Not only does it take milliseconds to lint a document, take less than 1/50th of LanguageTool's memory footprint, but it is also completely private.
  - Harper is even small enough to load via WebAssembly.
  - 🌐 Harper currently only supports English, but the core is extensible to support other languages
  - Supported Editors: Visual Studio Code, Neovim, Helix, Emacs, Zed

- https://github.com/theJayTea/WritingTools /2.1kStar/GPL/202601/python/swift/全局浮窗交互
  - The world's smartest system-wide grammar assistant; a better version of the Apple Intelligence Writing Tools. 
  - Works on Windows, Linux, & macOS, with the free Gemini API, local LLMs, & more.
  - Instantly proofread and optimize your writing system-wide with AI
  - an Apple Intelligence-inspired application for Windows, Linux, and macOS that supercharges your writing with an AI LLM (cloud-based or local).
  - Select any text on your PC and invoke Writing Tools with ctrl+space.
  - The macOS version is a native Swift port, macOS 14 or later is required due to accessibility API requirements.
    - Run local LLMs with MLX on Apple Silicon
# more
- https://github.com/leplusorg/docker-pdf /apache2/202512/docker
  - Multi-platform Docker container with utilities to process PDF files (pdftk, ghostscript, ocrmypdf, pdfgrep, qpdf...).

- https://github.com/scambier/obsidian-text-extractor /GPL/202512/ts
  - A (companion) plugin to facilitate the extraction of text from images (OCR) and PDFs.
  - I unfortunately can't dedicate much time anymore on Text Extractor. It's mostly feature-complete
  - https://github.com/MohrJonas/obsidian-ocr
  - https://github.com/diegomarzaa/pdf-ocr-obsidian
