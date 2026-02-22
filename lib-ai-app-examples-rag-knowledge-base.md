---
title: lib-ai-app-examples-rag-knowledge-base
tags: [ai, examples, knowledge-base, large-language-model, rag]
created: 2025-11-30T17:26:44.502Z
modified: 2025-11-30T17:27:16.720Z
---

# lib-ai-app-examples-rag-knowledge-base

# guide

- 优化提取中文文档文字的方案
  - 可参考华人团队的方案, 如 ragflow/WeKnora/LightRAG

- tips
  - 定制或优化方案时, 早晚都需要深入rag的各个环节: parse > chunk > embed > retrieval > rerank > summarize
  - 没有持久化vector embeddings的示例都是demo, 每次启动都要将大文件index一遍
  - 基于文件系统，还是基于数据库 来实现和优化rag
  - rag是很多产品都需要的基础能力之一, 可替代text-search, 可参考成功的产品或针对场景/codebase/local优化的产品

- tech-stack
  - 很多rag方案对中文的支持很差
  - 参考 cli-agent 的rag案例来实现rag后端, 大多数基于mcp-server或集成代码库
    - mcp-memory-service支持在不同cli中共享memory, 还要支持启用/禁止memory
    - migrate code indexing 的逻辑到 pdf rag
  - 结合 cli-agent + cli-rag 的方案, cli-agent的search通常通过MCP来实现
  - coding-agent is good at text and filesystem
    - store extracted text in db
    - use just-bash to interact with db

- who is NOT using #code-rag
  - claude-code
  - cline
- who is using #code-rag
  - roocode

- features: 
  - citations: 搜索rag citation的案例
  - local sources: pdf/docx
  - external sources: slack, github
  - external search: SearXNG, Tavily
  - large-file/pdf
  - ollama-embeddings
  - 中文优化
# citation/backlinks
- 权威数据源
  - arxiv
  - 类似 google-scholar, web-of-science
  - 国家统计局
  - 中国裁判文书网
  - 国家哲学社会科学(所有文献免费下载)

