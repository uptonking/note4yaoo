---
title: lib-ai-app-examples-rag-knowledge-base
tags: [ai, examples, knowledge-base, large-language-model, rag]
created: 2025-11-30T17:26:44.502Z
modified: 2025-11-30T17:27:16.720Z
---

# lib-ai-app-examples-rag-knowledge-base

# guide

- 优化提取中文文档文字的方案
  - 可参考华人团队的方案, 如 WeKnora, LightRAG
# popular
- https://github.com/pipeshub-ai/pipeshub-ai /2kStar/apache2/202511/python/ts
  - https://pipeshub.com/
  - The OpenSource Alternative to Glean's Workplace AI
  - PipesHub AI helps you quickly find the right information using natural language search—just like Google.
  - The platform not only delivers the most relevant results but also shows where the information came from, with proper citations, using Knowledge Graphs and Page Ranking
  - Beyond search, our platform allows enterprises to create custom apps and AI agents using a No-Code interface.
  - Knowledge Graph Backbone – All data is seamlessly structured into a powerful knowledge graph.
  - Enterprise-Grade Connectors – Scalable, reliable, and built for secure access across your organization.
  - Modular & Scalable Architecture – Every service is loosely coupled to scale independently and adapt to your needs.
  - 前端: Material UI、React Hook Form、zod
  - 后端: fastapi, LangGraph, LangChain, Qdrant(vector), ArangoDB(graph), Kafka, Redis, Docling, PyMuPDF, OCRmyPDF
  - 🛢️ 应用层数据在python侧和nodejs侧都大量使用arangodb来存储图结构的关系
  - 🐛 不支持外部搜索引擎如 Tavily/EXA/SearxNG, 但方便纯本地部署
  - [Work AI for all - AI platform for agents, assistant, search](https://www.glean.com/)
  - [Best way to extract data from PDFs and HTML : r/Rag _202510](https://www.reddit.com/r/Rag/comments/1oavnx4/best_way_to_extract_data_from_pdfs_and_html/)
    - At PipesHub, we use docling, pymupdf (faster than docling but need to use layout parser on top of it), ocrmupdf/Azure DI (scanned pdfs).
    - If you are looking for Higher Accuracy, Visual Citations, Cleaner UI, Direct integration with Google Drive, OneDrive, SharePoint Online, Dropbox and more. PipesHub is free and fully open source, extensible. 
  - pr已合并 [Backend Support for Ollama Models · Pull Request _202507](https://github.com/pipeshub-ai/pipeshub-ai/pull/475)
    - [Ollama Embedding model support · Pull Request ](https://github.com/pipeshub-ai/pipeshub-ai/pull/480)

- https://github.com/MODSetter/SurfSense /10.6kStar/apache2/202511/python/ts
  - https://www.surfsense.com/
  - Open source alternative to NotebookLM, Perplexity, and Glean.
  - Connects to search engines, Slack, Linear, Jira, ClickUp, Notion, YouTube, GitHub, Discord, and more. 
  - Save content from your own personal files (Documents, images, videos and supports 50+ file extensions) to your own personal knowledge base .
  - ⛓️ Get Cited answers just like Perplexity.
  - Works Flawlessly with Ollama local LLMs.
    - 🐛 embedding模型必须使用azure, 不支持本地模型
  - 后端: FastAPI, SQLAlchemy, pgvector, LangGraph, LangChain, Hybrid Search, Rerankers, Redis
  - 前端: next, Vercel AI SDK Kit UI Stream Protocol, Shadcn, Framer Motion, React Hook Form, tanstack/table
  - 依赖chonkie对doc进行embedding
  - ETL Service (choose one)
    - Docling (local processing, no API key required, supports PDF, Office docs, images, HTML, CSV)
    - LlamaIndex API key (enhanced parsing, supports 50+ formats)
  - 👇 xp
    - 跨workspace不能共享source-document
    - 聊天时~~只能选择全部文档或不选文档，不~~可以只选择部分文档
    - 支持根据场景配置不同llm: fast, long, reasoning
    - 🐛 聊天中的内容支持点击跳转到文档的chunk位置，而不是源文件，且中文文档的chunk经常是乱码
  - 📡 [【Feature Request】 Streaming Response for Research Agent _202505](https://github.com/MODSetter/SurfSense/issues/86)
  - https://discord.com/channels/1359368468260192417/1359416865939787837/1409642464792412220
    - I was considering installing Surfsense but it needs API keys, doesn't it? How much does it cost to use it?
    - Every service has a local alternative other than Speech to Text service. No need to put any API keys if you use everything local.
  - https://discord.com/channels/1359368468260192417/1359416891831222362/1437030441910669403  _202511
    - how does embedding work for large documents (not chunks)  if my embedding model’s context window is only 256 or 512 tokens, but the document is tens of thousands of tokens long? 
    - We generate embedding of the summary of doc.

- https://github.com/infiniflow/ragflow /68.2kStar/apache2/202511/python/ts/华人团队
  - https://ragflow.io/
  - https://demo.ragflow.io/
  - open-source RAG (Retrieval-Augmented Generation) engine based on deep document understanding
  - Template-based chunking: Plenty of template options to choose from
  - Grounded citations with reduced hallucinations
  - Supports Word, slides, excel, txt, images, scanned copies, structured data, web pages, and more.
  - Multiple recall paired with fused re-ranking.
  - 依赖 Crawl4AI、elasticsearch、flask-login、minio、pandas、voyageai、pyobvector
  - 未使用langchain/aisdk, 多model-provider的集成完全自定义实现
  - 🌹 对中文的支持较好
  - 实测本地运行很不友好
    - elasticsearch/infinity 数据层还在迁移与优化
    - 本地运行的入口依赖 libjemalloc.so
  - Prerequisites: RAM >= 16 GB
    - gVisor: Required only if you intend to use the code executor (sandbox) feature of RAGFlow.
  - ✨ 实测, rag后的chunk文本可查看chunk与原文对应的细节
    - 聊天的回答中, hover图标能显示引文，并可点击引文后可在页面遮罩侧面弹窗中查看pdf原文位置
  - 🐛 整个 知识库/聊天/查询 的创建及使用交互过于复杂， 不够简洁和自然
  - DeepDoc (Default) - RAGFlowPdfParser
    - Full OCR, Most comprehensive but slower
    - Stream Reading Capability: ✅ YES
    - Page-by-page processing with configurable page_from/page_to
    - Uses `pdfplumber.open()` with `page_from` and `page_to` parameters
    - 使用pdfplumber.open()和pypdf.PdfReader(), 一次性加载整个PDF文件到内存
  - Plain Text Parser - PlainParser
    - Uses `pypdf` for text extraction only
    - Only for text-based PDFs
    - Stream Reading Capability: ✅ YES
    - Uses `pypdf.PdfReader` with page ranges
    - Memory Usage: Very low - only text content loaded
    - 可以逐页处理，但仍需要加载完整PDF
  - Docling Parser - DoclingParser
    -  Uses `docling.DocumentConverter` with full file
  - MinerU Parser - MinerUParser
    - External tool, entire file processing
  - TCADP Parser - TCADPParser
    - Tencent Cloud API integration
    - Cloud-based, file upload to Tencent Cloud
    - Reading Method: Converts entire file to `base64` and uploads, entire file loaded into memory for Base64 conversion
  - Vision Parser - VisionParser
    - Visual model processing, full file
    - Higher memory requirements
    - Uses `pdfplumber` with full file access
  - [HARD -- Efficient way to use enterprise dataset without uploading all files? _202509](https://github.com/orgs/infiniflow/discussions/10388)
    - You have to upload the data from Azure to RAGFlow. And currently you can do that through API. From 0.22 which is going to be launched in this Nov, we will provide some data sources and you can ingest data by just click several buttons. And more data sources could be easily added.
  - [[Question]: Why can't knowledge graphs be used? _202509](https://github.com/infiniflow/ragflow/issues/10017)
    - Knowledge graphs can’t currently be used with the Table chunking method in RAGFlow. The reason is that table chunking treats each row as a separate chunk and stores field mappings for retrieval, but it does not run those chunks through the knowledge graph extraction pipeline. As a result, entity–relationship extraction is skipped for tables.
    - If you need a knowledge graph from table data, you’d have to implement a custom post-processing step (e.g., parsing the rows yourself and generating triples).
  - [Select PDF parser | RAGFlow](https://ragflow.io/docs/dev/select_pdf_parser)
  - [Deploy local models | RAGFlow](https://ragflow.io/docs/dev/deploy_local_llm)
    - RAGFlow supports deploying models locally using Ollama, Xinference, IPEX-LLM, or jina.
  - 🐛 [[Bug]: Fail to access model(text-embedding-bge-reranker-v2-m3). The LmStudioRerank has not been implement _202502](https://github.com/infiniflow/ragflow/issues/5354)
    - Unable to add reranker model for LM STUDIO，Fail to access model(text-embedding-bge-reranker-v2-m3).The LmStudioRerank has not been implement
  - 🐛 [[Question]: Support for calling the OLLAMA Reranker models ？ _202509](https://github.com/infiniflow/ragflow/issues/8988)
    - Ollama supports very few rerank models and is not recommended.
  - [FAQs | RAGFlow](https://ragflow.io/docs/dev/faq)
    - RAGFlow supports MinerU (>= 2.6.3) as an optional PDF parser with multiple backends. RAGFlow acts only as a client for MinerU, calling it to parse documents, reading the output files, and ingesting the parsed content.
  - [[Question]: Big File Parsing ](https://github.com/infiniflow/ragflow/issues/10986)
  - [[Question]: High Memory and CPU Usage During PDF Parsing _202505](https://github.com/infiniflow/ragflow/issues/7602)
    - 原因找到了，用了deepdoc解析方式，就非常消耗资源，我用native就没问题。目前不需要图片识别，就不需要deepdoc
  - [Questions about Ragflow _202507](https://github.com/orgs/infiniflow/discussions/8904)
    - RAGFlow uses Elasticsearch by default. Is Elasticsearch your recommendation over Infinity (at version 0.19.1)?
    - Pls choose Elasticsearch. We're refactoring Infinity.
  - 🐛 [[Question]: Parsing resumes is not open source yet. Are there any plans to open source it in the future? ](https://github.com/infiniflow/ragflow/issues/1053)
    - 202406: currently, we don't have such plan.
  - [[Question]: How to using this "Team" option for open-source? ](https://github.com/infiniflow/ragflow/issues/7050)
    - 202504: It's a feature of enterprise version.

- https://github.com/Tencent/WeKnora /7.5kStar/MIT/202511/go/ts/vue
  - https://weknora.weixin.qq.com/
  - LLM-powered framework for deep document understanding, semantic retrieval, and context-aware answers using RAG paradigm
  - 📡 [WeKnora Roadmap ](https://github.com/Tencent/WeKnora/issues/414)
    - Vision: 独立部署个人知识库，支持文档、数据、图片，基于传统RAG框架拓展更多LLM应用场景
  - [[Question]: 请问有计划支持MinerU、PP-Structure-V3等第三方解析服务的调用么? 以及是否支持更多像lightrag这种graph的构建？ _202509](https://github.com/Tencent/WeKnora/issues/248)
    - 现在支持了PPOCR-V4.PP-Structure-V3当然也是可以的，具体解析逻辑在docreader这个模块中。
    - MinerU这块暂时没有详细调研，docreader在设计上是一个Python的独立模块，理论上可以比较轻松的接入其他SDK。
    - graphRag这块我们现在有按照我们的索引结构进行实现。如果有更好的方式，感觉可以按照多路索引的思路进行单独一路的实现
  - 🐛 [文档解析失败 _202508](https://github.com/Tencent/WeKnora/issues/77)
    - 刚刚找到解决方法了，疑似是调用通过本地ollama 模型的问题； 解决方法就是通过api去调用embedding模型，虽然配置时会提示报错，但是可以是保存的，保存后也可以使用。再次上传时就解析成功了
  - [[Question]: 上传大文件怎么办？ _202510](https://github.com/Tencent/WeKnora/issues/348)
    - 这个应该是nginx的配置问题吧。先进入前端文件夹，修改nginx.conf文件
    - 比如，将最大文件修改为200M,将上传时间修改为300s;
      - 将client_max_body_size 50M ;修改为200M;
      - client_max_body_size 200M
      - proxy_connect_timeout 300s;
  - [[Question]: 解除了30M的限制之后解析失败了 ](https://github.com/Tencent/WeKnora/issues/245)
    - 找到了问题了 给 gRPC 消息大小设置为 5GB 这好像是超范围了 修改为500M后 就能正常解析了，大概在65M左右的一个pdf解析了将近15分钟 不知道是不是我电脑性能的问题 m1 pro 32
    - 目前有并发性能问题，后面会进一步优化
  - [[Bug]: 使用bge-m3导入文本知识库超过一定字符就失败 ](https://github.com/Tencent/WeKnora/issues/410)
    - 使用bge-m3向量化模型，本地txt文本文件导入知识库的过程中，当文档字符大于等于2w时，就会导入失败，而适当删除字符，比如19997，则可以正常导入。初步推测有一个2万的限制？从任务管理器的资源情况来看，机器资源在健康水位，所以不是机器资源的问题
  - [[Feature]: 知识库是否能支持上传文件夹 _202511](https://github.com/Tencent/WeKnora/issues/388)
    - 还没有计划放开这个功能，如果一次性上传文件过多，多服务负载来说不是一件好事情
  - [[Question]: 知识图谱  ](https://github.com/Tencent/WeKnora/issues/364)
    - 发现问题了，是模型的问题，知识图谱的构建需要json格式，之前使用的是推理模型，包含了think标签，所以一直失败。 
    - 如果我想关闭知识图谱的构建以及禁止它依据知识图谱进行检索，只需要“ENABLE_GRAPH_RAG=False”就可以了吗？想做一下有无知识图谱情况下的检索性能的对比
    - 是的。然后重启重新上传就好
  - [[Question]: 只能通过知识库的内容问答，知识库中没有内容时，无返回 ](https://github.com/Tencent/WeKnora/issues/359)
    - 期望在知识库检索不到时，大模型也可以输出
    - 这样设计的目的是为了防止模型输出一些危险的，无法预测的内容
    - 可以修改summary prompt, 把 NO_MATCH 的话术从 Prompt中去掉，改成你想要的

- https://github.com/UnicomAI/wanwu /2.7kStar/apache2/202511/go/🆚
  - 元景万悟智能体平台是一款面向企业级场景的一站式、商用license友好的智能体开发平台
  - 多租户架构：提供多租户账号体系，满足用户成本控制、数据安全隔离、业务弹性扩展、行业定制化、快速上线及生态协同等核心需求
  - 🆚 提供了竞品比较: dify, fastgpt, ragflow, coze
  - 信创适配：已适配国产信创数据库TiDB和OceanBase
  - model hub: 支持用户导入包括联通元景、OpenAI-API-compatible、Ollama、通义千问、火山引擎等模型供应商的LLM、Embedding、Rerank模型
  - 提供 多推理后端支持（vLLM、TGI等）与 自托管解决方案，满足不同规模企业的算力需求
  - 联网检索（Web Search）
  - 可视化工作流（Workflow Studio）
  - 企业级知识库、RAG Pipeline:  提供知识库创建→ 文档解析→向量化→检索→精排 的全流程知识管理能力，支持pdf/docx/txt/xlsx/csv/pptx等 多种格式 文档，还支持网页资源的抓取和接入
  - 提供 RESTful API ，支持与企业现有系统（OA/CRM/ERP等）深度集成

- https://github.com/pingcap/autoflow /2.6kStar/apache2/202507/python
  - https://tidb.ai/
  - a Graph RAG based and conversational knowledge base tool built with TiDB Serverless Vector Storage.
  - An open source GraphRAG (Knowledge Graph) built on top of TiDB Vector and LlamaIndex and DSPy.
  - UI交互类似chatgpt
  - https://x.com/9hills/status/1862522244527972625
    - RAG Demo 到 RAG Application 难度的完美表现，其实功能不算丰富（增加了 Graph RAG和 Agent RAG 的思想），
    - 代码却不得不做的非常复杂，大部分其实是应用逻辑。 P. S. 代码已经成熟到可以直接抄了，直接复刻就完了

- https://github.com/netease-youdao/QAnything /13.8kStar/apache2 > AGPL/202503/python/vue/inactive
  - https://qanything.ai/
  - 开源的企业级本地知识库问答解决方案，致力于支持任意格式文件或数据库的问答
  - 模型数据全在本地，可断网使用
  - Support selecting multiple knowledge bases for Q&A
  - Currently supported formats include: PDF(pdf), Word(docx), PPT(pptx), XLS(xlsx), Markdown(md), Email(eml), TXT(txt), Image(jpg，jpeg，png), CSV(csv), Web links(html) and more
  - https://github.com/netease-youdao/BCEmbedding /apache2/202409/python/inactive
    - 由网易有道开发的中英双语和跨语种语义表征算法模型库，其中包含 EmbeddingModel和 RerankerModel两类基础模型
    - EmbeddingModel专门用于生成语义向量，在语义搜索和问答中起着关键作用，而 RerankerModel擅长优化语义搜索结果和语义相关顺序精排。
    - BCEmbedding作为有道的检索增强生成式应用（RAG）的基石，特别是在QAnything中发挥着重要作用
    - 双语和跨语种能力：基于有道翻译引擎的强大能力，BCEmbedding实现强大的中英双语和跨语种语义表征能力
    - 面向RAG做针对性优化，可适配大多数相关任务，比如翻译，摘要，问答等。此外，针对 问题理解（query understanding） 也做了针对优化

- https://github.com/Future-House/paper-qa /7.9kStar/apache2/202511/python
  - https://futurehouse.gitbook.io/futurehouse-cookbook
  - PaperQA2 is a package for doing high-accuracy retrieval augmented generation (RAG) on PDFs, text files, Microsoft Office documents, and source code files, with a focus on the scientific literature.
  - A usable full-text search engine for a local repository of PDF/text files.
  - You can use llama.cpp to be the LLM. You won't get good performance with 7B models.
  - [save and import embeddings for faster answer generation _202411](https://github.com/Future-House/paper-qa/issues/721)
    - I’ve been able to use it to ask questions by providing over 100 papers as input, and I’ve been using only local models via Ollama. Everything is working well, but I’d like to know how I can avoid reloading the same files and retraining an embedding model each time I have a new Question.
    - 🔡 需要手动修改embedding模型配置, 而不是使用默认openai模型
  - [usage with large local paper results exceeding `text-embeeded`'s maximium prompt limit _202409](https://github.com/Future-House/paper-qa/issues/453)
    - I'm using paperqa with CLI frontend, while this could apply to code usage too. just run pqa ask cusum in a directory with a 10MiB Chinese paper pdf, results an error 'exceeding 8192 tokens limit' using OpenAI third-party proxy API (did some trick in litellm to actually set api_base)
    - We could call tokenizer, or ask litellm to support pre-check before api call (this will be better)
# rag-examples
- https://github.com/pymupdf/pymupdf4llm /1.2kStar/AGPL/202511/python/lib
  - https://pymupdf.readthedocs.io/en/latest/pymupdf4llm
  - a specialized extension of PyMuPDF designed specifically for extracting content from PDFs in a format that's optimized for LLMs
  - Converts PDFs to clean, structured Markdown format
  - Automatically identifies headers, paragraphs, tables, and images
  - Preserves document hierarchy (headers, lists, tables)
  - Maintains document layout and reading order: process multi-column pages
  - Extracts images from PDFs: save images separately or encode them inline
  - [Build a Multimodal RAG using — PyMuPDF4LLM-llamaindex-Qdrant _202411](https://ai.gopubby.com/build-a-multimodal-rag-using-pymupdf4llm-llamaindex-qdrant-e9d23a4409cc)

- https://github.com/danny-avila/rag_api /710Star/MIT/202508/python/librechat
  - [RAG API - Chat with files](https://www.librechat.ai/docs/features/rag_api)
  - This project integrates Langchain with FastAPI in an Asynchronous, Scalable manner, providing a framework for document indexing and retrieval, using PostgreSQL/pgvector.
  - Files are organized into embeddings by `file_id`. The primary use case is for integration with LibreChat, but this simple API can be used for any ID-based use case.
  - The main reason to use the ID approach is to work with embeddings on a file-level. This makes for targeted queries when combined with file metadata stored in a database, such as is done by LibreChat.
  - [[Enhancement] Reduce memory consumption greatly, and speed up process slighlty by processing file async and inserting to vectordb in chunks rather than all at once _202510](https://github.com/danny-avila/rag_api/issues/213)
    - Currently RAG creates embeddings for the file holding them all in memory then bulk inserts them all into the vectordb. When embedding very large files this consumes a vast amount of memory
    - This is largely solved by changing the logic such that it breaks the file up into chucks and embeds each separately, and asynchronously bulk inserting each chunk individually as the embedding process completes each chunk. 
    - pr未合并
  - [[Issue] `/health` endpoint becomes unresponsive during large file processing _202510](https://github.com/danny-avila/rag_api/issues/216)
    - When uploading and processing large files, the /health endpoint becomes unresponsive until the processing is complete.

- https://github.com/clusterzx/paperless-ai /4.6kStar/MIT/202511/python/js
  - https://clusterzx.github.io/paperless-ai/
  - an AI-powered extension for Paperless-ngx that brings automatic document classification, smart tagging, and semantic search using OpenAI-compatible APIs and Ollama.
  - [Paperless-AI: Now including a RAG Chat for all of your documents : r/selfhosted _202505](https://www.reddit.com/r/selfhosted/comments/1kqbouu/paperlessai_now_including_a_rag_chat_for_all_of/)
  - [Paperless-ai runs well on local chatgpt-oss installation  _202510](https://github.com/clusterzx/paperless-ai/discussions/749)
    - I installed chatgpt-oss-20b FP16 model, using koboldcpp on a Ryzen 7 7840HS mini pc with 32G RAM. Using -- usevulkan all 25 layers of the model can offloaded to gpu using VRAM. There is no major speed reduction when using FP16, as compared to Q4 etc.! Running on proxmox / debian LXC.
    - For the first 100 docs, the results are very good for my mostly German documents. Processing time is mostly below 10 seconds per document for smaller 1-3 page and 30-40 seconds for larger documents. Works fine for me.

- https://github.com/ari99/lm_studio_big_rag_plugin /202511/ts
  - LM Studio Plugin to mark a directory full of documents as a RAG source and another directory as the Vectorstore and build a RAG for use in your queries. Built using Cursor.
  - Massive Scale: Designed to handle large document collections (GB to TB scale)
  - Deep Directory Scanning: Recursively scans all subdirectories
  - PDF parsing via pdf-parse
  - Multiple File Formats: Supports HTM, HTML, XHTML, PDF, EPUB, TXT, TEXT, Markdown variants (MD/MDX), BMP, JPEG, PNG
  - OCR Support: Optional OCR for image files using Tesseract.js
  - Vector Search: Uses LanceDB for efficient vector storage and retrieval
  - Persistent Storage: Vector embeddings are stored locally and persist across sessions
  - Incremental Indexing: Automatically detects and skips already-indexed files
  - Concurrent Processing: Configurable concurrency for optimal performance
  - Disk Space: The vector store requires additional disk space (typically 10-20% of original document size)
  - Initial Indexing: Can take several hours for TB-scale collections
  - Memory Usage: Scales with concurrent processing (reduce maxConcurrentFiles if needed)
  - Limitations
    - RAR Archives: Not yet implemented (files are skipped)
    - Very Large Files: Individual files >100MB may cause memory issues
    - Non-English OCR: Currently only English OCR is configured

- https://github.com/2dogsandanerd/Knowledge-Base-Self-Hosting-Kit /MIT/202511/python
  - A Docker-powered RAG system that understands the difference between code and prose. 
  - Ingest your codebase and documentation, then query them with full privacy and zero configuration.
  - Different chunking strategies for code vs. prose
    - Code collections use AST-based chunking that respects function boundaries
    - Document collections use semantic chunking optimized for prose
  - Backend: FastAPI, LlamaIndex 0.12.9
  - Vector DB: ChromaDB 0.5.23
  - LLM/Embeddings: Ollama (configurable)
  - Document Parser: Docling 2.13.0 (advanced OCR, table extraction)
  - Frontend: Vanilla HTML/JS (no build step)
  - Batch Ingestion — Process multiple files (sequential processing in Community Edition)
  - 🧪
    - chroma run --host 0.0.0.0 --port 8000 --path ~/Documents/repos/libfwk/ai-llm/all-rag/Knowledge-Base-Self-Hosting-Kit/backend/ENV/ingestdb
    - OLLAMA_DEBUG=2 ollama serve
    - uv run --env-file .env -- uvicorn src.main:app --port 8080
  - [I spent 2 years building privacy-first local AI. My conclusion: Ingestion is the bottleneck, not the Model. (Showcase: Ollama + Docling RAG Kit) : r/LocalLLaMA _202512](https://www.reddit.com/r/LocalLLaMA/comments/1pamu5t/i_spent_2_years_building_privacyfirst_local_ai_my/)
    - I’ve been working on strictly local, data-privacy-compliant AI solutions for about two years
    - The biggest lesson I learned: We spend 90% of our time debating model quantization, VRAM, and context windows. But in real-world implementations, the project usually fails long before the prompt hits the LLM. It fails at Ingestion.
    - I built a self-hosting starter kit that focuses heavily on fixing the Input Layer before worrying about the model.
    - Ingestion: Docling (v2). I chose this over PyPDF/LangChain splitters because it actually performs layout analysis. It reconstructs tables and headers into Markdown, so the LLM isn't guessing when reading a row.
    - I’d love to hear your thoughts on the "Ingestion First" approach. For me, switching from simple text-splitting to layout-aware parsing was the game changer for retrieval accuracy.
  - 👾 prompts-agent
    - i have run this project fully locally without docker and nginx.
    - the backend server starts by `cd backend && uv run --env-file .env -- uvicorn src.main:app --port 8080`.

- https://github.com/djleamen/doc-reader /MIT/202511/python/django
  - A Django-based document Q&A system using Retrieval-Augmented Generation (RAG) to process and query large documents with AI-powered responses.
  - Large Document Support: Handle documents up to 800k+ words
  - Multiple Formats: PDF, DOCX, TXT, and Markdown support
  - REST API: Django REST Framework for integrations
  - Vector Search: FAISS/ChromaDB/Pinecone vector databases
  - CLI Tools: Command-line interface for batch operations
  - Memory issues with large docs: Reduce `CHUNK_SIZE` in `.env` or process documents individually

- https://github.com/renton4code/pdf-rag /AGPL/202502/ts/inactive
  - A production-ready template for building Retrieval-Augmented Generation (RAG) applications. 
  - This template provides a complete setup for document processing, vector storage, and AI-powered question answering with kickass UI.
  - PDF document processing with OCR
  - Milvus DB with billions of vectors scale support: Vector DB for storing embeddings
  - PostgreSQL: Relational DB for metadata storage
  - Click-to-view document references with highlighting
  - Large documents processing and status updates
  - AI/ML: Google Gemini (LLM), HuggingFace Transformers (Embeddings)
  - Backend: Bun
  - Based on Q&A with a large document (700+ pages) in comparison to RagFlow

- https://github.com/gptme/gptme-rag /MIT/202511/python/cli
  - Local RAG as a simple CLI
  - Built primarily for gptme, but can be used standalone.
  - Document indexing with ChromaDB
  - Streaming large file handling: chunking splits large documents into manageable pieces
  - File watching and auto-indexing: Real-time index updates, batch processing
  - https://github.com/gptme/gptme /4.1kStar/MIT/202511/python
    - Your agent in your terminal, equipped with local tools: writes code, uses the terminal, browses the web, vision

- https://github.com/thiswillbeyourgithub/wdoc /GPL/202511/python
  - https://wdoc.readthedocs.io/en/stable/
  - Summarize and query from a lot of heterogeneous documents. 

- https://github.com/IlyaRice/RAG-Challenge-2 /MIT/202503/python/inactive
  - [Ilya Rice: How I Won the Enterprise RAG Challenge _202503](https://abdullin.com/ilya/how-to-build-best-rag/)
  - Custom PDF parsing with Docling
  - Vector search with parent document retrieval: Faiss from Meta for efficient similarity search and clustering of dense vectors.
  - LLM reranking for improved context relevance
  - Structured output prompting with chain-of-thought reasoning
  - Query routing for multi-company comparisons
  - You'll need your own API keys for OpenAI/Gemini
  - [5.4 Enterprise-level RAG Practice (I) | AI Roadmap](https://comfyai.app/article/llm-applications/enterprise-level-rag-hands-on-practice)

- https://github.com/in-tech-gration/LangChain-RAG /202503/js/inactive
  - A simple RAG application for doing question-answering on a PDF document
  - This repository contains the JavaScript version of the python RAG implementation by Jodie Burchell using LangChain as demoed in her Beyond the Hype: A Realistic Look at Large Language Models GOTO 2024 presentation.
  - Uses LangChain.js v0.2
  - Key differences between the original python repository and the JavaScript version
    - This code uses two types of Vector stores instead of one. The original code used the ChromaDB vector store, whereas this repo contains code using ChromaDB but also code using the In-memory vector store module provided by LangChain.js.
    - The original repo contains a large PDF (pycharm-documentation.pdf which is around 174MB) that is used in the demo. This is a great source to test and also compare the results with the demo, but it turns out that it takes quite a lot of time to get vectorized. 
    - https://github.com/slvg01/90.10d_RAG_OnTheFly
      - you can upload any PDF document, with a limit of 200 MB per file. You can upload as many PDFs as you'd like.
      - Upload PDF files which are combined into one big text chunk.
    - [Machine-Learning/Optimizing RAG with Document Chunking Techniques Using Python.md at main · xbeat/Machine-Learning](https://github.com/xbeat/Machine-Learning/blob/main/Optimizing%20RAG%20with%20Document%20Chunking%20Techniques%20Using%20Python.md)

- https://github.com/Gopendranath/Rag-pdf-chat-backend /202511/js
  - This backend server provides comprehensive file upload functionality for handling images, documents, and messages in a chat application.
  - Multiple File Upload: Support for uploading multiple images and documents simultaneously
  - File Size Limits: 10MB maximum file size per file
  - Static File Serving: Uploaded files are served statically via /uploads/* endpoint
  - This project can use a vector-enabled PostgreSQL (pgvector) for embeddings and MongoDB for document storage.
  - https://github.com/Gopendranath/frontend-rag-chat-agent /ts

- https://github.com/iamarunbrahma/rag-ingest /MIT/202411/python/inactive
  - tool designed to seamlessly convert PDF documents into markdown format while preserving the original layout and formatting
  - The extracted content is indexed in a vector database (Qdrant) to enhance RAG
  - Advanced text extraction with layout preservation using PyMuPDF
  - Uses Ollama model for contextual enhancement of document chunks
  - Combines dense and sparse embeddings via Qdrant for improved retrieval
  - Memory Issues: Process large PDFs in smaller batches

- https://github.com/yash1912/colpali-rag /202410/python/单文件/inactive
  - RAG solution leveraging cutting-edge AI models like ColPali and Qwen2VL.
  - converts PDFs into searchable embeddings using ColPali's AI model

- https://github.com/datawhalechina/all-in-rag /202511/python
  - https://datawhalechina.github.io/all-in-rag/
  - 大模型应用开发实战一：RAG 技术全栈指南，在线阅读
  - https://github.com/yksanjo/all-in-rag

- https://github.com/ZohaibCodez/document-qa-rag-system /MIT/202509/python/inactive
  - https://document-rag-system.streamlit.app/
  - RAG project built with LangChain and Streamlit. 
  - Upload documents (PDF/TXT) and interact with them using natural language questions powered by embeddings and vector search.
  - Vector-based similarity search using FAISS
  - Frontend: Streamlit
  - Limitations
    - File Types: Currently supports only PDF and TXT formats
    - Large documents (>50 pages) may take longer to process
    - Scanned PDFs: Does not support OCR for image-based PDFs
    - Large PDF files (>100MB) may cause memory issues
    - Embedded images in PDFs are not processed
    - Some complex PDF layouts may not parse correctly

- https://github.com/pratheeshkumar99/Document-based-Question-Answering-System /202408/python/inactive
  - This project demonstrates a Retrieval-Augmented Generation (RAG) system for question answering. 
  - It integrates OpenAI’s GPT-4 model with FAISS for vector similarity search
  - Vector Store: The embeddings are stored in FAISS (Facebook AI Similarity Search)
  - Handles large documents by splitting them into smaller chunks, ensuring efficient processing and retrieval.

- https://github.com/BjornMelin/docmind-ai-llm /MIT/202509/python/功能丰富
  - open-source Streamlit application leveraging LlamaIndex, LangGraph, and local Large Language Models (LLMs) via Ollama, LMStudio, llama.cpp, or vLLM for advanced document analysis. 
  - provides local document analysis with zero cloud dependency
  - This system combines hybrid search (dense + sparse embeddings), knowledge graph extraction, and a 5-agent coordination system to extract and analyze information from your PDFs, Office docs, and multimedia content.
  - Built on LlamaIndex pipelines with LangGraph supervisor orchestration and Qwen3-4B-Instruct-2507's FULL 262K context capability through INT8 KV cache optimization
  - Offline-First Design: 100% local processing with no external API dependencies.
  - Enable Chunked Analysis for large documents, Late Chunking for accuracy, or Multi-Vector Embeddings for enhanced retrieval.
  - LlamaIndex `IngestionPipeline` orchestrates Unstructured parsing, deterministic hashing, DuckDB caching, and AES-GCM page image handling with OpenTelemetry spans for each run.
  - Retrieval/Router: RouterQueryEngine composed via router_factory with tools semantic_search, hybrid_search (Qdrant server‑side fusion), and optional knowledge_graph; uses async/batching where appropriate.
  - Hybrid Retrieval: Qdrant Query API server‑side fusion (RRF default, DBSF optional) over named vectors text-dense (BGE‑M3; COSINE) and text-sparse (FastEmbed BM42/BM25 with IDF). Dense via LlamaIndex; sparse via FastEmbed.
  - Feature Flags: Boolean environment variables for experimental features

- https://github.com/ricardolx/rag-query /202401/ts/inactive
  - [Implement RAG for large document search— semantic search with a vector database and LLM _202401](https://medium.com/@ricrivero3/implement-large-document-search-using-rag-semantic-search-with-a-vector-database-and-llm-b798675dca08)
  - Backend — Firebase Cloud Functions
  - Database — Firestore
  - Vector DB — Pinecone
  - LLM — OpenAI

- https://github.com/chaanakyaaM/QueryPDF /202507/python/代码少/inactive
  - a local-first, terminal-based RAG tool that allows users to interact with PDF documents using natural language, entirely offline.
  - It extracts text from user-specified pages, chunks it intelligently, embeds the content, and stores it in a local vector database.
  - Local Caching: Caches both tokenizers and embedding models locally for offline use and faster future runs.
  - Graceful Exit Handling: Automatically cleans up ChromaDB collections on exit.
  - Visual Progress Feedback: Shows embedding generation progress.
  - Uses semantic search to find the most relevant chunks for your questions.
  - Fully Customizable: Users can configure embedding model, LLMs, and chunk parameters via a simple JSON file.

- https://github.com/raghavan/pdfgptindexer-offline /MIT/202511/python
  - local RAG system for indexing and querying PDF documents
  - PyMuPDF for text extraction
  - Text Splitting: LangChain's RecursiveCharacterTextSplitter
  - Embeddings: HuggingFace Sentence Transformers (local)
  - Vector Store: FAISS for efficient similarity search
  - LLM: Ollama (local LLM runner)
  - Larger PDFs take longer to index - be patient
  - The FAISS index can be reused - you don't need to re-index unless PDFs change
  - https://github.com/amithkoujalgi/ollama-pdf-bot /202502/strealit
  - https://github.com/tonykipkemboi/ollama_pdf_rag /202501/streamlit

- https://github.com/drisskhattabi6/Chat-with-PDF-Locally /202505/python/inactive
  - An advanced chatbot using Ollama / Sambanova LLMs to interactively extract information from PDFs, Using Streamlit & Ollama / Sambanova API and langchain
  - uses the Marker library to convert PDFs to Markdown format. 
  - Text Chunking: Large documents are split into manageable chunks for easier processing.
  - Embedded Models: The app supports Ollama models for document embeddings and generating answers based on the content.
  - Chroma Vector Store: All the processed documents are stored in a Chroma vector store for efficient retrieval.

- https://github.com/krey-yon/Cliven /MIT/202506/python/inactive
  - a command-line tool that allows you to process PDF documents and have interactive conversations with their content using local AI models. 
  - using ChromaDB for vector storage and Ollama for AI inference.

- https://github.com/codesniper99/LLM-Tinkering /202508/python/inactive
  - This repository enables semantic search and question-answering on research papers using PDF ingestion, vector databases, and local or cloud-hosted LLM

- https://github.com/jacoblee93/fully-local-pdf-chatbot /MIT/202410/ts/inactive
  - another chat over documents implementation... but this one is entirely local
  - Exposing a port to a local LLM running on your desktop via Ollama.
  - Downloading weights into your browser and running via WebLLM.

- https://github.com/AvaAvarai/Local_Small_LM_Document_RAG /MIT/202409/python/inactive
  - Local Document Retrieval Augmented Generation (RAG) with sentence embedding context for cited question answering with small language models (LM).
  - Currently runs in terminal again, will add GUI back soon.

- https://github.com/snexus/llm-search /MIT/202506/python/inactive
  - RAG with a simple YAML-based configuration that enables interaction with a collection of local documents.
  - The package is designed to work with custom Large Language Models (LLMs) – whether from OpenAI or installed locally.

- https://github.com/swirlai/swirl-search /2.9kStar/apache2/202511/python
  - https://swirlaiconnect.com/
  - AI Search & RAG Without Moving Your Data. Get instant answers from your company's knowledge across 100+ apps
  - Warning: The Docker version of Swirl does not retain any data or configuration when shut down
  - Swirl comes configured to search Arxiv, European PMC and Google News right out of the box.

- https://github.com/KeiranHome/Rag_demo /202505/python/inactive
  - 本项目利用FAISS向量库和千问模型API构建了一个检索增强生成（RAG）系统，旨在为用户提供针对公司年度总结数据的智能问答服务
  - 中文分词工具：Jieba/THULAC，用于断句和关键词提取，提升后续Embedding语义表征精度。
  - 通义千问Embedding模型：专为中文优化，支持长文本语义编码（最长16K tokens），余弦相似度准确率较开源模型（如BERT-base）提升15%；
# rag-fwk
- https://github.com/phbst/tinyRAG /202409/jupyter/inactive
  - 全手写的一个RAG应用。Langchain的大部分库会很方便，但是你不一定理解其中原理，所以代码尽可能展现基本算法，主打理解RAG的原理

- https://github.com/codemilestones/TinyCodeBase /apache2/202509/python
  - 本项目是一个轻量级的代码智能系统，包含了RAG（检索增强生成）、Agent（智能代理）和评估系统的完整实现。
  - 项目从[TinyRAG](https://github.com/KMnO4-zx/TinyRAG)扩展而来，专注于代码场景的优化和实践。
  - [之前有多嫌弃大模型框架，现在用 LangGraph 就有多香 - 知乎 _202509](https://zhuanlan.zhihu.com/p/1946396924342177830)

- https://github.com/wzdavid/ThinkRAG /MIT/202507/python/inactive
  - 大模型检索增强生成系统，可以轻松部署在笔记本电脑上，实现本地知识库智能问答
  - built on LlamaIndex and Streamlit, and has been optimized for Chinese users in various fields such as model selection and text processing.
  - Supports locally deployed models and offline use
  - a lot of customizations and optimizations for Chinese users:
    - Uses Spacy text splitter for better handling of Chinese characters
    - Uses Chinese prompt templates for Q&A and refinement processes
    - Uses bilingual embedding models, such as `bge-large-zh-v1.5` from BAAI

- https://github.com/HKUDS/RAG-Anything /10.7kStar/MIT/202511/python
  - All-in-One Multimodal Document Processing RAG system built on LightRAG.
  - As a unified solution, RAG-Anything eliminates the need for multiple specialized tools. It provides seamless processing and querying across all content modalities within a single integrated framework. 
  - [[Question]: 我使用中文数据构建了RAG，但是为什么检索出来的内容是英文的？ _202510](https://github.com/HKUDS/RAG-Anything/issues/136)
    - .env里好像有个语言设置，默认是英文，可以看看和这个是否有关
  - [[Question]: 目前是否支持长表格的导入 _202509](https://github.com/HKUDS/RAG-Anything/issues/100)
  - https://github.com/HKUDS/LightRAG /20.1kStar/MIT/202508/python
    - Simple and Fast Retrieval-Augmented Generation
    - [2025.06.16]🎯 Our team has released RAG-Anything an All-in-One Multimodal RAG System for seamless text, image, table, and equation processing.
- https://github.com/xerrors/Yuxi-Know /2.6kStar/MIT/202512/python/vue
  - https://xerrors.github.io/Yuxi-Know/
  - 功能强大的智能体平台，融合了 RAG 知识库与知识图谱技术，基于 LangGraph v1 + Vue.js + FastAPI + LightRAG 架构构建
  - 集成主流大模型、LightRAG、MinerU、PP-Structure、Neo4j 、联网检索、工具调用。

- https://github.com/getzep/graphiti /20.6kStar/apache2/202511/python
  - https://help.getzep.com/graphiti
  - a framework for building and querying temporally-aware knowledge graphs
  - Unlike traditional RAG, Graphiti continuously integrates user interactions, structured and unstructured enterprise data, and external information into a coherent, queryable graph. 
  - The framework supports incremental data updates, efficient retrieval, and precise historical queries without requiring complete graph recomputation
  - Graphiti powers the core of Zep, a turn-key context engineering platform for AI Agents.
  - Traditional RAG approaches often rely on batch processing and static data summarization, making them inefficient for frequently changing data. 
  - Real-Time Incremental Updates: Immediate integration of new data episodes without batch recomputation.
  - Scalability: Efficiently manages large datasets with parallel processing, suitable for enterprise environments.

- https://github.com/chunkhound/chunkhound /118Star/MIT/202509/python
  - https://chunkhound.github.io/
  - Deep Research for Code & Files
  - Transform your codebase into a searchable knowledge base for AI assistants using semantic search via cAST algorithm and regex search. 
  - Integrates with AI assistants via the Model Context Protocol (MCP).
  - cAST Algorithm - Research-backed semantic code chunking
  - Multi-Hop Semantic Search - Discovers interconnected code relationships beyond direct matches
  - Semantic search - Natural language queries like "find authentication code"
  - Regex search - Pattern matching without API keys
  - Local-first - Your code stays on your machine
  - 22 languages with structured parsing, via Tree-sitter

- https://github.com/memfreeme/memfree /MIT/202409/ts
  - https://www.memfree.me/
  - MemFree is a Hybrid AI Search Engine.
  - Search and ask questions with text, images, files, and web pages.
  - Multi AI Models: ChatGPT, Claude, Gemini
  - 支持多模态（图片、文字、文件），多来源（Twitter、学术、本地知识库），多种表现形式（思维导图、图片音视频）等混合搜索形态

- https://github.com/KruxAI/ragbuilder /apache2/202410/python
  - https://docs.ragbuilder.io/
  - A toolkit to create optimal Production-readyRetrieval Augmented Generation(RAG) setup for your data
  - By performing hyperparameter tuning on various RAG parameters (Eg: chunking strategy: semantic, character etc., chunk size: 1000, 2000 etc.), RagBuilder evaluates these configurations against a test dataset to identify the best-performing setup for your data.

- https://github.com/llmware-ai/llmware /14.5kStar/apache2/202507/python/inactive
  - https://llmware-ai.github.io/llmware/
  - a unified framework for building LLM-based applications (e.g., RAG, Agents), using small, specialized models that can be deployed privately
  - llmware has two main components:
    - RAG Pipeline - integrated components for the full lifecycle of connecting knowledge sources to ai models
    - 50+ small, specialized models fine-tuned for key tasks in enterprise process automation, including fact-based question-answering, classification, summarization, and extraction
  - RAG-Optimized Models - 1-7B parameter models designed for RAG workflow integration and running locally.

- https://github.com/VectifyAI/PageIndex /4.1kStar/MIT/202511/pyhton
  - https://pageindex.ai/
  - Inspired by AlphaGo, we propose PageIndex — a vectorless, reasoning-based RAG system that builds a hierarchical tree index for long documents and reasons over that index for retrieval. 
  - [RAG without Vectors – PageIndex: Reasoning-Based Document Indexing · run-llama/llama_index _202504](https://github.com/run-llama/llama_index/discussions/18360)
    - We were frustrated by vector-based RAG systems that rely on semantic similarity and often fail on long, domain-specific documents.
    - PageIndex, a hierarchical indexing system that transforms large documents (like financial reports, regulatory documents, or textbooks) into semantic trees optimized for reasoning-based RAG.

- https://github.com/dataelement/bisheng /10.5kStar/apache2/202511/python/ts
  - http://www.bisheng.ai/
  - open LLM devops platform 
  - Powerful and comprehensive features include: GenAI workflow, RAG, Agent, Unified model management, Evaluation, SFT, Dataset Management, Enterprise-level System Management, Observability and more.
  - [有计划将企业数据库作为数据源之一吗？ ](https://github.com/dataelement/bisheng/issues/500)
    - 202509: 目前可以通过助手节点数据查询功能实现 nl2sql 能力

- https://github.com/rag-web-ui/rag-web-ui /2.7kStar/apache2/202511/python/ts/提交少
  - RAG Web UI is an intelligent dialogue system based on RAG

- https://github.com/agentset-ai/agentset /1.6kStar/MIT/202512/ts
  - https://agentset.ai/
  - The open-source RAG platform: built-in citations, deep research, 22+ file formats, partitions, MCP server, and more.
  - It provides end-to-end tooling: ingestion, vector indexing, evaluation/benchmarks, chat playground, hosting, and a developer-friendly API.
  - Model agnostic: works with your choice of LLM, embeddings, and vector DB
  - Chat playground with message editing and citations
  - Built-in multi-tenancy
  - Built with TypeScript, Next.js, AI SDK, Prisma, Supabase, and Trigger.dev

- https://github.com/percent4/embedding_rerank_retrieval /202507/jupyter/inactive
  - 本项目是针对RAG中的Retrieve阶段的召回技术及算法效果所做评估实验。使用主体框架为LlamaIndex.
  - 使用Gradio实现中文Late-Chunking服务: late_chunking/late_chunking_gradio_server.py
# rag-memory
- https://github.com/jakops88-hub/Long-Term-Memory-API /202512/ts
  - A Memory Server for AI Agents. Runs on Postgres + pgvector. 
  - Now supporting 100% Local/Offline execution via Ollama.
  - [I implemented Hybrid Search (BM25 + pgvector) in Postgres to fix RAG retrieval for exact keywords. Here is the logic. : r/Rag _202512](https://www.reddit.com/r/Rag/comments/1pcvtan/i_implemented_hybrid_search_bm25_pgvector_in/)
    - I don't stick to just one framework myself, most people jump between LangChain (for quick prototyping) and **Vercel AI SDK** (for production/streaming). MemVault is built to work with both. Regarding state, yeah, MemVault handles the state layer.
    - So the queries sent back to memvault are plain nlp texts ?
      - Exactly. You just send raw text (e.g., "What is the user's budget?")
      - The API handles the embedding/vectorization internally and matches it against the stored memories. So from the agent's perspective, it's just natural language in, relevant context out.
    - Does it work well enough for other languages? Did you try that?
      - you're right, 'english' is too aggressive with stemming. I haven't tested non-English languages extensively yet, but switching to the 'simple' config is the smart move to remove stemming issues, I'll update the config to that now.

- https://github.com/mem0ai/mem0 /apache2/202409/python
  - https://mem0.ai/
  - Mem0 (pronounced as "mem-zero") enhances AI assistants and agents with an intelligent memory layer, enabling personalized AI interactions. 
  - Mem0 remembers user preferences, adapts to individual needs, and continuously improves over time, making it ideal for customer support chatbots, AI assistants, and autonomous systems.
  - Multi-Level Memory: User, Session, and AI Agent memory retention
  - Mem0 leverages a hybrid database approach to manage and retrieve long-term memories for AI agents and assistants. 
    - Each memory is associated with a unique identifier, such as a user ID or agent ID, allowing Mem0 to organize and access memories specific to an individual or context.
    - 🛢️ When a message is added to the Mem0 using add() method, the system extracts relevant facts and preferences and stores it across data stores: a vector database, a key-value database, and a graph database. 
    - This hybrid approach ensures that different types of information are stored in the most efficient manner, making subsequent searches quick and effective.
    - Mem0 performs search across these data stores, retrieving relevant information from each source

- https://github.com/getzep/zep /apache2/202409/go
  - https://docs.getzep.com/
  - a long-term memory service for AI Assistant apps. 
  - With Zep, you can provide AI assistants with the ability to recall past conversations, no matter how distant, while also reducing hallucinations, latency, and cost.
  - Zep persists and recalls chat histories, and automatically generates summaries and other artifacts from these chat histories. 
  - Zep also provides a simple, easy to use abstraction for document vector search called Document Collections. This is designed to complement Zep's core memory features, but is not designed to be a general purpose vector database.
# chunking/embedding
- https://github.com/CoreyFransen08/chunk-forge /apache2/202512/python/ts
  - A self-hosted document processing platform for converting PDFs to Markdown with semantic chunking, drag-and-drop editing, rich metadata management, and multi-format export.
  - Upload PDFs and convert them to Markdown using LlamaParse, MarkItDown, or Docling.
  - Multiple strategies (recursive, paragraph, heading, semantic, sentence, token, hierarchical) with configurable chunk sizes.
  - Frontend: React + Vite + TypeScript + Tailwind CSS + dnd-kit
  - Backend: Node.js + Express + TypeScript + Drizzle ORM
  - Parser Service: Python + FastAPI + LlamaParse/MarkItDown/Docling
  - Storage: Local filesystem
  - Built-in export presets for popular vector databases: Pinecone, Chroma

- https://github.com/sovit-123/local_file_search /MIT/202510/python
  - Scripts to replicate simple file search and RAG in a directory with embeddings and Language Models.

- https://github.com/AlwaysSany/huggingface-local-embedding /MIT/202507/python
  - A Fast API server that provides local text and multi-modal embedding using LlamaIndex Hugging Face Embedding

- https://github.com/huggingface/text-embeddings-inference /apache2/202511/rust
  - A blazing fast inference solution for text embeddings models.
  - From scratch implementation, no Vector DBs yet.
  - Steps to Chat with Any PDF in Gradio UI
# chat-docs/knowledgebase
- https://github.com/arc53/DocsGPT /17.4kStar/MIT/202511/python/ts/提交多
  - https://app.docsgpt.cloud/
  - https://docsgpt.arc53.com/
  - GPT-powered chat for documentation, chat with your documents
  - open-source AI platform for building intelligent agents and assistants. 
  - 使用langchain的代码不多
  - Wide Format Support: Reads PDF, DOCX, CSV, XLSX, EPUB, MD, RST, HTML, MDX, JSON, PPTX, and images.
  - Web & Data Integration: Ingests from URLs, sitemaps, Reddit, GitHub and web crawlers.
  - Reliable Answers: Get accurate, hallucination-free responses with source citations 
  - Flexible Deployment: Works with major LLMs (OpenAI, Google, Anthropic) and local models (Ollama, llama_cpp).
  - Pre-built Integrations: Use readily available HTML/React chat widgets, search tools, Discord/Telegram bots, and more.
  - Secure & Scalable: Run privately and securely with Kubernetes support
  - Manually updating chunks in the app UI (Feb 2025)
  - [Show HN: DocsGPT, open-source documentation assistant, fully aware of libraries | Hacker News _202302](https://news.ycombinator.com/item?id=34648266)
  - [When ingesting data, ingest using chunks. _202302](https://github.com/arc53/DocsGPT/issues/54)
    - 似乎chunking的实现存在问题

- https://github.com/PromtEngineer/localGPT /22kStar/MIT/202507/python/ts/提交少/inactive
  - LocalGPT is a fully private, on-premise Document Intelligence platform. 
  - Ask questions, summarise, and uncover insights from your files with AI—no data ever leaves your machine.
  - LocalGPT features a hybrid search engine that blends semantic similarity, keyword matching, and Late Chunking for long-context precision
  - A smart router automatically selects between RAG and direct LLM answering for every query, while contextual enrichment and sentence-level Context Pruning surface only the most relevant content
  - An independent verification pass adds an extra layer of accuracy.
  - The architecture is modular and lightweight—enable only the components you need. With a pure-Python core and minimal dependencies
  - 🏠 The RAG system is pure python and does not require any additional dependencies.
  - models via Ollama.
  - Chat History: Remembers your previous conversations (in a session).
  - API: LocalGPT has an API that you can use for building RAG Applications.
  - GPU, CPU, HPU & MPS Support
  - Multi-format Support: PDF, DOCX, TXT, Markdown, and more (Currently only PDF is supported)
  - Contextual Enrichment: Enhanced document understanding with AI-generated context, inspired by Contextual Retrieval
  - Batch Processing: Handle multiple documents simultaneously
  - Smart Routing: Automatically chooses between RAG and direct LLM responses
  - Query Decomposition: Breaks complex queries into sub-questions for better answers
  - Intuitive Web UI: Clean, responsive design
  - Real-time Chat: Streaming responses for immediate feedback
  - [Ingest larger documents (over 800MB) _202306](https://github.com/PromtEngineer/localGPT/discussions/112)
    - Im currently using a system with 16GB RAM, and 3 nvidia TESLA GPUs (16GBs each) but the localGPT only took 4-5 GB of GPU space.
    - it took some time to finish the ingesting (I kept it running for a day). But the inferences from the model takes some time. Any way to reduce that?
  - [I am running on CPU and I have 6.4GB worth of file _202309](https://github.com/PromtEngineer/localGPT/issues/448)
    - The pdf size is too large. Please try using a smaller pdf. or export relevant text out of it (reduce the pdf size) and then use it. For this much big pdf you will certainly need NVIDIA cuda cores for faster processing.

- https://github.com/Cinnamon/kotaemon /23kStar/apache2/202507/python/提交少/inactive
  - https://cinnamon.github.io/kotaemon/
  - https://huggingface.co/spaces/cin-model/kotaemon-demo
  - open-source clean & customizable RAG UI for chatting with your documents. Built with both end users and developers in mind.
  - This project serves as a functional RAG UI for both end users who want to do QA on their documents and developers who want to build their own RAG pipeline.
  - Minimalistic UI: A user-friendly interface for RAG-based QA.
  - Support for Various LLMs: Compatible with LLM API providers (OpenAI, AzureOpenAI, Cohere, etc.) and local LLMs (via `ollama` and `llama-cpp-python`).
  - Framework for RAG Pipelines: Tools to build your own RAG-based document QA pipeline.
  - Customizable UI: See your RAG pipeline in action with the provided UI, built with `Gradio`.
  - Host your own document QA (RAG) web-UI: Support multi-user login, organize your files in private/public collections, collaborate and share your favorite chat with others.
  - Hybrid RAG pipeline: Sane default RAG pipeline with hybrid (full-text & vector) retriever 
  - Advanced citations with document preview: By default the system will provide detailed citations to ensure the correctness of LLM answers.
  - Extensible: Being built on `Gradio`, you are free to customize or add any UI elements as you like.
  - require `Unstructured` if you want to process files other than .pdf, .html, .mhtml, and .xlsx documents.
    - We support both `lite` & `full` version of Docker images. With `full` version, the extra packages of `unstructured` will be installed, which can support additional file types (`.doc, .docx`, ...)
  - [Kotaemon: An open-source RAG-based tool for chatting with your documents | Hacker News _202501](https://news.ycombinator.com/item?id=42571272)
  - [Kotaemon-papers: an open-source web app to chat with your academic papers | Hacker News _202501](https://news.ycombinator.com/item?id=42603357)
    - Our team has been working on a public demo to showcase the new advanced citation features in our RAG
  - [[BUG] Unable to index document in docker ](https://github.com/Cinnamon/kotaemon/issues/539)
    - I think its PDF file size thing. Doesn't seem to happen on PDFs with <100 pages...
  - [[BUG] - Local Model LLM works, but not Embedding _202409](https://github.com/Cinnamon/kotaemon/issues/240)
    - I tried to use the base URL that works for me in AnythingLLM but it still didn't work in kotaemon. 

- https://github.com/h2oai/h2ogpt /11.9kStar/apache2/202503/python/inactive
  - http://h2o.ai/
  - [Gradio Demo](https://gpt.h2o.ai/)
  - [OpenWebUI Demo](https://gpt-docs.h2o.ai/)
  - Query and summarize your documents or just chat with local private GPT LLMs using h2oGPT
  - Private offline database of any documents (PDFs, Excel, Word, Images, Video Frames, YouTube, Audio, Code, Text, MarkDown, etc.)
  - Persistent database (Chroma, Weaviate, or in-memory FAISS) using accurate embeddings (instructor-large, all-MiniLM-L6-v2, etc.)
  - Efficient use of context using instruct-tuned LLMs (no need for LangChain's few-shot approach)
  - Parallel summarization and extraction, reaching an output of 80 tokens per second with the 13B LLaMa2 model
  - Gradio UI or CLI with streaming of all models
  - [Feature request - to add support for nomic-ai/nomic-embed-text-v1 embeddings _202402](https://github.com/h2oai/h2ogpt/issues/1418)
    - 83333 is very large. I made the max 4096. Or you can control via env `CHROMA_MAX_BATCH_SIZE`.
    - 4096 is on high end, yes can make it smaller as required. If on CPU I expect should work pretty ok, but issue is bge-m3 has 8k context so uses alot more memory despite size if chunks are large.

- https://github.com/GitHamza0206/simba /1.4kStar/apache2/202505/python/jupyter/inactive
  - https://simba.mintlify.app/
  - Portable KMS (knowledge management system) designed to integrate seamlessly with any RAG
  - Modular Architecture: Flexible integration of vector stores, embedding models, chunkers, and parsers.

- https://github.com/labring/FastGPT /25.5kStar/apache2+LOGO+nonTenant/202508/ts
  - https://fastgpt.io/
  - 一个 AI Agent 构建平台，提供开箱即用的数据处理、模型调用等能力，同时可以通过 Flow 可视化进行工作流编排，从而实现复杂的应用场景
  - 项目技术栈：NextJs + TS + ChakraUI + MongoDB + PostgreSQL (PG Vector 插件)/Milvus
  - ⚖️ License
    - 允许作为后台服务直接商用，但不允许提供 SaaS 服务

- https://github.com/QuivrHQ/quivr /38.4kStar/apache2/202506/python
  - https://core.quivr.com/
  - Opiniated RAG for integrating GenAI in your apps
  - Opiniated RAG: We created a RAG that is opinionated, fast and efficient so you can focus on your product
  - LLMs: Quivr works with any LLM, you can use it with OpenAI, Anthropic, Mistral, Gemma, etc.
  - Any File: Quivr works with any file, you can use it with PDF, TXT, Markdown, etc and even add your own parsers.
  - Customize your RAG: Quivr allows you to customize your RAG, add internet search, add tools, etc.

- https://github.com/dontizi/rlama /1.1kStar/apache2/202508/go/js
  - https://rlama.dev/
  - a powerful AI-driven question-answering tool for your documents, seamlessly integrating with your local Ollama models.
  - It enables you to create, manage, and interact with Retrieval-Augmented Generation (RAG) systems tailored to your documentation needs.
  - This project is currently on pause due to my work and university commitments that take up a lot of my time
  - [RLAMA -- A document AI question-answering tool that connects to your local Ollama models. : r/ollama _202503](https://www.reddit.com/r/ollama/comments/1j66pg3/rlama_a_document_ai_questionanswering_tool_that/)
    - I developed RLAMA to solve a straightforward but frustrating problem: how to easily query my own documents with a local LLM without using cloud services.
    - RLAMA extracts text from the documents and generates embeddings via Ollama
    - it uses Tesseract OCR to extract text from image-based PDFs or scanned documents where text can't be directly selected.

- https://github.com/morphik-org/morphik-core /3.2kStar/BSL/202508/python/ts
  - https://morphik.ai/docs
  - The most accurate document search and store for building AI apps
  - We are building the best way for developers to integrate context (however complex and nuanced) into their AI applications. 
  - Morphik provides developers the tools to ingest, search (deep and shallow), transform, and manage unstructured and multimodal documents.
  - Multimodal Search: We employ techniques such as ColPali to build search that actually understands the visual content of documents you provide. Search over images, PDFs, videos, and more

- https://github.com/jorge-armando-navarro-flores/chat_with_your_docs /MIT/202409/python
  - ChatWithYourDocs Chat App is a Python application that allows you to chat with multiple Docs formats like PDF, WEB pages and YouTube videos. 
  - This app utilizes a language model to generate accurate answers to your queries

- https://github.com/zylon-ai/private-gpt /56.5kStar/apache2/202409/python/inactive
  - a production-ready AI project that allows you to ask questions about your documents using LLM
  - Conceptually, PrivateGPT is an API that wraps a RAG pipeline and exposes its primitives.
    - The API is built using FastAPI and follows OpenAI's API scheme.
    - The RAG pipeline is based on LlamaIndex.
  - The design of PrivateGPT allows to easily extend and adapt both the API and the RAG implementation.
    - Dependency Injection, decoupling the different components and layers.
    - Usage of `LlamaIndex` abstractions such as `LLM, BaseEmbedding or VectorStore`, making it immediate to change the actual implementations of those abstractions.
    - Ready to use, providing a full implementation of the API and RAG pipeline.
  - The project provides an API offering all the primitives required to build private, context-aware AI applications. 
  - It follows and extends the OpenAI API standard, and supports both normal and streaming responses.
  - [Ollama Embedding Fails with Large PDF files _202410](https://github.com/zylon-ai/private-gpt/discussions/2097)
  - [Ingesting large number of files _202402](https://github.com/zylon-ai/private-gpt/issues/1660)
    - Its using SQLLite as its using simple (filesystem based) indexes and doc stores. Once this #1706 is pulled, those things can be moved into Postgres.

- https://github.com/thiswillbeyourgithub/WDoc /478Star/GPL/202511/python
  - https://wdoc.readthedocs.io/en/stable/
  - Summarize and query from a lot of heterogeneous documents. 
  - Any LLM provider, any filetype, advanced RAG, advanced summaries, scriptable, etc
  - Created by a medical student who needed a way to get a definitive answer from multiple sources at the same time (audio recordings, video lectures, Anki flashcards, PDFs, EPUBs, etc.). wdoc was born from frustration with existing RAG solutions for querying and summarizing.
  - It uses mostly `LangChain` and `LiteLLM` as backends.
  - High recall and specificity: it was made to find A LOT of documents using carefully designed embedding search then carefully aggregate gradually each answer using semantic batch to produce a single answer that mentions the source pointing to the exact portion of the source document.
    - Use both an expensive and cheap LLM to make recall as high as possible because we can afford fetching a lot of documents per query (via embeddings)
  - Extensible: this is both a tool and a library. It was even turned into an Open-WebUI Tool
  - Local and Private LLM
  - Web Search: Preliminary web search support using DuckDuckGo (via the ddgs library)
  - Fast: Parallel document loading, parsing, embeddings, querying, etc.
  - Roadmap
    - figure out a good way to skip merging batches that are too large before trying to merge them

- https://github.com/kqlade/dory-frontend /AGPL/202504/ts/inactive
  - [Dory – AI Knowledge Base Powered by Browser History | Hacker News _202504](https://news.ycombinator.com/item?id=43619021)
  - Dynamic Online Recall for You (DORY) helps you find anything you've seen before online using whatever you remember about it. 
  - DORY also builds a cognitive context graph to organize your work into auto-updating workflows and serve them to you in real time based on your browsing context.
  - DORY uses Neo4j to store browsing data with weighted edge relationships (semantic, behavioral, temporal) then applies stochastic block modeling for community detection and temporal-behavioral profiling.
  - It's an approach similar to how banks analyze transaction networks to detect fraud but works surprisingly well for teasing apart browser workflows.

- https://github.com/Zipstack/unstract /5.9kStar/AGPL/202511/python
  - https://unstract.com/
  - No-code LLM Platform to launch APIs and ETL Pipelines to structure unstructured documents

- https://github.com/freeCodeCamp/devdocs /37.9kStar/MPL/202511/ruby
  - https://devdocs.io/
  - DevDocs combines multiple developer documentations in a clean and organized web UI with instant search, offline support, mobile version, dark theme, keyboard shortcuts, and more
  - DevDocs was created by Thibaut Courouble and is operated by freeCodeCamp.

- https://github.com/1Panel-dev/MaxKB /15.5kStar/GPL/202504/python/ts/vue
  - https://maxkb.pro/
  - 基于大模型和 RAG 的开源知识库问答系统
  - it is a ready-to-use RAG chatbot that features robust workflow and MCP tool-use capabilities. 
  - 依赖django、langchain、pgvector、Vue
  - Flexible Orchestration: Equipped with a powerful workflow engine, function library and MCP tool-use, enabling the orchestration of AI processes to meet the needs of complex business scenarios.

- https://github.com/chaitin/PandaWiki /8.3kStar/AGPL/202512/go/ts
  - https://pandawiki.docs.baizhi.cloud/
  - AI 大模型驱动的开源知识库搭建系统，帮助你快速构建智能化的 产品文档、技术文档、FAQ、博客系统，借助大模型的力量为你提供 AI 创作、AI 问答、AI 搜索等能力。
  - 强大的富文本编辑能力：兼容 Markdown 和 HTML，支持导出为 word、pdf、markdown 等多种格式。
  - 轻松与第三方应用进行集成：支持做成网页挂件挂在其他网站上，支持做成钉钉、飞书、企业微信等聊天机器人。
  - 通过第三方来源导入内容：根据网页 URL 导入、通过网站 Sitemap 导入、通过 RSS 订阅、通过离线文件导入等。
# chat-excel
- https://github.com/huggingface/aisheets /1.5kStar/apache2/202510/python/ts
  - https://huggingface.co/spaces/aisheets/sheets
  - an open-source tool for building, enriching, and transforming datasets using AI models with no code. 
  - The tool can be deployed locally or on the Hub. 
  - By default, AI Sheets is configured to use the Huggingface Inference Providers API to run inference on the latest open-source models. However, you can also run Sheets with own custom LLMs, such as those hosted on your own infrastructure or other cloud providers. The only requirement is that your LLMs must support the OpenAI API specification.
  - This app has a minimal Expressjs server implementation

- https://github.com/weijunext/smart-excel-ai /MIT/202312/ts
  - https://smartexcel.cc/
  - Generate the Excel formulas you need in seconds using ChatGPT
  - https://twitter.com/weijunext/status/1744225202228089173
    - 这是一个足够简单（调用ChatGPT的API）却又功能俱全（有登录和支付）的demo级产品。
    - 前后端：Next.js+Tailwind+Prisma
    - 登录：Next-Auth
    - 支付：Lemon Squeezy
    - 部署：Vercel
# chat-pdf
- https://github.com/AKSarav/pdfstract /202509/python/inactive
  - web application built with FastAPI and HTML that converts PDF files to Markdown format using various conversion libraries.
  - [Built a small tool to compare PDF → Markdown libraries (for RAG / LLM workflows) : r/Rag _202507](https://www.reddit.com/r/Rag/comments/1m1j10e/built_a_small_tool_to_compare_pdf_markdown/)
  - I’ve been exploring different libraries for converting PDFs to Markdown to use in a Retrieval-Augmented Generation (RAG) setup.
  - But testing each library turned out to be quite a hassle — environment setup, dependencies, version conflicts, etc.
  - Currently, it supports: docling pymupdf4llm markitdown marker

- https://github.com/weiwill88/Local_Pdf_Chat_RAG /202510/python/inactive
  - 本地化智能问答系统 (FAISS版)
  - 混合检索：结合FAISS进行语义检索和BM25进行关键词检索，提高检索召回率和准确性
  - 结果重排序：支持交叉编码器（CrossEncoder）和LLM对检索结果进行重排序，优化相关性
  - 可选择使用本地Ollama大模型（如DeepSeek-R1系列）或云端SiliconFlow API进行推理
  - 基于Gradio构建交互式Web界面，支持多种主题界面

- https://github.com/shibing624/ChatPDF /801Star/apache2/202409/python/inactive
  - 纯原生实现RAG功能，基于本地LLM、embedding模型、reranker模型实现，支持GraphRAG，无须安装任何第三方agent库。
  - 本项目实现了轻量版的GraphRAG
  - 支持local模式的关系图检索的文档问答
  - 支持Openai API, Deepseek API, Ollama API等，可自行扩展支持更多LLM
  - 支持openai embedding、本地 text2vec embedding、huggingface embedding、sentence-transformers embedding等
  - 本项目支持多种文件格式，包括PDF、docx、markdown、txt等
  - 优化了RAG准确率: Chinese chunk切分优化，适配中英文混合文档
  - 本项目基于`gradio`开发了RAG对话页面，支持流式对话

- https://github.com/mayooear/ai-pdf-chatbot-langchain /15.8kStar/MIT/202502/ts/inactive
  - PDF chatbot agent built with LangChain & LangGraph
  - This monorepo is a customizable template example of an AI chatbot agent that "ingests" PDF documents, stores embeddings in a vector database (Supabase), and then answers user queries using OpenAI (or another LLM provider) utilising LangChain and LangGraph as orchestration frameworks.
  - This template is also an accompanying example to the book Learning LangChain (O'Reilly): Building AI and LLM applications with LangChain and LangGraph.
  - [Support for BIG PDFs?(like 500pages) ](https://github.com/mayooear/ai-pdf-chatbot-langchain/issues/409)
    - you must be mindful of the pinecone.io free tier's pod capacity, which may be exceeded
  - https://github.com/mayooear/ai-pdf-chatbot-langchain/tree/feat/chroma

- https://github.com/williamcaseylucas/quill-pdf-chat /202401/ts
  - 依赖prisma, shadcn-ui, react-pdf, AWS S3 buckets
  - https://github.com/khaledmk20/quill
    - Quill redefines PDF interaction with intelligent conversations.

- https://github.com/Byaidu/PDFMathTranslate /29.8kStar/AGPLv3/202511/python 
  - https://pdf2zh.com/
  - 基于 AI 完整保留排版的 PDF 文档全文双语翻译，支持 Google/DeepL/Ollama/OpenAI 等服务，提供 CLI/GUI/MCP/Docker/Zotero
  - Preserve formulas, charts, table of contents, and annotations
  - Support multiple languages, and diverse translation services.
  - https://github.com/PDFMathTranslate/PDFMathTranslate-next /AGPLv3
    - pdf2zh 2.0 does not currently provide an online demo

- https://github.com/bhaskatripathi/pdfGPT /7.2kStar/MIT/202306/python/代码少/inactive
  - chat with the contents of your PDF file by using GPT capabilities. 
  - When you pass a large text to Open AI, it suffers from a 4K token limit. It cannot take an entire pdf file as an input
  - The application intelligently breaks the document into smaller chunks and employs a powerful Deep Averaging Network Encoder to generate embeddings.
  - A semantic search is first performed on your pdf content and the most relevant embeddings are passed to the Open AI.
  - https://github.com/tuxxon/PDFGPT /202408/inactive
    - I rebuilt it because I thought this repository was no longer being maintained.
# chat-workspace
- https://github.com/lfnovo/open-notebook /10.2kStar/MIT/202511/python/ts/提交少
  - https://www.open-notebook.ai/
  - Open Source implementation of Notebook LM with more flexibility and features
  - AI-powered note-taking/research platform that respects your privacy

- https://github.com/rmusser01/tldw_server /1.1kStar/GPL/202511/python
  - https://tldwproject.com/
  - Too Long; Didn't Watch - API-first media analysis & research platform
  - tldw_server is an open-source research multi-tool / backend for ingesting, transcribing, analyzing, and retrieving knowledge from video, audio, documents, websites, and more.
  - It consists of a FastAPI API-first server architecture backed by SQLite or Postgres depending on user choice, with OpenAI-compatible Chat and Audio APIs, a unified RAG pipeline, knowledge management, and integrations with local or hosted LLM providers (with cost/usage tracking).
  - https://github.com/the-crypt-keeper/tldw /inactive

- https://github.com/CaviraOSS/PageLM /NonCommercial/202511/ts
  - https://pagelm.spotit.dev/
  - a community driven version of NotebookLM & a education platform that transforms study materials into interactive resources like quizzes, flashcards, notes, and podcasts.

- https://github.com/souzatharsis/podcastfy /5.6kStar/apache2/202510/python
  - Open Source Python alternative to NotebookLM's podcast feature: Transforming Multimodal Content into Captivating Multilingual Audio Conversations with GenAI
  - https://github.com/gabrielchua/open-notebooklm
    - Convert any PDF into a podcast episode

- https://github.com/run-llama/notebookllama /1.6kStar/MIT/202508/python/inactive
  - open-source, LlamaCloud-backed alternative to NotebookLM
  - [NotebookLlama: An open source version of NotebookLM | Hacker News _202410](https://news.ycombinator.com/item?id=41964980)

- https://github.com/xynehq/xyne /635Star/apache2/202511/ts
  - https://xynehq.com/
  - AI-first Search & Answer Engine for work. 
  - Open-source alternative to Glean, Gemini and MS Copilot
  - Your work information has become fragmented — across so many SaaS apps, docs, files, repos
  - Xyne connects to your applications (Google Workspace, Atlassian suite, Slack, Github, etc), securely indexes your data, and maps a graph of relationships.
  - 🐛 必须使用google账户登录才能使用?
    - 似乎不支持上传本地pdf文件
  - Model Agnostic: Plugs into any LLM of your choice. You can even point it to a local Deepseek via ollama.
  - 使用自研ai框架 jaf  结合 aisdk
  - https://github.com/xynehq/jaf
    - functional agent framework built on immutable state, type safety, and composable policies.

- https://github.com/deta/surf /2.7kStar/apache2/202511/rust/ts/svelte
  - https://deta.surf/
  - Personal AI Notebooks. Organize files & webpages and generate notes from them. 
  - built in Svelte, TypeScript and Rust, runs on MacOS, Windows & Linux, stores data locally in open formats 
  - PDF Notes: open a PDF and ask a question
  - Create an applet: use the "app generation" tool and ask for an app
  - 📡 [Optimized Embeddings CPU Usage _202510](https://github.com/deta/surf/pull/43)
    - Implemented Lazy Embeddings for Large Document Types
    - Embeddings will then be generated on-demand when documents are accessed in chat/search
    - Larger chunks (2000 → 2500): fewer embeddings to generate and store
  - [[FEATURE] Migrate to a better browser engine _202510](https://github.com/deta/surf/issues/27)
    - We understand the pros and cons of using Electron, and for the moment the pros outweigh the cons, specially for a small team.
  - [Show HN: Deta Surf – An open source and local-first AI notebook | Hacker News _202510](https://news.ycombinator.com/item?id=45680937)
    - We took inspiration from analog notebooks as a tool for thought, but wanted something for multi-media. We also see NotebookLM as the closest mainstream product to Surf.
    - 🆚 The big difference UX wise between chatbots and Surf is that Surf is built entirely on editable documents that you can mold / craft into an output (vs chat).
      - We actually had a chatbot, but our explorations showed that notes were a more effective in many cases!
    - Is this an open source equivalent to google’s NotebookLM? I can tell. How does it stack up features wise?
      - Surf is built entirely on editable WYSIWYG documents, NotebookLM's main AI is built on chat. Surf is built to be a bit more open, NotebookLM was a bit locked down for our taste.
      - An example I'd highlight is taking notes against a PDF.
      - NotebookLM will convert the PDF to simple text, and the chat responses are read only. NotebookLM also has a lot of strict walls between chat, artifacts & sources. You have to "save" responses as (read only) notes, and move notes to sources.
      - With Surf you can generate notes that deep link to specific pages in the PDF, and Surf will open those pages in the original PDF. You can remove the fluff you don't want in your notes. The intention is to be a little more open -- all notes are sources from the get go, you don't have to save or migrate anything.

- https://github.com/ItzCrazyKns/Perplexica /27.3kStar/MIT/202511/ts
  - Open source alternative to Perplexity AI
  - a privacy-focused AI answering engine that runs entirely on your own hardware. It combines knowledge from the vast internet with support for local LLMs (Ollama) and cloud providers (OpenAI, Claude, Groq), delivering accurate answers with cited sources while keeping your searches completely private
  - Web search powered by SearxNG - Support for Tavily and Exa coming soon
  - Upload documents and ask questions about them. PDFs, text files, images - Perplexica understands them all.
    - 未使用docling/libreoffice
  - Get intelligent search suggestions as you type, helping you formulate better queries.
  - Perplexica also provides an API for developers looking to integrate its powerful search engine into their own applications.
  - Perplexica runs on Next.js and handles all API requests.
  - 🐛 官方未提供外部数据源的集成，如slack/notion/gmail
    - [Add private search connectors _202508](https://github.com/ItzCrazyKns/Perplexica/issues/856)
  - [fix(uploads): Resolve the bug of large document attachment upload failure](https://github.com/ItzCrazyKns/Perplexica/pull/675)
    - Resolve the bug where large document uploads prompt an "exceeded maximum allowed batch size" error. The error message is as follows: error: Error in uploading file results: 413 input batch size 512 > maximum allowed batch size 32 (request id: 2025031909320299661815003514673)

- https://github.com/zaidmukaddam/scira /11.4kStar/AGPL/202511/ts
  - https://scira.ai/
  - Scira (Formerly MiniPerplx) is a minimalistic AI-powered search engine that helps you find information on the internet and cites it too. 
  - Powered by Vercel AI SDK
  - using multiple AI models including xAI's Grok, Anthropic's Claude, Google's Gemini, and OpenAI's GPT models
  - Search the web using Exa's API with support for multiple queries, search depths, and topics
  - Extract and analyze content from any URL using Exa AI with live crawling capabilities
    - Search Reddit content with time range filtering using Tavily API
    - X (Twitter) search: Search X posts with date ranges and specific handle filtering using xAI Live Search
  - Advanced multi-step search capability for complex queries
  - Academic search: Search for academic papers and research using Exa AI with abstracts and summaries
  - YouTube search: Find YouTube videos with detailed information, captions, and timestamps powered by Exa AI
# citation/sourcing
- https://github.com/stanford-oval/WikiChat /1.5kStar/apache2/202504/python/inactive
  - https://wikichat.genie.stanford.edu/
  - WikiChat is an improved RAG. It stops the hallucination of large language models by retrieving data from a corpus.
  - WikiChat uses Wikipedia and the following 7-stage pipeline to makes sure its responses are factual. Each numbered stage involves one or more LLM calls.

- https://github.com/AdyTech99/volo /GPL/202501/python/inactive
  - combining AI with Wikipedia knowledge via a RAG pipeline
  - It utilizes an offline database of Wikipedia created by Kiwix, ensuring fast and reliable access to information without requiring constant internet connectivity.
  - Volo uses a tiny model (Qwen2.5:3b) and gives it the knowledge of nearly 7 million Wikipedia articles, making it a more reliable source of information than giant closed-source models like OpenAI's GPT4o and Anthropic's Claude 3.5 Sonnet, which are prone to hallucinations.
  - Offline Wikipedia Database: Leverages a `.zim` file from Kiwix, offering a snapshot of Wikipedia for offline access.
  - OpenAI-Compatible REST APIs: Use Volo with interfaces like Open WebUI or your own API client.

- https://github.com/imDelivered/WikiRAG /202512/python/代码少
  - [I built an offline AI chat app that automatically pulls Wikipedia articles for factual answers - runs completely locally with Ollama : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1pd2x8u/i_built_an_offline_ai_chat_app_that_automatically/)
    - We really need a universal Kiwix API endpoint that Just Works with tools calls from whatever inference engine someone is using
# more
