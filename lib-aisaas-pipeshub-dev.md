---
title: lib-aisaas-pipeshub-dev
tags: [pipeshub]
created: 2025-11-16T15:33:44.605Z
modified: 2025-11-16T15:34:02.881Z
---

# lib-aisaas-pipeshub-dev

# guide

- pros
  - 支持使用本地llm
  - AGI内容中包含知识库中的内容引用，点击时能自动打开原文pdf并高亮原文位置
  - create custom apps and AI agents using a No-Code interface

- cons
  - AGI内容只包含知识库中的内容，不包含llm自身知识，经常拒绝用户 I cannot answer your query 
  - ai回复的内容简短不够丰富，体验不如 SurfSense

- features
  - ?
# draft
- 不选择kb知识库时，不支持随意聊天

- 
- 
- 
- 

# dev-xp

## devops

```sh
# ArangoDB
docker run -d --name arangodb -p 8529:8529 -e ARANGO_ROOT_PASSWORD=11111111 arangodb/arangodb:latest

docker run -d --name zookeeper -p 2181:2181 \
  -e ZOOKEEPER_CLIENT_PORT=2181 \
  -e ZOOKEEPER_TICK_TIME=2000 \
  confluentinc/cp-zookeeper:7.9.0

docker run -d --name kafka --link zookeeper:zookeeper -p 9092:9092 \
  -e KAFKA_BROKER_ID=1 \
  -e KAFKA_ZOOKEEPER_CONNECT=zookeeper:2181 \
  -e KAFKA_ADVERTISED_LISTENERS=PLAINTEXT://localhost:9092 \
  -e KAFKA_LISTENER_SECURITY_PROTOCOL_MAP=PLAINTEXT:PLAINTEXT \
  -e KAFKA_INTER_BROKER_LISTENER_NAME=PLAINTEXT \
  -e KAFKA_OFFSETS_TOPIC_REPLICATION_FACTOR=1 \
  confluentinc/cp-kafka:7.9.0

# python -m spacy download en_core_web_sm
uv run python -m spacy download en_core_web_sm
uv run python -c "import nltk; nltk.download('punkt')"

# Run each service in a separate terminal
uv run python -m app.connectors_main
uv run python -m app.indexing_main
uv run python -m app.query_main
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
- 
- 
- 
- 
- 
