---
title: lib-aisaas-pipeshub-dev
tags: [pipeshub]
created: 2025-11-16T15:33:44.605Z
modified: 2025-11-16T15:34:02.881Z
---

# lib-aisaas-pipeshub-dev

> extensible and explainable workplace AI platform for enterprise search and workflow automation

# guide
- pros
  - license: apache2
  - 🔗 insights with citations: traceable source in every answer combined with confidence scores
    - AGI内容中包含知识库中的内容引用，点击时能自动打开原文pdf并高亮原文位置
  - 支持使用本地llm, 包括ollama/lmstudio
  - 🇨🇳 对中文的支持较好
  - create custom apps and AI agents using a No-Code interface
  - graph: All data is structured into a powerful knowledge graph
  - Modular & Scalable Architecture – Every service is loosely coupled to scale independently
  - 支持上传本地文件: pdf, docx, xlsx, csv, markdown, images, audio, video
  - 官方提供很多外部数据源的集成: google-drive/gmail/docs, OneDrive, slack, notion, airtable, github
  - 支持直接在界面上配置第三方依赖 redis/kafka/mongo/qdrant

- cons
  - AGI内容只包含知识库中的内容, 不包含llm自身知识，经常拒绝用户 I cannot answer your query
  - ai回复的内容简短不够丰富，体验不如 SurfSense
  - ai思考时间过长, 界面上没有交互反馈
  - 💥 本地lmstudio, 无法embedding大文档
  - 架构复杂，依赖 kafka
  - 未实现online search集成，如tavily/exa/SearxNG
  - roadmap
    - Code Search
    - Workplace AI Agents
    - MCP
    - APIs and SDKs
    - Personalized Search
    - Highly available and scalable Kubernetes deployment
    - PageRank

- features
  - 使用 arangodb 实现图结构的数据关系逻辑
  - Real-Time or Scheduled Indexing – Index data as it flows or schedule it to run exactly when you need
  - Source-level permissions ensure every document is shown only to those who are authorized
  - 基于langchain/langgraph实现
  - 能以用户提问的语言回复用户

- tips 💡
  - 虽然性能及功能上有缺点, 但功能较丰富、体验较友好、复杂度也不高, 值得深入优化
    - 完善的方案很难找, 可以尝试改进现有的方案
  - 文件内容提取工具或格式转换工具，缺少应用层chunking/embedding/vector的高性能调度逻辑

- SurfSense
  - 架构简单，依赖不多, 主要依赖PGVector/Redis
  - file formats (Documents, images, videos and supports 50+ file extensions)
  - External Sources: Tavily, SearxNG, Slack, Linear, Jira, Notion
  - Powerful Search
  - Get Cited answers just like Perplexity
  - Local LLM Support
  - 提供了浏览器扩展
  - fast podcast generation agent. (Creates a 3-minute podcast in under 20 seconds.)
  - Advanced RAG Techniques
    - Uses Hierarchical Indices (2 tiered RAG setup).
    - Supports all major Rerankers (Pinecode, Cohere, Flashrank etc)
    - Utilizes Hybrid Search (Semantic + Full Text Search combined with Reciprocal Rank Fusion).
  - Work together effortlessly with real-time collaboration
# not-yet ❓
- 为何启动后端要在4个terminal运行4个端口不同的服务, indexing/query/docling/connectors
  - 为什么不是一个api，然后使用4个不同的route url
# draft
- topics
  - Wikipedia
  - developer docs: react/vue/ecmascript/python/golang/pg

- 
- 
- 

- 不选择kb知识库时，不支持随意聊天

- search
  - 不仅支持sources, 还支持搜索 comments/discussions

- local-models
  - 本地的prompt-processing速度非常慢

- 处理大pdf时chunking/embedding的进度反馈出来更好, 可重试可恢复更好, 目前的实现感觉一直卡在inprogress然后就失败了

- 删除文档时，未实现回收站

- 统一不同数据源的搜索/AGI体验
  - pdf
  - wikipedia-zim
  - mdn-docs-offline
  - dictionary

- 
- 
- 
- 
- 
- 

- open source alternative
  - Google just dropped the Gemini File Search API (RAG-as-a-Service)
    - It allowed me to build a RAG chatbot in 31 min. No coding

- ~~未实现流式输出~~

## large-pdf/docs 💥

- 提升处理超大pdf的能力
  - 可参考pymupdf4llm
  - 可参考 https://github.com/v4ler11/llm-chat

- https://github.com/renton4code/pdf-rag /AGPL/202502/ts/inactive
  - A production-ready template for building Retrieval-Augmented Generation (RAG) applications. 
  - This template provides a complete setup for document processing, vector storage, and AI-powered question answering with kickass UI.
  - PDF document processing with OCR
  - Milvus DB with billions of vectors scale support: Vector DB for storing embeddings
  - PostgreSQL: Relational DB for metadata storage
  - Click-to-view document references with highlighting
  - Large documents processing and status updates
  - AI/ML: Google Gemini (LLM), HuggingFace Transformers (Embeddings)
  - Based on Q&A with a large document (700+ pages) in comparison to RagFlow

