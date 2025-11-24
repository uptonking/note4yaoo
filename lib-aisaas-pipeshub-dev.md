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
  - create custom apps and AI agents using a No-Code interface
  - graph: All data is structured into a powerful knowledge graph
  - Modular & Scalable Architecture – Every service is loosely coupled to scale independently
  - 支持上传本地文件: pdf, docx, xlsx, csv, markdown, images, audio, video
  - 官方提供很多外部数据源的集成: google-drive/gmail/docs, OneDrive, slack, notion, airtable, github
  - 支持直接在界面上配置第三方依赖 redis/kafka/mongo/qdrant

- cons
  - AGI内容只包含知识库中的内容，不包含llm自身知识，经常拒绝用户 I cannot answer your query
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

- 删除文档时，未实现回收站

- 不选择kb知识库时，不支持随意聊天

- search
  - 不仅支持sources, 还支持搜索 comments/discussions

- local-models
  - 本地的prompt-processing速度非常慢

- open source alternative
  - Google just dropped the Gemini File Search API (RAG-as-a-Service)
    - It allowed me to build a RAG chatbot in 31 min. No coding

- ~~未实现流式输出~~

- 
- 
- 
- 

# dev-xp
- 💥 无法embedding大文档, 本地lmstudio提示
  - [lmstudio-llama-cpp] Error in predictTokens: The number of tokens to keep from the initial prompt is greater than the context length. Try to load the model with a larger context length, or provide a shorter input

- 使用本地model时，不要使用global proxy, lmstudio/langchain存在问题

- 
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
  - 通过LiteLLM的配置支持本地Ollama/LMStudio

- cons
  - citation点击后查看的事chunk文本, 体验不如pdf
  - 上传pdf后不支持查看pdf原文, sources中保存的数据是处理过的文本内容, citation
  - 聊天对话不支持流式输出，等待时间较长
  - 不能以用户提问的语言回复用户
  - 整个回复内容有时citation的编号都是同1处

## draft

- 是否使用了本地embedding

- 
- 
- 