- 图书
  - [Project Gutenberg - Free eBooks ](https://www.gutenberg.org/)
    - focus on older works for which U.S. copyright has expired
  - 国家数字图书馆
    - [电子图书公益阅读](http://read.nlc.cn/gyyd/index)
  - 书格, 版权过期图书
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

- https://github.com/MODSetter/SurfSense /12.7kStar/apache2/202601/python/ts
  - https://www.surfsense.com/
  - Open source alternative to NotebookLM, Perplexity, and Glean.
  - Connects to search engines, Slack, Linear, Jira, ClickUp, Notion, YouTube, GitHub, Discord, and more. 
  - Save content from your own personal files (Documents, images, videos and supports 50+ file extensions) to your own personal knowledge base .
  - ⛓️ Get Cited answers just like Perplexity.
  - Works Flawlessly with Ollama local LLMs.
    - 🐛 embedding模型必须使用azure, 不支持本地模型
  - 后端: litellm, FastAPI, SQLAlchemy, pgvector, LangGraph, LangChain, Hybrid Search, Rerankers, Redis
  - 前端: next, Vercel AI SDK Kit UI Stream Protocol, Shadcn, Framer Motion, React Hook Form, tanstack/table
  - 依赖chonkie对doc进行embedding
  - ETL Service (choose one)
    - Docling (local processing, no API key required, supports PDF, Office docs, images, HTML, CSV)
    - LlamaIndex API key (enhanced parsing, supports 50+ formats)
  - 👷 xp
    - 跨workspace不能共享source-document
    - 聊天时~~只能选择全部文档或不选文档，不~~可以只选择部分文档
    - 支持根据场景配置不同llm: fast, long, reasoning
    - 🐛 聊天中的内容支持点击跳转到文档的chunk位置，而不是源文件，且中文文档的chunk经常是乱码
  - [【Feature Request】 Streaming Response for Research Agent _202505](https://github.com/MODSetter/SurfSense/issues/86)
    - 202512 已合并pr
  - https://discord.com/channels/1359368468260192417/1359416865939787837/1409642464792412220
    - I was considering installing Surfsense but it needs API keys, doesn't it? How much does it cost to use it?
    - Every service has a local alternative other than Speech to Text service. No need to put any API keys if you use everything local.
  - https://discord.com/channels/1359368468260192417/1359416891831222362/1437030441910669403  _202511
    - how does embedding work for large documents (not chunks)  if my embedding model’s context window is only 256 or 512 tokens, but the document is tens of thousands of tokens long? 
    - We generate embedding of the summary of doc.
  - [OSS Alternative to Glean : r/LocalLLaMA _202601](https://www.reddit.com/r/LocalLLaMA/comments/1qbgdu2/oss_alternative_to_glean/)
    - We use litellm to route our LLM calls and it supports nearly everything

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
  - 🇨🇳 对中文的支持较好
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
  - https://github.com/tedhappy/ragflow-admin /apache2/202512/python/ts
    - 基于ragflow二次开发的后台管理系统，可以独立运行，支持批量管理知识库、聊天、智能体、用户等，解决ragflow在后台管理上的痛点。
    - 内置管理界面在生产环境中存在一些局限：单知识库视图, 无批量操作, 任务队列隐藏
  - https://github.com/knowflow-ai/KnowFlow /AGPL/202512/python
    - https://knowflowchat.cn/
    - 基于 RAGFlow 的企业级开源知识库解决方案，专注于为企业提供真正落地的最后一公里服务
    - 持续兼容 RAGFlow 官方版本（当前适配 RAGFlow v0.20.1），同时将社区最佳实践整合进来，为企业知识管理提供更加完善的解决方案。
    - 插件化增强平台：通过独立服务方式扩展 RAGFlow 功能
    - 企业级知识管理系统：提供完整的用户权限、团队协作、数据安全保障
    - 商业版: PaddleOCR, RAG 评估系统, RBAC 完整版本, Dify 深度集成, 使用统计

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
  - [[Question]: 为什么pdf用minerU的parser后，还单独用了paddle ocr处理图片？ _202512](https://github.com/Tencent/WeKnora/issues/461)
    - 目前 minuerU 的 PDF 解析功能暂未集成 OCR 能力，若你对此功能感兴趣，欢迎提交 PR 贡献代码。

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

- https://github.com/pingcap/autoflow /2.6kStar/apache2/202601/python/inactive
  - https://tidb.ai/
  - a Graph RAG based and conversational knowledge base tool built with TiDB Serverless Vector Storage.
  - An open source GraphRAG (Knowledge Graph) built on top of TiDB Vector and LlamaIndex and DSPy.
  - UI交互类似chatgpt
  - https://x.com/9hills/status/1862522244527972625
    - RAG Demo 到 RAG Application 难度的完美表现，其实功能不算丰富（增加了 Graph RAG和 Agent RAG 的思想），
    - 代码却不得不做的非常复杂，大部分其实是应用逻辑。 P. S. 代码已经成熟到可以直接抄了，直接复刻就完了

- https://github.com/dataelement/bisheng /10.5kStar/apache2/202511/python/ts
  - http://www.bisheng.ai/
  - open LLM devops platform 
  - Powerful and comprehensive features include: GenAI workflow, RAG, Agent, Unified model management, Evaluation, SFT, Dataset Management, Enterprise-level System Management, Observability and more.
  - [有计划将企业数据库作为数据源之一吗？ ](https://github.com/dataelement/bisheng/issues/500)
    - 202509: 目前可以通过助手节点数据查询功能实现 nl2sql 能力

- https://github.com/coze-dev/coze-studio /18.8kStar/apache2/202512/go/ts
  - agent development platform with all-in-one visual tools, simplifying agent creation, debugging, and deployment like never before
  - Provides all core technologies needed for AI agent development: prompt, RAG, plugin, workflow, enabling developers to focus on creating the core value of AI.
  - https://github.com/cloudwego/eino /apache2/go
    - ultimate LLM/AI application development framework in Golang
  - https://github.com/bytedance/flowgram.ai /MIT/ts
    - providing a high-quality workflow building engine for Coze Studio's frontend workflow canvas editor
  - https://github.com/cloudwego/hertz /apache2/go
    - Go HTTP framework with high-performance and strong-extensibility for building micro-services

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

- https://github.com/timescale/pgai /5.5kStar/PGLic/202512/python
  - A suite of tools to develop RAG, semantic search, and other AI applications more easily with PostgreSQL
  - A Python library that transforms PostgreSQL into a robust, production-ready retrieval engine for RAG and Agentic applications.
  - Automatically create and synchronize vector embeddings from PostgreSQL data and S3 documents. Embeddings update automatically as data changes.
  - Enable natural language to SQL with AI. 
  - Works with any PostgreSQL database, including Timescale Cloud, Amazon RDS, Supabase and more.
  - Architecture: The system consists of an application you write, a PostgreSQL database, and stateless vectorizer workers.
    - data modifications made by the application are decoupled from the embedding process, ensuring that failures in the embedding service do not affect the core data operations.
- https://github.com/neondatabase-labs/pgrag /apache2/202510/rust
  - Postgres extensions to support end-to-end Retrieval-Augmented Generation (RAG) pipelines
  - Text extraction and conversion, using pdf-extract
  - Text chunking
  - Local embedding and reranking models
- https://github.com/postgresml/korvus /1.5kStar/MIT/202501/rust/inactive
  - a search SDK that unifies the entire RAG pipeline in a single database query. 
  - Built on top of Postgres with bindings for Python, JavaScript, Rust and C.

- https://github.com/joelhooks/pdf-brain /157Star/MIT/202601/ts
  - Local PDF & Markdown knowledge base with semantic search and AI-powered enrichment.
  - CLI
  - extract-pdf/text > ollama-enrichment(打标) > embeding > libsql-vector-hnsw-index
    - Extract - PDF text via `pdf-parse`, Markdown parsed directly
    - Enrich (optional) - LLM extracts metadata, matches taxonomy concepts
    - Chunk - Text split into ~512 token chunks with overlap
    - Embed - Each chunk embedded via Ollama (1024 dimensions)
    - Store - `libSQL` with vector index (HNSW) + FTS5
    - Search - Query embedded, compared via cosine similarity
  - PDF + Markdown - Index .pdf and .md files with the same workflow
  - Local-first - Everything runs on your machine, no API costs
  - AI enrichment - LLM extracts titles, summaries, tags, and concepts
  - Organize documents with hierarchical concepts
    - The taxonomy(生物分类学; 分类系统) is a hierarchical concept system for organizing documents
  - Vector search - Semantic search via Ollama embeddings
  - Hybrid search - Combine vector similarity with full-text search
  - MCP server - Use with Claude, Cursor, and other AI assistants
  - The database can get large due to vector index overhead. 
    - Text content	~180MB	Actual chunk text(~500k chunks)
    - FTS index	~200MB	Full-text search
    - Embeddings	~1.9GB	500k × 1024 dims × 4 bytes
    - Vector index	~48GB	HNSW neighbor graphs (~100KB/row)

- https://github.com/Hamza5/file-brain /GPL/202601/python/ts
  - https://file-brain.com/
  - open-source desktop tool that lets you search your local files using natural language.
  - Uses advanced Semantic Search -in addition to full text search- to understand the intent behind your query 
  - Extracts the content of over 1400+ file formats (PDF, Word, Excel, PowerPoint, images, archives, and more).
  - Semantic Search: It uses a multilingual embedding model to understand intent. You can search in one language and find docs in another.
  - OCR Support: Automatically extracts text from screenshots, and scanned documents.
  - Auto-Indexing: Detects changes in real-time and updates the index instantly.
  - Read-Only & Safe: File Brain only reads your files to index them. It never modifies, deletes, or alters your data in any way.
  - All indexing and AI processing happens 100% locally on your machine. 
  - Python/FastAPI/watchdog for backend and the custom filesystem crawler/monitor.
  - React + PrimeReact for the UI
  - Typesense for indexing and search.
  - Apache Tika for file content extraction.
  - 💰 PRO version is on the way with advanced capabilities:
    - Chat with Files
    - Video Search
    - Cloud & Network Drives: Connect Google Drive, Dropbox, Box, and network drives.
  - [Local file search engine that understands your documents (OCR + Semantic Search) - Open Source. : r/LocalLLaMA _202601](https://www.reddit.com/r/LocalLLaMA/comments/1qiuxko/local_file_search_engine_that_understands_your/)
  - if you are usin embeddings to search, does that mean you are maintaing a vector database of all files on disk? that would be a huge memory overhead?
    - Yes that's it. As you can see in the screenshot, the app displays the index size, which is always above 1 Go, because the embedding itself takes around 1.1 Go.

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

- https://github.com/signerlabs/klee /1.7kStar/MIT/202511/ts/inactive
  - a modern desktop application that combines AI-powered chat, knowledge base management, and note-taking capabilities.
  - It offers both Cloud Mode for seamless synchronization and Private Mode for complete offline functionality.
  - Integrated with OpenAI and local Ollama models
  - Tiptap-based collaborative editor with Markdown support
  - At its core, Klee is built on:
    - `Ollama`: For running local LLMs quickly and efficiently.
    - `LlamaIndex`: As the data framework.
  - Privacy-First: Complete offline mode with local AI and data storage
  - Optional cloud synchronization via Supabase
  - Private Mode
    - Local AI: Powered by Ollama (embedded or system-installed)
    - Local Storage: SQLite for structured data
    - Vector Search: LanceDB for semantic search (planned)
  - Cloud Mode
    - File Storage: Supabase Storage for documents and attachments
    - Data Sync: PostgreSQL database with real-time updates
    - Authentication: Google OAuth and email/password via Supabase
  - 🍴 forks
  - https://github.com/EclipseFever/Klee /202504
    - electron-build-ci: https://github.com/EclipseFever/Klee/blob/main/.github/workflows/build.yml
  - [I built and open sourced a electron app to run LLMs locally with built-in RAG knowledge base and note-taking capabilities. : r/electronjs _202503](https://www.reddit.com/r/electronjs/comments/1j43om9/i_built_and_open_sourced_a_electron_app_to_run/)
    - Would the users need to download Ollama separately or is it somehow embedded?
      - It is embedded, but if you already have ollama running, we will use your ollama instance.
    - We start with SwiftUI but switch to Electron after 3 weeks
  - [I built and open sourced a desktop app to run LLMs locally with built-in RAG knowledge base and note-taking capabilities. : r/LocalLLM _202503](https://www.reddit.com/r/LocalLLM/comments/1j4wvsu)
  - [I open-sourced Klee today, a desktop app designed to run LLMs locally with ZERO data collection. It also includes built-in RAG knowledge base and note-taking capabilities. : r/LocalLLaMA _202503](https://www.reddit.com/r/LocalLLaMA/comments/1j2j7su/i_opensourced_klee_today_a_desktop_app_designed/)
    - I see you were inspired by Slack's UI
    - Can I just point it at the folder with my existing models?
      - If you use windows, look up junctions and symbolic links: mklink /J C:\LinkDirectory D:\TargetDirectory
    - When I've used Ollama I find it's not just the file location; it requires turning the GGUF models into some hashed 'model file', which is exactly why I quit using Ollama.
    - Does this force Ollama? Or can I use llama.cpp as a backend?
      - backend and front end are in different repo, you can use llamacpp as backend
    - What key features differentiate this from those options like lmstudio/koboldai?
      - Nothing. Just yet another wrapper over ollama.
    - What does Klee use for embeddings for the RAG? does it support directory/folder upload or just individual file upload?
      - individual file, multiple files and folder
    - Would also like to know if it allows users to connect to an existing ollama instance over LAN? Would it allow me to connect to my ollama API on my network? So I can use this on my laptop and connect to my AI server in the basement? Can you put a custom IP/port? 
      - this is the most requested feature 
# rag-examples
- https://github.com/pymupdf/pymupdf4llm /1.2kStar/AGPL/202601/python/lib
  - https://pymupdf.readthedocs.io/en/latest/pymupdf4llm
  - a specialized extension of PyMuPDF designed specifically for extracting content from PDFs in a format that's optimized for LLMs
  - Converts PDFs to clean, structured Markdown format
  - Automatically identifies headers, paragraphs, tables, and images
  - Preserves document hierarchy (headers, lists, tables)
  - Maintains document layout and reading order: process multi-column pages
  - Extracts images from PDFs: save images separately or encode them inline
  - [Build a Multimodal RAG using — PyMuPDF4LLM-llamaindex-Qdrant _202411](https://ai.gopubby.com/build-a-multimodal-rag-using-pymupdf4llm-llamaindex-qdrant-e9d23a4409cc)
- https://github.com/intercepted16/pymupdf4llm-C /AGPL/202512/c/python
  - "Blazingly-fast" PDF extractor; a high quality 300 pages/s alternative to Markitdown, PyMUPDF4LLM & others.
  - a PDF extractor in C using MuPDF, inspired by pymupdf4llm. i took many of its heuristics and approach but rewrote it in C for speed, then bound it to Python and Rust so it's easy to use.
    - primarily intended for use with python bindings. but for some reason i got bored and added Rust ones too if ya want.
  - outputs JSON for every block: text, type, bounding box, font metrics, tables. you get the raw data to process however you need.
  - [I made a fast, structured PDF extractor for RAG; 300 pages a second : r/Rag _202512](https://www.reddit.com/r/Rag/comments/1pzwot0/i_made_a_fast_structured_pdf_extractor_for_rag/)
  - [I ported PyMuPDF4LLM to Go/C, and made it 100x faster (literally), while keeping comparable quality : r/Python _202602](https://www.reddit.com/r/Python/comments/1qxb67f/i_ported_pymupdf4llm_to_goc_and_made_it_100x/)
    - About 1000 pages/s on a 1600 page document, and 500 pages/s on a 149 page document

- https://github.com/danny-avila/rag_api /710Star/MIT/202508/python/librechat
  - [RAG API - Chat with files](https://www.librechat.ai/docs/features/rag_api)
  - This project integrates Langchain with FastAPI in an Asynchronous, Scalable manner, providing a framework for document indexing and retrieval, using PostgreSQL/pgvector.
  - Files are organized into embeddings by `file_id`. The primary use case is for integration with LibreChat, but this simple API can be used for any ID-based use case.
  - The main reason to use the ID approach is to work with embeddings on a file-level. This makes for targeted queries when combined with file metadata stored in a database, such as is done by LibreChat.
  - [[Enhancement] Reduce memory consumption greatly, and speed up process slighlty by processing file async and inserting to vectordb in chunks rather than all at once _202510](https://github.com/danny-avila/rag_api/issues/213)
    - Currently RAG creates embeddings for the file holding them all in memory then bulk inserts them all into the vectordb. When embedding very large files this consumes a vast amount of memory
    - This is largely solved by changing the logic such that it breaks the file up into chucks and embeds each separately, and asynchronously bulk inserting each chunk individually as the embedding process completes each chunk. 
    - pr已合并 _202512
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
  - 🛝
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
  - 依赖langchain
  - 🐛 实测查询效果很差, 很多关键词都搜不出内容 The provided context does not contain any information related to your query
    - 页面显示score都是 1.0
  - Multiple Formats: PDF, DOCX, TXT, and Markdown support
  - REST API: Django REST Framework for integrations
  - Vector Search: FAISS/ChromaDB/Pinecone vector databases
  - CLI Tools: Command-line interface for batch operations
  - Memory issues with large docs: Reduce `CHUNK_SIZE` in `.env` or process documents individually
  - 🛝
    - chroma run --host 0.0.0.0 --port 8000 --path ~/Documents/repos/libfwk/ai-llm/all-rag/doc-reader/chroma_db
    - OLLAMA_DEBUG=2 ollama serve
    - uv run --env-file .env -- python main.py start
    - 需要手动创建 创建默认的 DocumentIndex(找AI协助): DocumentIndex.objects.create(name='default'
  - 👾 prompt
    - i have run this django rag webapp fully locally by `uv run --env-file .env -- python main.py start`.
    - when i open http://localhost:8000/ , the browser shows 

- https://github.com/itanishqshelar/SmartRAG /106Star/MIT/202512/python
  - a privacy-first multimodal RAG system that lets you chat intelligently with your documents, images, and audio. 
  - Documents: PDF, DOCX, TXT, MD with intelligent chunking
  - Images: OCR + visual understanding via BLIP
  - Local AI Stack
    - Ollama (Llama 3.1 8B) for generation
    - Nomic Embed Text (768-dim) for embeddings
    - ChromaDB for vector storage
    - Complete offline operation

- https://github.com/MLNativeAI/paperjet /AGPL/202512/ts
  - https://getpaperjet.com/
  - Open-source platform to securely extract data from any document. Build custom workflows while keeping your data private.
  - Fully open-source - The web and self-hosted versions have the same feature set
  - Zero cloud dependencies - PaperJet doesn’t depend on any cloud services. Everything is self-contained in Docker
  - Built for large documents: easily ingest hundreds of pages at once
  - Use any LLM with your own keys (BYOK)
  - local providers: VLLM, LM Studio and Ollama

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

- https://github.com/Arterning/DeepParseX /MIT/202512/python
  - 强大的多模态文档解析与知识管理平台，支持 PDF、Word、Excel、PPT、图片、视频、音频 等多种文件格式的智能解析，自动提取关键信息，并构建 检索增强生成（RAG） 和 知识图谱（Knowledge Graph） 系统，实现结构化数据的智能检索与推理
  - 向量存储：ParadeDB
  - 知识图谱：NetworkX
  - 后端：FastAPI, Docker, MinIO
  - https://github.com/Arterning/DeepParseXWeb

- https://github.com/gptme/gptme-rag /MIT/202511/python/cli
  - Local RAG as a simple CLI
  - Built primarily for gptme, but can be used standalone.
  - Document indexing with ChromaDB
  - Streaming large file handling: chunking splits large documents into manageable pieces
  - File watching and auto-indexing: Real-time index updates, batch processing
  - https://github.com/gptme/gptme /4.1kStar/MIT/202602/python
    - https://gptme.org/docs/
    - Your agent in your terminal, equipped with local tools: writes code, uses the terminal, browses the web, vision
    - An unconstrained local free and open-source alternative to Claude Code, Codex, Cursor Agents, etc.
  - https://github.com/gptme/gptme-tauri /NALic/202507/rust/ts/inactive
    - Desktop app for gptme built with Tauri

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

- https://github.com/joelhooks/pdf-library /MIT/202512/ts
  - Local PDF knowledge base with vector search using PGlite + pgvector
  - i've got a crazy deep pdf library so I vibed up this @opencode (et al) tool that slurps pdfs into a pglite database with pgvector using ollama for embeddings and gives me semantic search over library of alexandria for how i think

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

- https://github.com/jayshah5696/pravah /apache2/202409/python/inactive
  - LLM powered Local Perplexity-Inspired Search Engine

- https://github.com/ragpi/ragpi /MIT/202511/python
  - https://docs.ragpi.io/
  - open-source AI assistant that answers questions using your documentation, GitHub issues, and READMEs. 
  - supports multiple providers like OpenAI, Ollama, and Deepseek, and has built-in integrations with Discord and Slack.
  - A web widget integration is also available to embed the assistant in your website.
  - After adding a source, documents will be synced automatically. You can monitor the sync process through the /tasks endpoint.

- https://github.com/NotYuSheng/OmniPDF /MIT/202510/python/inactive
  - OmniPDF is a PDF analyzer capable of translation, summarization, captioning and conversational capabilities through Retrieval-Augmented-Generation (RAG).
  - OmniPDF follows a microservices architecture with centralized orchestration:
    - pdf-processor-service: Main hub that coordinates all processing workflows
    - Processing services: Specialized services for extraction, translation, rendering, and embedding
    - Data layer: Redis (sessions), ChromaDB (vectors), MinIO (files)
    - Service mesh layer: Istio for mTLS, traffic management, and observability (prestaging/staging/production)

- https://github.com/ikantkode/pdfLLM /MIT/202509/python/inactive
  - open source, proof of concept RAG app.
  - uses PostgreSQL for session management, Qdrant for vector storage, Dgraph for graph-based indexing, and Celery for asynchronous task processing.

- https://github.com/pega2077/ai_file_manager /MIT/202601/ts/Electron
  - file manager powered by AI. It automatically classifies your imported files into the most suitable folders and tags them intelligently based on their content, making future search and retrieval easy.
  - Document Import and Management - Supports multiple document formats, automatically converts to Markdown format
  - Semantic Search - Intelligent document retrieval based on vector database
  - Supports Windows and macOS systems
  - Embedded Node.js (Express) server inside the Electron main process
  - Data Storage: SQLite (document metadata via Sequelize) + Faiss vector index (faiss-node)
  - AI Models: Pluggable LLM / embedding providers (OpenAI, Azure, OpenRouter, Bailian, Ollama, etc.)

- https://github.com/hyson666/pdf-rag-mcp-server /202505/python/js/inactive
  - This system allows you to upload, process, and query PDF documents through a modern web interface or via the MCP protocol for integration with AI tools like Cursor.
  - FastAPI Backend: Handles API requests, PDF processing, and vector storage
  - MCP Server: Exposes knowledge base to MCP-compatible clients

- https://github.com/christopherkarani/Wax /256Star/apache2/202602/swift
  - The SQLite for AI memory. Memory layer for on-device AI Agents. Replace complex RAG pipelines with a serverless, single-file memory layer.
  - One file. Full RAG. Zero infrastructure.
  - [Local-First. Sub-Millisecond RAG – 0.84ms vector search, zero cloud dependencies. Your Agents remember everything : r/LocalLLaMA _202602](https://www.reddit.com/r/LocalLLaMA/comments/1r7otbt/localfirst_submillisecond_rag_084ms_vector_search/)
    - Every RAG solution requires either cloud APIs (Pinecone/Weaviate) or running a database locally (ChromaDB/Qdrant). 
    - I wanted what SQLite gave us: import a library, open a file, query. Except for multimodal content at GPU speed on Apple Silicon.
    - So I built Wax – a pure Swift RAG engine for truly local AI apps.

- https://github.com/velle999/velle.ai /202602/js
  - Locally-run AI companion with persistent memory, swappable personalities, and system command execution. Powered by Ollama.
  - Zero external AI APIs. Zero telemetry. Zero cloud. Everything local.
  - [I built VELLE. AI - a local AI companion with memory, voice, quant engine, and a full productivity suite. No cloud, no subscriptions. Everything on your machine. : r/LocalLLM _202602](https://www.reddit.com/r/LocalLLM/comments/1r7dbwm/i_built_velleai_a_local_ai_companion_with_memory/)
    - a local AI operating system that runs on top of Ollama. It's not just another chat wrapper. It's a full personal assistant with persistent memory, two-way voice, a quantitative finance engine, and a productivity suite with todos, habits, goals, journal, and achievements.
    - Persistent memory — it actually remembers you across sessions. Your preferences, your name, your projects. All stored locally in `SQLite`.
    - Tech stack: Node.js, Express, WebSocket, SQLite, Ollama, vanilla JS. About 8,000 lines across 6 server modules. Works with any Ollama model including qwen3:8b, llama3, mistral. Ships as a Windows .exe or run from source on any OS.
# rag-fwk
- https://github.com/run-llama/semtools /1.5kStar/MIT/202511/rust/ts
  - Semantic search and document parsing tools for the command line
  - A collection of high-performance CLI tools for document processing and semantic search, built with Rust for speed and reliability.
  - parse - Parse documents (PDF, DOCX, etc.) using, by default, the `LlamaParse` API into markdown format
  - search - Local semantic keyword search using multilingual embeddings with cosine similarity matching and per-line context matching
  - ask - AI agent with search and read tools for answering questions over document collections (defaults to OpenAI, but see the config section to learn more about connecting to any OpenAI-Compatible API)
  - By default, parse uses LlamaParse as a backend. search and workspace remain local-only. ask requires an OpenAI API key.
  - Multi-format support for parsing documents (PDF, DOCX, PPTX, etc.)
  - Fast semantic search using model2vec embeddings from minishlab/potion-multilingual-128M
  - 🔀 Concurrent processing for better parsing performance
  - 📡 roadmap
    - More parsing backends (something local-only would be great!)
  - https://x.com/jerryjliu0/status/1999163155898069206
    - We made a simple cli command `ask` which lets you ask questions over any arbitrary folder in your filesystem. 
    - It's a specialized agent that does super-efficient indexing/search. Can natively help you parse all your pdfs/powerpoints/word docs.
    - You can also plug it into Claude Code to give it an efficient way to query your filesystem for context, without polluting the context window with a ton of raw file text. 

- https://github.com/phbst/tinyRAG /202409/jupyter/inactive
  - 全手写的一个RAG应用。Langchain的大部分库会很方便，但是你不一定理解其中原理，所以代码尽可能展现基本算法，主打理解RAG的原理

- https://github.com/codemilestones/TinyCodeBase /apache2/202509/python
  - 本项目是一个轻量级的代码智能系统，包含了RAG（检索增强生成）、Agent（智能代理）和评估系统的完整实现。
  - 项目从[TinyRAG](https://github.com/KMnO4-zx/TinyRAG)扩展而来，专注于代码场景的优化和实践。
  - [之前有多嫌弃大模型框架，现在用 LangGraph 就有多香 - 知乎 _202509](https://zhuanlan.zhihu.com/p/1946396924342177830)

- https://github.com/onyx-dot-app/onyx /16.7kStar/MIT+EE/202512/python/ts/偏业务app
  - https://github.com/danswer-ai/danswer /legacy
  - https://onyx.app/
  - Onyx is a feature-rich, self-hostable Chat UI that works with any LLM.
  - Onyx comes loaded with advanced features like Agents, Web Search, RAG, MCP, Deep Research, Connectors to 40+ knowledge sources, and more.
  - RAG: Best in class hybrid-search + knowledge graph for uploaded files and connectors
  - Connectors: Pull knowledge, metadata, and access information from over 40 applications.
  - 💰 enterprise: Knowledge Graph, Query History, Usage Dashboards, dev api, rbac
  - 很多issue无人处理就自动关闭了
  - 🐛 实测服务启动后首次上传文件会一直loading/processing, 此时重启服务就能正常上传了，原因待排查
    - 对中文的embedding和search有问题，关键词搜不出来: The provided document does not contain any information about your query
    - 回答能显示引用的文件，但点击引用文件的图标显示的是文本，而不是pdf原文
  - Code Interpreter: Execute code to analyze data, render graphs and create files.
  - Image Generation: Generate images based on user prompts.
  - 👾 Onyx works with all LLMs (like OpenAI, Anthropic, Gemini, etc.) and self-hosted LLMs (like Ollama, vLLM, etc.)
  - Enterprise Search: far more than simple RAG, Onyx has custom indexing and retrieval that remains performant and accurate for scales of up to tens of millions of documents.
  - [Configure Onyx - Onyx Documentation](https://docs.onyx.app/deployment/configuration/configuration)
    - Although Onyx assumes English by default, the system can be configured to support multiple languages
  - 🐛 [Enable to work with other Vector Database ](https://github.com/onyx-dot-app/onyx/issues/1165)
    - Danswer has both vector search and BM25, followed by re-ranking. Additionally, Vespa is not a database; it is more like an application server that handles both roles effectively.
    - So, I want to say that it would not be possible to migrate to something else, as it is quite a big job due to much of the logic being handled by Vespa itself. Vespa is not just a dummy storage.
  - 🐛🏠 [High memory consumption _202412](https://github.com/onyx-dot-app/onyx/issues/3427)
    - we are experiencing a similar issue, is it expected that the index container's memory usage grows proportionately to number of indexed documents? that seems like a poor design decision if that's the case - acts more like a memory leak. isn't the Vespa database meant to prevent a need for loading every document in ram?
      - Not really ... in fact being in memory is a key component of being able to perform similarity searches across documents quickly. There are probably some significant optimizations we can apply here, but generally speaking this is expected behavior.
    - A solution is to use an external vector database instead of running it within the VM. To achieve this, a new class inheriting from DocumentIndex can be implemented
    - Using an external vector database such as Qdrant Cloud, Elasticsearch, or Vespa Cloud etc. is often a better approach than running the vector index directly within the VM. The vector database is typically the component that demands the most memory.
  - 🐛 [markdown files (.md / .mdx) not supported yet ](https://github.com/onyx-dot-app/onyx/issues/5621)
  - [Feature Request: Support embedding via ollama _202511](https://github.com/onyx-dot-app/onyx/issues/6189)
    - onyx expects the embedding models to return vectors of 1536 or 3072 dimensions, respectively. I don't think that I can work around this without building my own Onyx docker image.
  - [Only getting 1 chunk per document _202402](https://github.com/onyx-dot-app/onyx/issues/1081)
    - When im querying say a pdf document, the results shown to me are based solely on 1 chunk from that document. The one with the highest semantic proximity to the user query.
  - [When I ask questions in Chinese, why are the responses always in English? _202401](https://github.com/onyx-dot-app/onyx/issues/1024)
  - [Introducing Onyx - a fully open source chat UI with RAG, web search, deep research, and MCP : r/LocalLLaMA _202510](https://www.reddit.com/r/LocalLLaMA/comments/1nw52ad/introducing_onyx_a_fully_open_source_chat_ui_with/)
    - Onyx actually is Danswer. We re-named the project ~6 months ago
    - The way I think about it is that any/every feature needed to have a great chat experience should be completely free to use.
      - The project actually started as a pure RAG/enterprise search system called Danswer, and the enterprise features were built for that world. I’m moving all features from ee to MIT that fit into the bucket above (e.g. advanced SSO).
    - You have a list of what features are included and which are pay walled?
      - Every chat/core experience feature is completely open-source! So custom assistants, RAG, web search, MCP, image gen, etc.
      - Currently, the ee features are permission syncing (e.g. for RAG, pulling in permissions from enterprise tools and applying them within the tool), a few admin dashboards, and some whitelabeling (ofc the code is MIT, so you can just edit things yourself if you want).
    - 🆚 What is the main differences between Openwebui besides being fully open source
      - One of the biggest differences is native RAG/file indexing that scales. In my experience, it's a huge pain to set up OpenWebUI with private docs. Onyx has data connectors to apps like drive, a vector db, and indexing and retrieval pipelines pre-configured for documentation search. System can comfortably do a few hundred thousand docs order of magnitude.
  - [Launch HN: Onyx (YC W24) – Open-source chat UI | Hacker News _202511](https://news.ycombinator.com/item?id=46045987)
  - 🛝 
    - minio server --address :9004 --console-address :9005  ~/Documents/repos/libfwk/ai-llm/all-rag/onyx/dataruntime/onyxs3
    - docker compose up index , docker start 
    - OLLAMA_DEBUG=2 ollama serve
    - uv run --env-file .env -- alembic upgrade head
    - uv run --env-file .env -- uvicorn model_server.main:app --reload --port 9000
    - uv run --env-file .env -- python ./scripts/dev_run_background_jobs.py
    - uv run --env-file .env -- uvicorn onyx.main:app --reload --port 8080
  - 👾 prompts
    - i have run this project fully locally without docker and nginx, only vespa is hosted using docker, all other services are running locally on my macos.
    - the backend server starts by `cd backend && uv run --env-file .env -- uvicorn onyx.main:app --reload --port 8080`.

- https://github.com/deepset-ai/haystack /23.5kStar/apache2/202512/python
  - https://haystack.deepset.ai/
  - https://docs.haystack.deepset.ai/docs
  - Haystack is an end-to-end LLM framework that allows you to build applications powered by LLMs, Transformer models, vector search and more
  - Haystack can orchestrate state-of-the-art embedding models and LLMs into pipelines to build end-to-end NLP applications 
  - 👷 xp
    - 是类似 langchain/llama_index 的框架，不是类似ragflow这样的带ui的可用产品
  - Model agnostic: Allow users the flexibility to decide what vendor or technology they want. 
  - Explicit: Make it transparent how different moving parts can “talk” to each other so it's easier to fit your tech stack and use case.
  - Haystack provides all tooling in one place: database access, file conversion, cleaning, splitting, training, eval, inference, and more
  - Extensible: Provide a uniform and easy way for the community and third parties to build their own components
  - deepset AI Platform is our fully managed, end-to-end platform to integrate LLMs with your data, which uses Haystack for the LLM pipelines architecture.
  - https://github.com/deepset-ai/haystack-cookbook /202511
    - A collection of example notebooks using Haystack
  - https://github.com/deepset-ai/haystack-demos
  - https://github.com/deepset-ai/hayhooks /apache2/python
    - Easily deploy Haystack pipelines as REST APIs and MCP Tools.
  - [Ollama: support Embedders ](https://github.com/deepset-ai/haystack-core-integrations/issues/190)
    - 202411: TextEmbedder done. Document Embedder has been merged some time ago.
  - [Investigate support for images in `ToolCallResult` _202505](https://github.com/deepset-ai/haystack/issues/9432)
    - Currently, providers that expose a tool role for messages (OpenAI, Gemini, Ollama) do not support images in the tool result.
    - Conversely, Anthropic has no tool role and requires tool results to be included in a user message, which can contain images.
    - Since multimodal support in Amazon Bedrock is mostly based on Anthropic, Bedrock supports this use case as well. 
    - Supporting this use case would require refactoring our `ToolCallResult` dataclass.
    - a simple workaround is to create a user message with the image returned by the tool.
  - [Handling rich data files such as PDF/CSV/XLSX _202511](https://github.com/deepset-ai/haystack/discussions/10034)
    - I’d like to ask how you usually handle document ingestion for large files — for example, CSVs, XLSX, or PDFs. I’m currently facing out-of-memory (OOM) issues when uploading rich data files. Our production server has 24 GB of GPU memory, but I’d like to make the process as optimized as possible.
    - Reproducing: What's the batch size for embedder? I guess you could lower that to 4-5 and see? Your splitter looks good but still do for just one file and check if it is working as expected and breaking into proper chunks. But I guess batch size is the issue
  - [Can this framework be used to Chinese full-text searches? _202307](https://github.com/deepset-ai/haystack/discussions/5471)
    - 官方源码不支持。 可以通过改源码实现。 具体在分词分句部分， 其源码使用的nltk库，没有中文。 但是可以自己修改这部分的函数。使其支持中文的分词分句规则
    - 202412: The support for Chinese is very poor. I hope v2 supports Chinese.
    - 202508: We have a new integration for processing Chinese Text with Haystack https://haystack.deepset.ai/integrations/hanlp
    - [for Chinese text processing, can we still only use regular expressions? I wonder if there is a new way now _202303](https://github.com/deepset-ai/haystack/discussions/4312)
  - [Best pipeline for similarity question search _202205](https://github.com/deepset-ai/haystack/discussions/2516)
    - Your advice saved me! Now I use `sentence-transformers/distiluse-base-multilingual-cased` for question embedding. It seems to have a nice result. 

- https://github.com/neuml/txtai /11.9kStar/apache2/202512/python
  - https://neuml.github.io/txtai
  - an all-in-one AI framework for semantic search, LLM orchestration and language model workflows
  - The key component of txtai is an embeddings database, which is a union of vector indexes (sparse and dense), graph networks and relational databases.
  - Vector search with SQL, object storage, topic modeling, graph analysis and multimodal indexing
  - Workflows to join pipelines together and aggregate business logic
  - Run local or scale out with container orchestration
  - built with Python 3.10+, Hugging Face Transformers, Sentence Transformers and FastAPI

- https://github.com/agentset-ai/agentset /1.6kStar/MIT/202512/ts
  - https://agentset.ai/
  - The open-source RAG platform: built-in citations, deep research, 22+ file formats, partitions, MCP server, and more.
  - It provides end-to-end tooling: ingestion, vector indexing, evaluation/benchmarks, chat playground, hosting, and a developer-friendly API.
  - Model agnostic: works with your choice of LLM, embeddings, and vector DB
  - Chat playground with message editing and citations
  - Built-in multi-tenancy
  - Built with TypeScript, Next.js, AI SDK, Prisma, Supabase, and Trigger.dev

- https://github.com/incidentfox/OpenRag /MIT/202602/python
  - Multi-strategy RAG system achieving 74% Recall@10 on MultiHop-RAG.
  - Combines RAPTOR hierarchical retrieval, knowledge graphs, HyDE, BM25, and Cohere neural reranking.
  - Full RAG Implementation (ultimate_rag/) - RAPTOR + Graph + HyDE + BM25 + Neural Reranking
  - This system uses Cohere's rerank API for neural reranking, which provides the best benchmark results (+9.3% improvement).
    - For privacy-sensitive use cases, consider these alternatives
    - Local cross-encoder: The system includes `CrossEncoderReranker` using `BAAI/bge-reranker-base` (runs locally, no external API)
  - [We open-sourced our code that outperforms RAPTOR on multi-hop retrieval : r/Rag _202602](https://www.reddit.com/r/Rag/comments/1qv17hv/we_opensourced_our_code_that_outperforms_raptor/)

- https://github.com/wzdavid/ThinkRAG /MIT/202512/python/inactive
  - https://bluedigit.ai/
  - 大模型检索增强生成系统，可以轻松部署在笔记本电脑上，实现本地知识库智能问答
  - 基于 LlamaIndex 和 Streamlit 构建，针对国内用户在模型选择、文本处理等诸多领域进行了优化
  - 开发模式支持本地文件存储，无需安装任何数据库
  - 为国内用户做了大量定制和优化：
    - 使用 Spacy 文本分割器，更好地处理中文字符
    - 采用中文标题增强功能
    - 使用中文提示词模板进行问答和细化过程
    - 默认支持国内大模型厂商，如DeepSeek，Moonshot和Zhipu等
    - 使用双语嵌入模型，如 BAAI的bge-large-zh-v1.5

- https://github.com/Bessouat40/RAGLight /612Star/MIT/202512/python
  - a lightweight and modular Python library for implementing RAG
  - provides modular components to easily integrate various LLMs, embeddings, and vector stores
  - supports: Ollama Google LMStudio vLLM OpenAI API Mistral API

- https://github.com/HKUDS/RAG-Anything /10.7kStar/MIT/202511/python
  - All-in-One Multimodal Document Processing RAG system built on LightRAG.
  - As a unified solution, RAG-Anything eliminates the need for multiple specialized tools. It provides seamless processing and querying across all content modalities within a single integrated framework. 
  - [[Question]: 我使用中文数据构建了RAG，但是为什么检索出来的内容是英文的？ _202510](https://github.com/HKUDS/RAG-Anything/issues/136)
    - .env里好像有个语言设置，默认是英文，可以看看和这个是否有关
  - [[Question]: 目前是否支持长表格的导入 _202509](https://github.com/HKUDS/RAG-Anything/issues/100)
  - https://github.com/HKUDS/LightRAG /20.1kStar/MIT/202508/python
    - Simple and Fast Retrieval-Augmented Generation
    - [2025.06.16]🎯 Our team has released RAG-Anything an All-in-One Multimodal RAG System for seamless text, image, table, and equation processing.
  - https://github.com/BukeLy/rag-api
    - Multi-tenant RAG API powered by LightRAG/RAG-Anything. Auto-selects best parser (DeepSeek-OCR/MinerU/Docling) via complexity scoring
- https://github.com/xerrors/Yuxi-Know /2.6kStar/MIT/202512/python/vue
  - https://xerrors.github.io/Yuxi-Know/
  - 功能强大的智能体平台，融合了 RAG 知识库与知识图谱技术，基于 LangGraph v1 + Vue.js + FastAPI + LightRAG 架构构建
  - 集成主流大模型、LightRAG、MinerU、PP-Structure、Neo4j 、联网检索、工具调用。

- https://github.com/SciPhi-AI/R2R /7.5kStar/MIT/202511/python
  - an advanced AI retrieval system supporting RAG
  - Built around a RESTful API, R2R offers multimodal content ingestion, hybrid search, knowledge graphs, and comprehensive document management.
  - Multimodal Ingestion: Parse .txt, .pdf, .json, .png, .mp3, and more
  - Hybrid Search: Semantic + keyword search with reciprocal rank fusion
  - User & Access Management: Complete authentication & collection system

- https://github.com/getzep/graphiti /20.6kStar/apache2/202511/python
  - https://help.getzep.com/graphiti
  - a framework for building and querying temporally-aware knowledge graphs
  - Unlike traditional RAG, Graphiti continuously integrates user interactions, structured and unstructured enterprise data, and external information into a coherent, queryable graph. 
  - The framework supports incremental data updates, efficient retrieval, and precise historical queries without requiring complete graph recomputation
  - Graphiti powers the core of Zep, a turn-key context engineering platform for AI Agents.
  - Traditional RAG approaches often rely on batch processing and static data summarization, making them inefficient for frequently changing data. 
  - Real-Time Incremental Updates: Immediate integration of new data episodes without batch recomputation.
  - Scalability: Efficiently manages large datasets with parallel processing, suitable for enterprise environments.

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

- https://github.com/OoriData/OgbujiPT /apache2/202512/python
  - Client-side toolkit for using large language models, including where self-hosted
  - It provides a unified API for storing, retrieving, and managing semantic knowledge across multiple backends, with support for dense vector search, sparse retrieval, hybrid search, and more.
  - Storage backends: in-memory, pgvector, qdrant
  - You can use the OpenAI cloud LLM API and APIs which conform to this, including Anthropic's, local LM Studio, Ollama, etc.

- https://github.com/yichuan-w/LEANN /9.9kStar/MIT/202602/python
  - an open-source vector database, compresses RAG indexes by an impressive 97% using graph-based recomputation and on-demand embedding calculation.
  - LEANN achieves this through graph-based selective recomputation with high-degree preserving pruning, computing embeddings on-demand instead of storing them all

- https://github.com/rag-web-ui/rag-web-ui /2.7kStar/apache2/202511/python/ts/提交少/inactive
  - RAG Web UI is an intelligent dialogue system based on RAG
  - FastAPI, MySQL + ChromaDB, MinIO, Langchain
  - Nextjs, Vercel AI SDK

- https://github.com/percent4/embedding_rerank_retrieval /202507/jupyter/inactive
  - 本项目是针对RAG中的Retrieve阶段的召回技术及算法效果所做评估实验。使用主体框架为LlamaIndex.
  - 使用Gradio实现中文Late-Chunking服务: late_chunking/late_chunking_gradio_server.py

- https://github.com/devflowinc/trieve /2.6kStar/MIT/202510/rust/js/inactive
  - https://trieve.ai/
  - All-in-one platform for search, recommendations, RAG, and analytics offered via API

- https://github.com/autollama/autollama /26Star/MIT/202509/js
  - https://autollama.io/
  - Anthropic's Contextual Retrieval implementation with visual chunk comparison. Preview context enrichment before/after embedding.
  - For too long, RAG has been about finding chunks, not understanding documents. AutoLlama changes that. 
  - Built on Anthropic's breakthrough contextual retrieval methodology, it's the first JavaScript-first RAG framework that actually comprehends your documents the way humans do.

- https://github.com/RapidFireAI/rapidfireai /apache2/python/ts
  - https://rapidfire.ai/
  - RapidFire AI is a new experiment execution framework that transforms your AI customization experimentation from slow, sequential processes into rapid, intelligent workflows with hyperparallelized execution, dynamic real-time experiment control, and automatic system optimization.

- https://github.com/OpenBMB/UltraRAG /2.6kStar/apache2/202601/python/js
  - https://ultrarag.openbmb.cn/
  - the first lightweight RAG development framework based on the Model Context Protocol (MCP) architecture design

- https://github.com/libragen/libragen /MIT/202601/ts
  - https://libragen.dev/
  - Create private, local RAG libraries that work offline—no API keys, no cloud services. Share them as single files your whole team can use.
  - It’s a CLI tool and MCP server for creating discrete, versioned “libraries” of RAG-able content.
  - Under the hood, it uses an embedding model locally. It chunks your content and stores embeddings in SQLite. The search functionality uses vector + keyword search + a re-ranking model.
  - You can also point it at any GitHub repo and it will create a RAG DB out of it.
  - You can also use the MCP server to create and query the libraries.
# graph-knowledge

## graph-examples

- https://github.com/liujuntao123/DeepRead /MIT/202509/ts
  - https://deepread.aizhi.site/
  - AI 驱动的智能书籍知识图谱, 将书籍转化为相互关联的知识网络
  - 基于大语言模型的全书内容分析
  - 类似 deepwiki/codewiki 的书籍版本

- https://github.com/abhigyanpatwari/GitNexus /202601/ts
    - https://gitnexus.vercel.app/
    - GitNexus is a client-side knowledge graph creator that runs entirely in your browser. 
    - Drop in a GitHub repo or ZIP file, and get an interactive knowledge graph wit a built in Graph RAG Agent. Perfect for code exploration
    - Zero-Server, Graph-Based Code Intelligence Engine Works fully in-browser through WebAssembly. (DB engine, Embeddings model, AST parsing, all happens inside browser)
# rag-memory/context
- https://github.com/zilliztech/memsearch /109Star/MIT/202602/python
  - https://zilliztech.github.io/memsearch/
  - A Markdown-first memory system, a standalone library for any AI agent. Inspired by OpenClaw.
  - basically proper RAG over markdown files with:
    - Hybrid search (vector + BM25, weighted fusion)
    - File watching + auto-indexing
    - Framework agnostic
  - Write memories as markdown, search them semantically. Inspired by OpenClaw's markdown-first memory architecture. Pluggable into any agent framework.
  - Ready-made Claude Code plugin — a drop-in example of agent memory built on memsearch
  - Markdown is the source of truth — the vector store is just a derived index, rebuildable anytime.
  - [RAG for AI memory: why is everyone indexing databases instead of markdown files? : r/Rag _202602](https://www.reddit.com/r/Rag/comments/1r2hlzd/rag_for_ai_memory_why_is_everyone_indexing/)

- https://github.com/volcengine/OpenViking /839Star/apache2/202602/python/cpp
  - https://openviking.ai/
  - 专为 AI Agent 设计的上下文数据库
  - OpenViking 摒弃了传统 RAG 的碎片化向量存储模式，创新性地采用 “文件系统范式”，将 Agent 所需的记忆、资源和技能进行统一的结构化组织。
  - 像管理本地文件一样构建 Agent 的大脑
  - 文件系统管理范式 → 解决碎片化问题：基于文件系统范式，将记忆、资源、技能进行统一上下文管理
  - 分层上下文按需加载 → 降低 Token 消耗：L0/L1/L2 三层结构，按需加载，大幅节省成本
  - 目录递归检索 → 提升检索效果：支持原生文件系统检索方式，融合目录定位与语义搜索，实现递归式精准上下文获取

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
- https://github.com/MichalZnalezniak/Chunking-Vis /MIT/202601/python
  - https://chunkingvis-production.up.railway.app/
  - A tool for visualizing different text-chunking methods.
  - Chunking Methods
  - [Built a tool for visualizing text chunking strategies : r/Rag](https://www.reddit.com/r/Rag/comments/1qnplpb/built_a_tool_for_visualizing_text_chunking/)
    - https://chunkviz.up.railway.app/

- https://github.com/chunkhound/chunkhound /974Star/MIT/202602/python
  - https://chunkhound.github.io/
  - Deep Research for Code & Files
  - Transform your codebase into a searchable knowledge base for AI assistants using semantic search via cAST algorithm and regex search. 
  - MCP integration - Works with Claude, VS Code, Cursor, Windsurf, Zed, etc
  - cAST Algorithm - Research-backed semantic code chunking
  - Multi-Hop Semantic Search - Discovers interconnected code relationships beyond direct matches
  - Semantic search - Natural language queries like "find authentication code"
  - Regex search - Pattern matching without API keys
  - Local-first - Your code stays on your machine
  - 22 languages with structured parsing, via Tree-sitter
  - Real-time indexing - Automatic file watching, smart diffs, seamless branch switching
  - pr已合并 [refactor: Extract BaseCLIProvider and improve OpenCode integration _202512](https://github.com/chunkhound/chunkhound/pull/122)

- https://github.com/CoreyFransen08/chunk-forge /apache2/202512/python/ts
  - A self-hosted document processing platform for converting PDFs to Markdown with semantic chunking, drag-and-drop editing, rich metadata management, and multi-format export.
  - Upload PDFs and convert them to Markdown using LlamaParse, MarkItDown, or Docling.
  - Multiple strategies (recursive, paragraph, heading, semantic, sentence, token, hierarchical) with configurable chunk sizes.
  - Frontend: React + Vite + TypeScript + Tailwind CSS + dnd-kit
  - Backend: Node.js + Express + TypeScript + Drizzle ORM
  - Parser Service: Python + FastAPI + LlamaParse/MarkItDown/Docling
  - Storage: Local filesystem
  - Built-in export presets for popular vector databases: Pinecone, Chroma

- https://github.com/zirkelc/chunkdown /MIT/202512/ts
  - a tree-based markdown text splitter to create semantically meaningful chunks for RAG applications.
  - Unlike traditional splitters that use simple character or regex-based methods, this library leverages markdown's hierarchical structure for optimal chunking. 
  - Chunkdown is built around a few core ideas that guide its design:
    - Markdown as Hierarchical Tree
  - https://x.com/zirkelc_/status/2000847712884068755
    - Chunkdown now supports split rules for fenced code blocks and inline code
  - https://x.com/zirkelc_/status/1992520261325771153
    - Chunkdown now compacts markdown tables thanks to a one-line PR
    - Markdown tables can be pretty formatted with additional dashes and spaces to align the columns vertically. This makes them easier for humans to read, but wastes tokens and embedding space on useless characters

- https://github.com/speedyk-005/chunklet-py /MIT/202512/python
  - https://speedyk-005.github.io/chunklet-py/
  - One library to split them all: Sentence, Code, Docs. Chunk smarter, not harder
  - Supports over 50 natural languages for text and document chunking 
  - formats including .pdf, .docx, .epub, .txt, .tex, .html, .hml, .md, .rst, .rtf, .odt, .csv, and .xlsx.
  - Triple Interface: CLI, Library & Web
  - [[Release] Chunklet-py v2.1.0: Interactive Web Visualizer & Expanded File Support! : r/Rag](https://www.reddit.com/r/Rag/comments/1prjdjp/release_chunkletpy_v210_interactive_web/)
    - Our `CodeChunker` is rule-based and language-agnostic, using clever patterns to identify functions, classes, and logical blocks without the overhead of heavy dependencies like tree-sitter.
  - ["Docling vs Chunklet-py: Which Document Processing Library Should You Use?" : r/Rag _202511](https://www.reddit.com/r/Rag/comments/1p42qik/docling_vs_chunkletpy_which_document_processing/)
    - Key Difference: Docling focuses on document understanding with complex chunking options, while Chunklet-py focuses on accessible, intelligent chunking with superior metadata and universal language support.

- https://github.com/supermemoryai/code-chunk /MIT/202512/ts
  - AST-aware code chunking for semantic search and RAG pipelines.
  - Uses `tree-sitter` to split source code at semantic boundaries (functions, classes, methods) rather than arbitrary character limits. 
  - Each chunk includes rich context: scope chain, imports, siblings, and entity signatures.
  - Batch processing: Process entire codebases with controlled concurrency
  - Streaming: Process large files incrementally
  - [Building code-chunk: AST Aware Code Chunking _202512](https://supermemory.ai/blog/building-code-chunk-ast-aware-code-chunking/)

- https://github.com/xuzeyu91/AntSK-FileChunk /202512/python
  - 一个基于语义理解的智能文本切片服务，专门用于处理PDF和Word文档，能够根据段落语义进行合理切片，避免传统基于Token数量切分导致的语义割裂问题。
  - 支持PDF、Word（.docx/.doc）、纯文本等多种文档格式

- https://github.com/sovit-123/local_file_search /MIT/202510/python
  - Scripts to replicate simple file search and RAG in a directory with embeddings and Language Models.

- https://github.com/AlwaysSany/huggingface-local-embedding /MIT/202507/python
  - A Fast API server that provides local text and multi-modal embedding using LlamaIndex Hugging Face Embedding

- https://github.com/huggingface/text-embeddings-inference /apache2/202511/rust
  - A blazing fast inference solution for text embeddings models.
  - From scratch implementation, no Vector DBs yet.
  - Steps to Chat with Any PDF in Gradio UI

- https://github.com/mburaksayici/smallevals /202512/python
  - A lightweight evaluation framework powered by tiny 0.6B models — runs 100% locally on CPU/GPU/MPS, attach any vector DB connection and run, fast and free.
  - Evaluation tools requiring LLM-as-a-judge or external, that costs/doesn't scale easily. 

- https://github.com/kannandreams/latentlens /202512/python
  - https://latentlens.streamlit.app/
  - a powerful visual debugger and educational tool for exploring vector embeddings. 
  - It helps you peek inside the "black box" of semantic search by projecting high-dimensional vectors into an interactive 3D map.
  - 3D Projection: PCA → UMAP reduction into an interactive 3D scatter plot.
  - Multiple Embedders: Support for Demo (synthetic), local MiniLM (sentence-transformers), and OpenAI (text-embedding-3-small).
  - Flexible Storage: Ships with an in-memory/local `ChromaDB` adapter.
  - matplotlib (for heatmap rendering)

- https://github.com/PotentiallyARobot/EmbeddingAdapters /CC-NC/202512/python
  - Universal embedding-space translation library. 
  - Plug-and-play adapters that map one embedding model’s vector space into another — locally or via API — enabling cross-model retrieval, routing, and interoperability.
  - a lightweight Python library and model collection that lets you map embeddings from one model’s space into another’s.
  - [I built a Python library that translates embeddings from MiniLM to OpenAI _202512](https://www.reddit.com/r/Rag/comments/1py8l8f/i_built_a_python_library_that_translates/)

- https://github.com/vectordbz/vectordbz /NonOpen
  - http://vectordbz.com/
  - modern desktop application for exploring, managing, and analyzing vector databases
  - Multiple Database Support — Connect to Qdrant, Weaviate, Milvus, ChromaDB, Pinecone, pgvector, and Elasticsearch

- https://github.com/Mintplex-Labs/vector-admin /2.2kStar/MIT/202401/ts/inactive
  - https://vectoradmin.com/
  - The universal tool suite for vector database management. Manage Pinecone, Chroma, Qdrant, Weaviate and more vector databases with ease
  - This repo and project is no longer actively maintained by Mintplex Labs. We hope one day to grow the team large enough to restart dedicated support and updates for this project. our main focus has moved to AnythingLLM.
# search 🔍
- https://github.com/AL-MARID/Lorph /MIT/202602/ts
  - AI chat application designed to run locally on your device, offering a seamless interactive experience with powerful large language models (LLMs) via Ollama.
  - What truly sets Lorph apart is the advanced and excellent search system I've developed. It's not just about conversation; it extends to highly dynamic and effective web search capabilities, enriching AI responses with up-to-date and relevant information.
  - Dynamic Web Search Integration: Leverages real-time web search to augment AI responses with current and relevant information.
  - Supports text extraction from images (OCR), PDF documents, Microsoft Word (.docx), and Excel (.xlsx) files, enhancing contextual understanding for AI responses.
  - [Lorph: A Local AI Chat App with Advanced Web Search via Ollama : r/ollama _202602](https://www.reddit.com/r/ollama/comments/1qy77nm/lorph_a_local_ai_chat_app_with_advanced_web/)

- https://github.com/tobi/qmd /5.1kStar/MIT/202602/python/ts
  - mini cli search engine for your docs, knowledge bases, meeting notes, whatever. 
  - Tracking current sota approaches while being all local
  - use it on the command line, it also exposes an MCP (Model Context Protocol) server for tighter integration.
# mobile-devices
- https://github.com/shubham0204/OnDevice-RAG-Android /aapche2/202601/kotlin
  - A simple Android app that allows the user to add a PDF/DOCX document and ask natural-language questions whose answers are generated by the means of an LLM (remote or on-device)
  - A custom RAG pipeline for multi-document QA from PDF/DOCX documents, in Android
# chat-docs/knowledgebase
- https://github.com/hyperbrowserai/hyperbooklm /MIT/202512/ts/仅云端模型
  - https://hyperbrowser.ai/
  - powerful research assistant built with Next.js 15, React 19, and Hyperbrowser. 
  - It allows users to aggregate diverse sources (Web URLs, PDFs) and gain deep insights through interactive AI tools.
  - Web Scraping: Hyperbrowser SDK
  - React Flow (Mindmaps)
  - https://x.com/hyperbrowser/status/2000655095764267050
    - Ask questions across all your sources

- https://github.com/MrSibe/KnowNote /54Star/GPL/202601/ts/Electron
  - 一个本地优先的知识笔记工具，灵感来自 Google NotebookLM。它将你的 PDF、Word 文档、PowerPoint 和网页转化为可提问、可引用、可追溯的个人知识库。
  - 自定义 LLM - 支持 OpenAI、Claude、本地模型等多种 AI 服务
  - 使用 SQLite 本地数据库，快速可靠
  - sqlite-vec · Drizzle ORM · pdfjs-dist · mammoth · officeparser · Tiptap
  - [I built a local-first NotebookLM-style app without Docker (Electron-based) : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1ptj78l/i_built_a_localfirst_notebooklmstyle_app_without/)
    - One of the main reasons I started KnowNote was that many similar projects (including open-notebook) rely on Docker-based setups, which can be a bit intimidating for non-technical users.
    - My goal here was to explore a lighter, desktop-first approach using Electron, so people can just download and run it without dealing with containers.

- https://github.com/Panda-995/wechat-editor /apache2/202601/ts
  - 专为微信公众号创作者打造的极致像素风 Markdown 编辑器，内置 Google Gemini AI 强大助手
  - [告别排版地狱！不只是NAS，更是写作助手、排版大师和美学设计师 ](https://linux.do/t/topic/1506017)
    - 上个月，熊猫开源了开发的妙笔生花项目，主要是利用AI来检测文章中的错别字以及语句问题，这也是熊猫之前被粉丝拷打很多的问题。但只有检测的功能就导致我很多时候写完并不愿意用它单独去跑一遍
    - 原因还是在于它的功能太少了，于是在妙笔生花的基础上，最近熊猫又折腾了一个新的开源项目-微信公众号编辑器
    - 直接做了个在线的编辑器，首页能看到最左侧是文章列表，右边则是编辑区和预览区，编辑区支持Markdown语法，同时编辑区和预览区支持同步滚动
  - https://github.com/Panda-995/ai-writing-assistant /202512/ts
    - 妙笔生花是一款基于 Google Gemini 和 OpenAI 技术的现代化智能写作辅助工具
    - 智能纠错与润色：自动检测错别字、语法错误、标点误用，并提供专业的润色建议。
    - 逻辑结构可视化：利用 D3.js 生成文章逻辑树状图，直观展示核心论点与支撑论据的层次结构。
    - 多模型支持：默认支持 Google Gemini (Flash/Pro)，兼容 OpenAI (GPT-4o) 及其他兼容接口。
    - AI SDK: @google/genai (Gemini 2.0/1.5)
    - Markdown 渲染: react-markdown

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
  - Kotaemon has 3 GraphRAG options (NanoGraphRAG, LightRAG, and MS's hosted GraphRAG)
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

- https://github.com/khoj-ai/khoj /31.6kStar/AGPLv3/202511/python/ts
  - https://khoj.dev/
  - Khoj is an application that creates always-available, personal AI agents for you to extend your capabilities
  - Your AI agents have access to the internet, allowing you to incorporate realtime information.
  - Khoj is accessible on Desktop, Emacs, Obsidian, Web and Whatsapp.
  - Khoj is open-source, self-hostable. Always.
  - 支持私有化部署、本地模型、与 Obsidian 无缝整合
  - 支持 github、pdf/markdown、notion 等内容源

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

- https://github.com/QuivrHQ/quivr /38.7kStar/apache2/202506/python/inactive
  - https://core.quivr.com/
  - Opiniated RAG for integrating GenAI in your apps
  - Opiniated RAG: We created a RAG that is opinionated, fast and efficient so you can focus on your product
  - LLMs: Quivr works with any LLM, you can use it with OpenAI, Anthropic, Mistral, Gemma, etc.
  - Any File: Quivr works with any file, you can use it with PDF, TXT, Markdown, etc and even add your own parsers.
  - Customize your RAG: Quivr allows you to customize your RAG, add internet search, add tools, etc.

- https://github.com/dontizi/rlama /1.1kStar/apache2/202505/go/js/inactive
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

- https://github.com/OpenDCAI/Paper2Any /1.2kStar/apache2/202601/python/ts
  - http://dcai-paper2any.nas.cpolar.cn/
  - From paper PDFs / images / text to editable scientific figures, slide decks, video scripts, academic posters, and other multimodal content in one click.
  - Paper2Figure - Editable Scientific Figures: One-click generation of model architecture diagrams, technical roadmaps (PPT + SVG), and experimental plots. Supports multiple input sources and outputs editable PPTX.
  - Paper2PPT - Editable Slide Decks: Generate PPTs in arbitrary styles, support ultra-long document processing, and include built-in table extraction and chart parsing.
  - PDF2PPT - Layout-Preserving Conversion: Intelligent cutout and layout analysis to accurately convert PDFs into editable PPTX.
  - MinerU (PDF Parsing)
  - OCR (PaddleOCR)
  - SAM (Segment Anything Model)
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
# chat-workspace/notebooklm
- https://github.com/lfnovo/open-notebook /13kStar/MIT/202512/python/ts/提交少
  - https://www.open-notebook.ai/
  - Open Source implementation of Notebook LM with more flexibility and features
  - A private, multi-model, 100% local, full-featured alternative to Notebook LM
  - Choose your AI models - Support for 16+ providers including OpenAI, Anthropic, Ollama, LM Studio, and more
  - 依赖SurrealDB、fatspi、nextjs
  - Organize multi-modal content - PDFs, videos, audio, web pages, and more
  - 🐛: no citation, no connector
  - [Our target for starting strong in 2026 _202601](https://github.com/lfnovo/open-notebook/discussions/375)
    - Here's what's on our radar:
    - RAG & Context Mechanism: We inject full source content into conversations. This overloads models and produces subpar responses
    - SurrealDB: Transaction conflicts under load, production readiness questions.Our decision: We're staying with SurrealDB. It gives us document storage, graph relationships, vector embeddings, and background jobs — all in one. The alternative (Postgres + Redis + Celery + vector DB) doesn't align with "easy self-hosting."
  - https://github.com/lfnovo/esperanto
    - Python library that provides a unified interface for interacting with various Large Language Model (LLM) providers.
    - All providers communicate directly via HTTP APIs using httpx - no bulky vendor SDKs required

- https://github.com/eclaire-labs/eclaire /728Star/MIT/202512/ts
  - https://eclaire.co/
  - Local-first, open-source AI assistant for your data. Unify tasks, notes, docs, photos, and bookmarks. 
  - Private by default: By default all AI models run locally, all data is stored locally.
  - Layered architecture: frontend, backend, and workers are separate services. Run only the backend for API-only/data-processing use cases
    - Backend for AI assistant (eg. Qwen3 model), 
    - Workers for image and document processing (eg. Gemma3 multi-modal). 
    - Docling for processing some of the document formats.
  - Model backends: works with llama.cpp, vLLM, mlx-lm/mlx-vlm, LM Studio, Ollama, and more via the standard OpenAI-compatible API.
  - Storage: all assets (uploaded or generated) live in Postgres or file/object storage.
  - Documents: PDF, DOC/DOCX, PPT/PPTX, XLS/XLSX, ODT/ODP/ODS, MD, TXT, RTF, Pages, Numbers, Keynote, HTML, CSV, and more.
  - [AI Model Configuration](https://github.com/eclaire-labs/eclaire/blob/main/docs/ai-models.md)
    - 依赖外部backend来期待llm api

- https://github.com/frumu-ai/tandem /MIT/202602/rust/ts/python/Tauri
  - A local-first, privacy-focused AI workspace. Your AI coworker that runs entirely on your machine.
  - Unlike cloud-based AI tools, Tandem runs on your machine. Your code, documents, and API keys never touch our servers
  - Use any LLM provider - Anthropic, OpenAI, or run models locally with Ollama
  - Cross-Platform: built on Tauri 
  - [I built a fully local, open-source AI workspace using Rust, Tauri, and sqlite-vec (No Python backend) : r/LocalLLaMA _202602](https://www.reddit.com/r/LocalLLaMA/comments/1qz6zi3/i_built_a_fully_local_opensource_ai_workspace/)
    - Vector Store: Instead of running a separate Docker container for Qdrant/Chroma, I'm using sqlite-vec. This allows me to store embeddings directly in the same SQLite file as the chat history. It simplifies the distribution massively—users just download one binary.
    - I built it primarily to drive local Llama models. It connects seamlessly to Ollama

- https://github.com/rmusser01/tldw_server /1.1kStar/GPL/202511/python
  - https://tldwproject.com/
  - Too Long; Didn't Watch - API-first media analysis & research platform
  - tldw_server is an open-source research multi-tool / backend for ingesting, transcribing, analyzing, and retrieving knowledge from video, audio, documents, websites, and more.
  - It consists of a FastAPI API-first server architecture backed by SQLite or Postgres depending on user choice, with OpenAI-compatible Chat and Audio APIs, a unified RAG pipeline, knowledge management, and integrations with local or hosted LLM providers (with cost/usage tracking).
  - https://github.com/the-crypt-keeper/tldw /inactive

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

- https://github.com/deta/surf /2.7kStar/apache2/202511/rust/ts/svelte/inactive
  - https://deta.surf/
  - Personal AI Notebooks. Organize files & webpages and generate notes from them. 
  - an AI notebook that brings all your files and the web directly into your stream of thought.
  - built in Svelte, TypeScript and Rust, runs on MacOS, Windows & Linux, stores data locally in open formats 
  - PDF Notes: open a PDF and ask a question
  - Create an applet: use the "app generation" tool and ask for an app
  - 整体体验是 Notion + AI
  - 📡 [Optimized Embeddings CPU Usage _202510](https://github.com/deta/surf/pull/43)
    - Implemented Lazy Embeddings for Large Document Types
    - Embeddings will then be generated on-demand when documents are accessed in chat/search
    - Larger chunks (2000 → 2500): fewer embeddings to generate and store
  - [[FEATURE] Migrate to a better browser engine _202510](https://github.com/deta/surf/issues/27)
    - We understand the pros and cons of using Electron, and for the moment the pros outweigh the cons, specially for a small team.
  - [Unable to drag window on Mac ](https://github.com/deta/surf/issues/94)
    - 必须将光标移到顶部resize改变窗口高度时，才可以移动窗口
  - [Show HN: Deta Surf – An open source and local-first AI notebook | Hacker News _202510](https://news.ycombinator.com/item?id=45680937)
    - We took inspiration from analog notebooks as a tool for thought, but wanted something for multi-media. We also see NotebookLM as the closest mainstream product to Surf.
    - 🆚📝 The big difference UX wise between chatbots and Surf is that Surf is built entirely on editable documents that you can mold / craft into an output (vs chat).
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

- https://github.com/rupeshs/verity /NALic/202602/python/js
  - a Perplexity-style AI search and answer engine that runs fully locally on AI PCs.
  - It combines SearXNG-powered search, retrieval, and local LLM reasoning to generate grounded, verifiable answers — without relying on cloud-based LLM providers.
  - Fully Local, AI PC Ready - Optimized for Intel AI PCs using OpenVINO (CPU / iGPU / NPU), Ollama (CPU / CUDA / Metal)
  - Privacy by Design - Search and inference can be fully self-hosted
  - SearXNG-Powered Search - Self-hosted, privacy-friendly meta search engine
  - Designed for fact-grounded, concise answers
  - OpenVINO and Ollama models supported
  - Modular architecture
  - CLI and WebUI support, API server support
  - [Verity, a Perplexity style AI search and answer engine that runs fully locally on AI PCs with CPU, GPU, NPU acceleration : r/LocalLLaMA _202602](https://www.reddit.com/r/LocalLLaMA/comments/1qz8clh/veritya_perplexity_style_ai_search_and_answer/)

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

- https://github.com/H0NEYP0T-466/Pen2PDF /MIT/202511/js
  - https://pen2-pdf.vercel.app/
  - a modern web application that offers six powerful productivity tools: AI-powered text extraction and PDF conversion, intelligent timetable management with Excel/CSV import, comprehensive todo list management with subtasks, smart notes generation with a searchable library, a full-featured digital whiteboard, and an AI assistant (Bella) for intelligent help - all designed to streamline your academic and professional workflow.

- https://github.com/CaviraOSS/PageLM /1.3kStar/NonCommercial/202512/ts/inactive
  - https://pagelm.spotit.dev/
  - a community driven version of NotebookLM & a education platform that transforms study materials into interactive resources like quizzes, flashcards, notes, and podcasts.

- https://github.com/zstmfhy/zlibrary-to-notebooklm /MIT/202601/python
  - 一键将 Z-Library 书籍自动下载并上传到 Google NotebookLM
# citation/sourcing
- https://github.com/preprocess-co/rag-document-viewer /MIT/202509/python/js
  - https://preprocess.co/rag-document-viewer
  - https://preprocess-rag-dv-demo.hf.space/
  - open-source library that generates high-fidelity file previews for seamless integration into your applications. 
  - It provides desktop-level file viewing capabilities for a wide range of document formats
  - The library converts these files into interactive HTML-based previews that can be easily embedded into web applications
  - You can now embed the viewer in your application with just an `<iframe>`.
  - 依赖LibreOffice、pdf2htmlEX, These tools are not bundled with the rag-document-viewer package; they must be installed on the host system where viewers are generated. 
  - 似乎不支持mac构建
  - Runs 100 % in-browser. Files are served directly from your backend under your auth logic, no external servers.
  - 🔗 Precise Highlights: Pass bounding-box coordinates from your RAG chunks; the viewer auto-scrolls and spotlights them.
    - You can get chunk coordinates from chunking providers like Preprocess.co (which supports paragraphs, layout items, multi-column layouts, slides, and more) or Unstructured.io (which offers PDF-only item-level support).
    - Chunks' coordinates should be stored in a list. When storing and then accessing a chunk, you should use the list index to reference the correct chunk.
    - If no chunk information is provided when generating the viewer, the following features will be disabled: Chunk highlighting and navigation

- https://github.com/zt6453928/ailat-translation /MIT/202601/python/js
  - AI-Powered Document Translation Tool
  - A web-based PDF document parsing and translation tool that supports intelligent document parsing, multi-language translation, and various export formats.
  - Supports PDF, DOCX and other document formats, extracts text, images, tables, and formulas
  - Export to PDF, Markdown, HTML, DOCX, JSON, LaTeX
  - Multiple Translation Engines: Supports DeepLX and OpenAI-compatible APIs
  - Real-time Preview: Side-by-side comparison of original and translated content
  - [开源一个支持多格式文档翻译应用 ](https://linux.do/t/topic/1511535)
    - 出于身边同学对论文翻译的需求，所以开发了这个项目，除了论文我也用来对一些AI教程文档进行翻译
    - 灵感来自于MinerU, PDF格式还支持对照翻译

- https://github.com/stanford-oval/WikiChat /1.5kStar/apache2/202504/python/inactive
  - https://wikichat.genie.stanford.edu/
  - WikiChat is an improved RAG. It stops the hallucination of large language models by retrieving data from a corpus.
  - WikiChat uses Wikipedia and the following 7-stage pipeline to makes sure its responses are factual. Each numbered stage involves one or more LLM calls.
  - [WikiChat: Stopping the Hallucination of Large Language Model Chatbots by Few-Shot Grounding on Wikipedia _202401](https://www.reddit.com/r/LocalLLaMA/comments/1920hho/wikichat_stopping_the_hallucination_of_large/)
  - [Is Wikipedia RAG possible entirely locally with a gaming machine? : r/ollama _202502](https://www.reddit.com/r/ollama/comments/1ihibp9/is_wikipedia_rag_possible_entirely_locally_with_a/)

- https://github.com/AdyTech99/volo /GPL/202501/python/inactive
  - combining AI with Wikipedia knowledge via a RAG pipeline
  - It utilizes an offline database of Wikipedia created by Kiwix, ensuring fast and reliable access to information without requiring constant internet connectivity.
  - Volo uses a tiny model (Qwen2.5:3b) and gives it the knowledge of nearly 7 million Wikipedia articles, making it a more reliable source of information than giant closed-source models like OpenAI's GPT4o and Anthropic's Claude 3.5 Sonnet, which are prone to hallucinations.
  - Offline Wikipedia Database: Leverages a `.zim` file from Kiwix, offering a snapshot of Wikipedia for offline access.
  - OpenAI-Compatible REST APIs: Use Volo with interfaces like Open WebUI or your own API client.
  - [Volo: An easy and local way to RAG with Wikipedia! : r/LocalLLaMA _202501](https://www.reddit.com/r/LocalLLaMA/comments/1hzsvkz/volo_an_easy_and_local_way_to_rag_with_wikipedia/)

- https://github.com/moodlehq/wiki-rag /BSD/202512/python
  - a project that leverages Mediawiki as a source for augmenting text generation tasks, enhancing the quality and relevance of generated content
  - RAG system specialised in ingesting MediaWiki sites via their API and providing an OpenAI API interface to interact with them.
  - Milvus 2.6.2 or later (for vector similarity search). Standalone or Distributed deployments are supported. Lite deployments are not supported.
  - Uses `LangGraph` for orchestration of the whole LLM pipeline.
  - Accepts virtually any Mediawiki site as a knowledge base (KB).
  - Uses Mediawiki API to extract content and metadata (not web crawling).
  - The whole KB is stored in a (dated) JSON file for later use, access and analysis.
  - Loads the KB into a vector database (Milvus) for fast retrieval.
  - Hybrid retrieval using both vector and keyword search with fusion reranking.
  - Exposed as a model using standard OpenAI API endpoints (v1/models and v1/chat/completions). Optionally protected with local or remote bearer tokens. Supports streaming responses.

- https://github.com/0nspaceshipearth/Hermit-AI /AGPL/202601/python
  - a privacy-first, 100% offline ai chatbot that lets you chat with wikipedia or any other `.zim` archive.
  - no cloud, no api keys, no tracking. everything stays on your machine.
  - [Hermit-AI: Chat with 100GB+ of Wikipedia/Docs offline using a Multi-Joint RAG pipeline : r/LocalLLM _202601](https://www.reddit.com/r/LocalLLM/comments/1q8mdwt/hermitai_chat_with_100gb_of_wikipediadocs_offline/)
    - I wanted to use Local AI along side my collection of ZIM files (Wikipedia, StackExchange, etc.) entirely offline. 
    - So I built a "Multi-Joint" Reasoning Pipeline. Instead of just doing one big search and hoping for the best, Hermit breaks the process down
    - Joint 1 (Extraction): It stops to ask "Who/What specifically is this user asking about?" before touching the database.
    - Joint 2 (JIT Indexing): It builds a tiny, ephemeral search index just for that query on the fly. This keeps it fast and accurate without needing 64GB of RAM.
    - Joint 3 (Verification): This is the cool part. It has a specific "Fact-Check" stage that reads the retrieved text and effectively says, "Wait, does this text actually support what the user is claiming?" If not, it corrects you.
    - zim is optimized for read-heavy content you rarely change.

- https://github.com/abgulati/LARS /622Star/AGPL/202410/python/inactive
  - LARS aims to be the ultimate open-source RAG-centric LLM application. Towards this end, LARS takes the concept of RAG much further by adding detailed citations to every response, supplying you with specific document names, page numbers, text-highlighting, and images relevant to your question
  - [Made a RAG-centric, Open-Source UI based on llama.cpp - With Advanced Source Citations & Referencing _202406](https://github.com/ggml-org/llama.cpp/discussions/7928)
  - [RAG for Documents with Advanced Source Citations & Referencing _202406](https://www.reddit.com/r/LocalLLaMA/comments/1db98el/rag_for_documents_with_advanced_source_citations/)

- https://github.com/upstash/wikipedia-semantic-search /MIT/202504/ts
  - https://wikipedia-semantic-search.vercel.app/
  - [Indexing Millions of Wikipedia Articles With Upstash Vector | Upstash Blog _202408](https://upstash.com/blog/indexing-wikipedia)
  - We've created a semantic search engine and Upstash RAG Chat SDK using Wikipedia data to demonstrate the capabilities of Upstash Vector and RAG Chat SDK.
  - Indexed over 144 million vectors from Wikipedia articles in 11 languages
  - Used BGE-M3 embedding model for multilingual support

- https://github.com/ollmer/wikichat /202401/python/inactive
  - Talk to Wikipedia offline using llama.cpp models and semantic search over the index of the whole English Wikipedia (44 million paragraphs).

- https://github.com/imDelivered/KiwixRAG /202512/python
  - A powerful offline-capable chatbot with Retrieval-Augmented Generation (RAG) that lets you chat with AI using local knowledge bases like Wikipedia, Python documentation, or any ZIM file archive.
  - Note: This software is currently only available for Linux. Windows and macOS support may be added in the future.
  - Download a ZIM file (e.g., from Kiwix), The chatbot will automatically detect and use it
  - Beautiful GUI built with tkinter
  - Hybrid Search: Semantic (FAISS) + keyword (BM25) search  
  - Just-In-Time Indexing: Auto-indexes articles on-the-fly
  - Multiple Models: Switch between any Ollama model
  - KiwixRAG uses a multi-joint architecture where three small AI reasoning models work together to prevent hallucinations and ensure accurate responses.
  - For faster retrieval on large ZIM files, you can pre-build an index
  - [Kiwix RAG: Terminal Chat Interface with Local Kiwix Content Integration : r/Kiwix _202512](https://www.reddit.com/r/Kiwix/comments/1pdio0i/kiwix_rag_terminal_chat_interface_with_local/)
  - [I built an offline AI chat app that automatically pulls Wikipedia articles for factual answers - runs completely locally with Ollama : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1pd2x8u/i_built_an_offline_ai_chat_app_that_automatically/)

- https://github.com/epheterson/zimi /MIT/202602/python
  - Search and read 100M+ articles offline. API-first knowledge server for ZIM files.
  - Kiwix packages the world's knowledge into ZIM files — offline archives of Wikipedia, Stack Overflow, dev docs, and thousands of other sources
  - Zimi makes them useful: JSON API for AI agents — search, read, and browse articles programmatically
  - Library manager — browse the Kiwix catalog and download ZIMs from the UI
  - Cross-ZIM search with relevance ranking, deduplication, and time budgets
  - Persistent cache — instant startup on subsequent runs
  - [Zimi – ZIM file access for AI agents and humans (UI, API, more...) : r/Kiwix _202602](https://www.reddit.com/r/Kiwix/comments/1r4f6vv/zimi_zim_file_access_for_ai_agents_and_humans_ui/)
    - I tried to use Claude Code to access my ZIM files and realized there's no great way to do that, so I built one.
    - It runs locally or in Docker and can be used via API, CLI, MCP, or a web UI in the browser.

- https://github.com/rouralberto/zim-llm /202508/python/inactive
  - [Building an Offline Knowledge Base with Kiwix Zim and Docker Model Runner - Alberto Roura](https://albertoroura.com/building-an-offline-knowledge-base-with-zim-and-docker-model-runner/)
  - This project provides a comprehensive system for processing ZIM files (compressed Wikipedia/offline content databases) and creating a vector database for Retrieval-Augmented Generation (RAG) with Large Language Models, effectively having an offline knowledge base.
  - Dynamic ZIM Library: Automatically discovers and processes multiple ZIM files from a dedicated library directory
  - Multi-format ZIM Support: Supports libzim, zimply, and CLI-based ZIM file reading
  - Flexible Vector Databases: Choose between ChromaDB and FAISS for storage
  - Local LLM Support: Docker Model Runner for offline LLM capabilities
  - Export articles from multiple ZIM files to JSON

- https://github.com/mozanunal/llm-tools-kiwix /202506/python/inactive
  - [I made an LLM tool to let you search offline Wikipedia/StackExchange/DevDocs ZIM files (llm-tools-kiwix, works with Python & LLM cli) : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1l3fdv3/i_made_an_llm_tool_to_let_you_search_offline/)

- https://github.com/tylertitsworth/multi-mediawiki-rag /202408/archived
  - A simple RAG chatbot that can retrieve from a mediawiki data dump
  - Mediawikis hosted by Fandom usually allow you to download an XML dump of the entire wiki as it currently exists
  - Your XML data needs to be loaded and transformed into embeddings to create a Chroma VectorDB.

- https://github.com/MauroAndretta/WikiRag /apache2/202408/python/inactive
  - RAG system designed for question answering, it reduces hallucination thanks to the RAG architecture. 
  - It leverages Wikipedia content as a knowledge base.
  - It integrates various components like Ollama, HuggingFaceEmbeddings, and Qdrant to create a powerful system

- https://github.com/zeyu-chen/Wikipedia-KG-RAG /202411/python/inactive
  - An intelligent question-answering system powered by knowledge graphs, combining Neo4j database and Wikipedia data for efficient Retrieval-Augmented Generation (RAG).
  - Hybrid vector and graph-based search
  - Real-time Updates - Dynamic Wikipedia data synchronization

- https://github.com/BurnyCoder/wikipedia-ai-agent /202501/inactive
  - AI agent research assistant that uses Wikipedia's vast knowledge base to deliver comprehensive, well-researched answers to your questions.
  - Built on a modern stack including LangChain's LangGraph's ReAct agent, Wikipedia API, FAISS vector storage, Microsoft's GraphRAG, support for leading LLM providers (OpenAI, Anthropic, Google), and Streamlit frontend.

- https://github.com/spring-projects-2024/wiki-savvy-rag /202411/inactive
  - build a Wikipedia-backed RAG system expert about STEM subjects. Features a streamlit demo.
  - We downloaded, filtered and cleaned the English Wikipedia (~100GB) and built a vector database of semantic embeddings based on all STEM articles, using the FAISS library for efficient retrieval of embeddings and SQLite for accessing text chunks from disk

- https://github.com/RUC-NLPIR/FlashRAG /MIT/202511/python
  - A Python Toolkit for Efficient RAG Research (WWW2025 Resource)
  - Features 23 advancing RAG algorithms with reported results, based on our framework.
  - [If you want to use Wikipedia as your corpus, you can download the Wikipedia dump you require in XML format](https://github.com/RUC-NLPIR/FlashRAG/blob/main/docs/original_docs/process-wiki.md)
  - https://github.com/RUC-NLPIR/FlashRAG-Paddle
    - built on the PaddlePaddle framework and PaddleNLP, which is optimized for Chinese-developed chips and computing platforms.

- https://github.com/TIGER-AI-Lab/LongRAG /202408/inactive
  - code for "LongRAG: Enhancing Retrieval-Augmented Generation with Long-context LLMs"
  - LongRAG, consisting of a "long retriever" and a "long reader". Our framework use a 4K-token retrieval unit, which is 30x longer than before. 
  - We leverage open-sourced dense retrieval toolkit, Tevatron. 

- https://github.com/neuml/txtchat /apache2/202505/python/inactive
  - txtchat builds autonomous agents, retrieval augmented generation (RAG) processes and language model powered chat applications.
  - Wikitalk: Retrieval Augmented Generation (RAG) with Wikipedia

- https://github.com/neuml/txtai/tree/master/examples
  - [Local RAG Streamlit Apps for querying Wikipedia and ArXiv : r/LocalLLaMA _202406](https://www.reddit.com/r/LocalLLaMA/comments/1dq6kem/local_rag_streamlit_apps_for_querying_wikipedia/)
  - The data source is self contained. There is no direct querying of Wikipedia.

- https://github.com/neuml/ragdata /apache2/202507/python/inactive
  - ragdata builds knowledge bases for Retrieval Augmented Generation (RAG).
  - The currently supported datasets are: ArXiv, Wikipedia
  - This project has processes to build txtai embeddings databases for common datasets.
- https://github.com/myscale/ChatData /MIT/202406/python/inactive
  - a robust chat-with-documents application designed to extract information and provide answers
  - The knowledge base is a snapshot on 2022-12.

- https://github.com/achyuthkumarmiryala/Wikipedia-RAG-QA /MIT/202505/python
  - RAG system that answers natural-language questions on any Wikipedia topic.
  - It combines dense vector retrieval (FAISS + Sentence Transformers) with a Hugging Face question-answering model, wrapped in a friendly Gradio interface.
  - Real-time Wikipedia retrieval – pulls the latest content directly from Wikipedia’s API.
  - Semantic search – encodes text with all-mpnet-base-v2 and finds the most relevant passages using FAISS.
  - run locally or publish to Hugging Face Spaces with the same app.py.

- https://github.com/exowanderer/WikidataChat /202411/inactive
  - RAG with for answering question with the Wikidata REST API
  - Search and Download: Utilizes Google's Serapi search pipeline and Wikidata's REST API to fetch relevant JSON data.
  - RAG Pipeline: Merges Wikidata string statements with user-provided questions to generate informed and accurate answers through an LLM.

- https://github.com/ahmedo42/wikiqa /202409/inactive
  - RAG pipeline built for answering questions by retrieving the most relevant wikipedia articles using the Wikipedia API and the Google Search API.

- https://github.com/datastaxdevs/workshop-wikipedia-qa /202311/inactive
  - Real-time document Q&A using Pulsar, Cassandra, LangChain, and open-source language models.
  - This workshop code runs a Retrieval Augmented Generation (RAG) application stack that takes data from Wikipedia, stores it in a vector database (Astra DB), and provides a chat interface for asking questions about the Wikipedia documents.

- https://github.com/Shreyjain203/Wikipedia-Continual-Learning-RAG /202404/python/inactive
  - When a user asks a question, the model provides an answer. If the model is unable to answer, it uses get_data.py to fetch more information and fine-tunes itself before providing an appropriate answer.

- https://github.com/wikimedia/wikipedia-preview /MIT/202512/js
  - https://wikimedia.github.io/wikipedia-preview/main
  - https://wikimedia.github.io/wikipedia-preview/main/storybook
  - a JavaScript component that allows you to provide context from Wikipedia about words or phrases on any website. 
  - It lets you show a popup card with a short summary from Wikipedia when a reader hovers over a link: Read full article on Wikipedia 
  - Works with any link that has an article on Wikipedia

- https://github.com/rahulanand1103/rag-citation /MIT/202411/python/inactive
  - RAG Citation enhances Retrieval-Augmented Generation (RAG) by automatically generating relevant citations for AI-generated content

- https://github.com/thomassbooth/document-citation-rag /202410/python/ts
  - This project implements a Retrieval-Augmented Generation (RAG) system using Python and a frontend built with Nextjs - TypeScript, and advanced retrieval strategies: Multi-Query, RAG Fusion 
  - It leverages Qdrant and uses streaming responses to delivery queries to the frontend. 

- citation-examples
  - [Bluebook Citation Generator - Instant Legal Citations & OCR](https://bluebookcitationgenerator.com/)
# examples/apps
- https://github.com/dmayboroda/minima /MPL/202512/python/ts
  - On-premises conversational RAG with configurable containers
  - open source RAG on-premises containers, with ability to integrate with ChatGPT and MCP. 
  - Minima can also be used as a fully local RAG or with your own deployed LLM.
  - Minima currently supports 3 modes:
    - Isolated installation (Ollama) – Operate fully on-premises with containers. All neural networks (LLM, reranker, embedding) run on your cloud or PC 
    - Custom LLM (OpenAI-compatible API) – Use your own deployed LLM with OpenAI-compatible API (vLLM, Ollama server, TGI, etc.). The indexer runs locally while the LLM can be on your server, cloud, or local machine.
    - Custom GPT – Query your local documents using ChatGPT app or web with custom GPTs. The indexer runs on your cloud or local PC, while the primary LLM remains ChatGPT.

- https://github.com/HKUDS/DeepTutor /9.3kStar/AGPL/202601/python/ts
  - https://hkuds.github.io/DeepTutor
  - AI-Powered Personalized Learning Assistant
  - Smart Knowledge Base: Upload textbooks, research papers, technical manuals, and domain-specific documents. 
  - Multi-Agent Problem Solving: Dual-loop reasoning architecture with RAG, web search, and code execution -- delivering step-by-step solutions with precise citations.
# data-rag
- https://github.com/statespace-tech/toolfront /801Star/MIT/202512/python
  - https://docs.toolfront.ai/
  - Turn your data into shareable RAG apps in minutes. All in pure Markdown.
  - [I built an MCP that finally makes your local AI models shine with SQL : r/LocalLLaMA _202506](https://www.reddit.com/r/LocalLLaMA/comments/1ll3qej/i_built_an_mcp_that_finally_makes_your_local_ai/)
  - ToolFront equips AI models with a set of read-only database tools
# benchmark-rag ⚡️
- https://github.com/Aaryanverma/trustifai /MIT/202601/python
  - a Python-based observability engine designed to evaluate the trustworthiness of LLM responses and Retrieval-Augmented Generation (RAG) systems. 
  - Unlike simple evaluation frameworks that rely on a single "correctness" score, TrustifAI computes a multi-dimensional Trust Score based on grounding, consistency, alignment, and diversity.
  - It also includes visualizations to help showcase why a model output was deemed unreliable.
  - [A framework to evaluate RAG answers in production : r/Rag](https://www.reddit.com/r/Rag/comments/1qpla70/a_framework_to_evaluate_rag_answers_in_production/)

- https://huggingface.co/datasets/G4KMU/t2-ragbench
  - [T2-RAGBench - Benchmark for RAG in Finance (10K Downloads on HF) : r/Rag](https://www.reddit.com/r/Rag/comments/1pde2au/t2ragbench_benchmark_for_rag_in_finance_10k/)
# more
- https://github.com/teng-lin/notebooklm-py /MIT/202601/python
  - The missing API for Google NotebookLM. 
  - [I mapped Google NotebookLM's internal RPC protocol to build a Python Library : r/Python _202601](https://www.reddit.com/r/Python/comments/1qbtgws/i_mapped_google_notebooklms_internal_rpc_protocol/)

- https://github.com/tensorlakeai/tensorlake /817Star/apache2/202512/python
  - https://tensorlake.ai/
  - Tensorlake is a Document Ingestion API and a serverless platform for building data processing and orchestration APIs
  - Parse documents (PDFs, DOCX, spreadsheets, presentations, images, and raw text) to markdown or extract structured data with schemas. This is powered by Tensorlake's state of the art layout detection and table recognition models.
  - Deploy Agentic Applications and AI Workflows using durable functions, with sandboxed and managed compute infrastructure that scales your agents with usage.
  - Sign up at cloud.tensorlake.ai and get your API key.

- [LanceDB Demos - Wikipedia 41M Hybrid Search](https://lancedb-demos.vercel.app/demo/wikipedia-search)
  - https://x.com/lancedb/status/2001327573968572579
  - We built WikiSearch, a search engine that stores and searches through real Wikipedia entries. 
  - The demo showcases how to use LanceDB’s full-text and hybrid search features to quickly find relevant information in a large dataset like Wikipedia.
  - [LanceDB WikiSearch: Native Full-Text Search on 41M Wikipedia Docs _202508](https://lancedb.com/blog/feature-full-text-search/)

- [One of our engineers wrote a 3-part series on building a RAG server with PostgreSQL : r/Rag _202512](https://www.reddit.com/r/Rag/comments/1pq79v4/one_of_our_engineers_wrote_a_3part_series_on/)
  - [Building a RAG Server with PostgreSQL - Part 1: Loading Your Content](https://www.pgedge.com/blog/building-a-rag-server-with-postgresql-part-1-loading-your-content)