- [How to Summarize Large Documents with LangChain and OpenAI _202405](https://medium.com/@myscale/how-to-summarize-large-documents-with-langchain-and-openai-4312568e80b1)
  - We have over 466, 000 tokens in this book, and if we pass them all directly to the LLM, it would charge us a lot. So, to reduce the cost, we will implement K-means clustering to extract the important chunks from the book.
  - We will split the book content into documents by using the SemanticChunker utility of LangChain.
  - we’ll transform the document vectors into a format compatible with Faiss, cluster them into 50 groups using K-means, and then create a Faiss index for efficient similarity searches among documents.

- [Late Chunking: Embedding First Chunk Later — Long-Context Retrieval in RAG Applications _202409](https://blog.stackademic.com/late-chunking-embedding-first-chunk-later-long-context-retrieval-in-rag-applications-3a292f6443bb)
  - In late chunking, the process of embedding happens first for the entire document, ensuring that every token’s embedding retains the document’s full context. 
  - Only after this embedding process do you chunk the embeddings into smaller parts, which are contextually rich because they preserve relationships between distant parts of the document. 
  - This approach ensures that each chunk maintains the global document context, leading to more precise and meaningful retrieval results.
  - [Late_Chunking_in_Long_Context_Embedding_Models.ipynb - Colab](https://colab.research.google.com/drive/19dZeMCx-7g0kPz35e5gEjtAIama38gGI?usp=sharing)

- [Building a PDF-Powered AI: Embeddings + ChromaDB + Ollama RAG Pipeline _202507](https://medium.com/@eliyaser3121/building-a-pdf-powered-ai-embeddings-chromadb-ollama-rag-pipeline-372aaab62aa8)
# dev-xp
- 💥 无法embedding大文档, 本地lmstudio提示
  - [lmstudio-llama-cpp] Error in predictTokens: The number of tokens to keep from the initial prompt is greater than the context length. Try to load the model with a larger context length, or provide a shorter input
  - libc++abi: terminating due to uncaught exception of type std::runtime_error: [METAL] Command buffer execution failed: Caused GPU Timeout Error (00000002:kIOGPUCommandBufferCallbackErrorTimeout)

- 使用本地model时，不要使用global proxy, lmstudio/langchain存在问题

- 上传大文件的场景
- 场景1, 上传7M/400页的pdf, Content exceeds 108800 tokens (108881). Truncating to head.
  - lmstudio的log感觉卡住, Prompt processing progress: 0.0%
  - 整个mac系统都有卡死的感觉

- 
- 
- 

## devops

```sh
# qdrant vector, 6333
cd ~/Documents/opt/compiled/qdrant && ./qdrant

# ArangoDB
docker run --name arangodb -p 8529:8529 -e ARANGO_ROOT_PASSWORD=11111111 arangodb/arangodb:latest
docker start arangodb

docker run -d --name zookeeper -p 2181:2181 \
  -e ZOOKEEPER_CLIENT_PORT=2181 \
  -e ZOOKEEPER_TICK_TIME=2000 \
  confluentinc/cp-zookeeper:7.9.0
docker start zookeeper

docker run -d --name kafka --link zookeeper:zookeeper -p 9092:9092 \
  -e KAFKA_BROKER_ID=1 \
  -e KAFKA_ZOOKEEPER_CONNECT=zookeeper:2181 \
  -e KAFKA_ADVERTISED_LISTENERS=PLAINTEXT://localhost:9092 \
  -e KAFKA_LISTENER_SECURITY_PROTOCOL_MAP=PLAINTEXT:PLAINTEXT \
  -e KAFKA_INTER_BROKER_LISTENER_NAME=PLAINTEXT \
  -e KAFKA_OFFSETS_TOPIC_REPLICATION_FACTOR=1 \
  confluentinc/cp-kafka:7.9.0
docker start kafka

# Starting Node.js Backend Service
cd backend/nodejs/apps
cp ../../env.template .env 
npm install
# 3000
npm run dev

# Setting Up Frontend
cd frontend
cp env.template .env
# 3001
npm run dev

# Starting Python Backend Services
cd backend/python
cp ../env.template .env
# uv venv
# source .venv/bin/activate #uv会自动激活，仅首次需要
# uv run python -m spacy download en_core_web_sm
uv add pip
uv run python -m spacy download en_core_web_sm

uv run python -c "import nltk; nltk.download('punkt')"

# 限制python版本 `requires-python = ">=3.10,<3.11"`
# Run each service in a separate terminal
# 8088
uv run python -m app.connectors_main
# 8091
uv run python -m app.indexing_main
# 8000
uv run python -m app.query_main
# 8081
uv run python -m app.docling_main

```

- `backend/nodejs/apps/src/libs/enums/db.enum.ts`: `export const ARANGO_DB_NAME = 'es'; export const MONGO_DB_NAME = 'es';`.
  - The issue is that `MONGO_DB_NAME` is hardcoded to 'es' instead of reading from your `MONGO_DB_NAME` environment variable.

- [Arango Installation Documentation](https://docs.arango.ai/arangodb/stable/operations/installation/)
  - ArangoDB requires systems with Little Endian byte order.
  - You can run ArangoDB on Linux directly (bare metal) or in containers.
  - Starting with version 3.12, ArangoDB packages for Windows and macOS are not provided anymore. You can use the official Docker images  instead.
# more

# docs

- PipesHub AI helps you quickly find the right information using natural language search—just like Google.
- The platform not only delivers the most relevant results but also shows where the information came from, with proper citations, using Knowledge Graphs and Page Ranking. 
- Beyond search, our platform allows enterprises to create custom apps and AI agents using a No-Code interface.

- 
- 
- 

# SurfSense
- pros
  - ~~支持超大文档~~(系统限制500页)的分批summarizing/chunking/embedding
    - 实测上传400页文档时, 处理1h后仍然出现异常 [lmstudio-llama-cpp] Error in predictTokens: The number of tokens to keep from the initial prompt is greater than the context length. 
  - 支持通过UI来配置llm provider url, 但不同workspace的url非全局, 不能共享需要重新配置一次
    - 通过LiteLLM的配置支持本地Ollama/LMStudio

- cons(bug特别多)
  - chunk的内容是summary，而不是原文，准确度不够高, (❓ 原文似乎未在系统中无法查看)
    - 上传pdf后不支持查看pdf原文, sources中保存的数据是处理过的文本内容
  - citation点击后查看的是chunk文本, 体验不如pdf原文
  - chat不支持export
  - 上传中文pdf后，chunk的内容是英文summary，设置了workspace级的语言为中文后chunk仍是英文
  - 有时不能以用户提问的语言回复用户
  - 有时整个回复内容citation的编号都是同1处, 特别是回复中文内容时
  - 点击chat列表切换聊天记录时，容易出现ai重新regenerate内容的问题
  - ~~chat聊天对话不支持流式输出，体验很慢~~, 20251205已支持

- features
  - Multiple File Formats
  - Cited Answers
  - Local LLM Support
  - External Sources: Tavily/SearxNG, slack, linear, notion, github, discord...

## not-yet

- ❓是否使用了本地embedding? 
  - 似乎使用了，但配置使用本地lmstudio的embedding模型错误

- 上传文档后， 原文似乎未在系统中无法查看
  - RAG Pipeline Implementation for PDFs
    - 1. Full Content Processing
      - PDFs are processed through ETL services (Unstructured/LlamaCloud/Docling) in file_processors.py:131
      - The complete extracted content is stored in the `Document.content` field
      - This content is then chunked using create_document_chunks from document_converters.py
    - 2. Dual-Level Embedding System
      - Document-level: Summary embedding stored in Document.embedding 
      - Chunk-level: Each chunk gets its own embedding in Chunk.embedding 
    - Hybrid Search Implementation
      - Both levels use hybrid search combining
      - Vector similarity search (embeddings)
      - Full-text search
      - Reciprocal Rank Fusion (RRF) for result ranking
  - Document-level search uses summary embeddings (more efficient for finding relevant documents)
    - Chunk-level search provides access to the full original content through individual chunks
  - The system supports both SearchMode. CHUNKS and SearchMode. DOCUMENTS
    - The default search mode might be set to DOCUMENTS which searches document summaries instead of chunk content
  - document.content: 存储 LLM 生成的摘要，不是原始内容
    - document.embedding: 存储文档摘要的嵌入向量
  - document.chunks: 存储原始内容的分块，每个块都有自己的嵌入向量

## draft

- 💥 大文档页数限制, 似乎对summary建立index成功了，但未对chunk建立index， 功能bug多
  - Failed task process_file_upload: Page limit exceeded before processing
  - [lmstudio-llama-cpp] Error in predictTokens: The number of tokens to keep from the initial prompt is greater than the context length. Try to load the model with a larger context length, or provide a shorter input
- 未完全建立index的情况下仍然可以聊天，但聊天会出现如下超限的异常
  - The number of tokens to keep from the initial prompt is greater than the context length. Try to load the model with a larger context length, or provide a shorter input
  - Token indices sequence length is longer than the specified maximum sequence length for this model (340362 > 262144). Running this sequence through the model will result in indexing errors

- 
- 
- 
- 
- 
- 
- 

## dev-xp-surfsense

- lm studio的配置为 `lm_studio`

- 
- 
