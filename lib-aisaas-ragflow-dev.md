---
title: lib-aisaas-ragflow-dev
tags: [rag, ragflow]
created: 2025-12-06T13:25:01.462Z
modified: 2025-12-06T13:25:29.309Z
---

# lib-aisaas-ragflow-dev

# guide
- pros
  - ?

- cons
  - 从主流的 elasticsearch 迁移到自研的 infinity 数据库是否会降低系统的灵活性和扩展性

- features
  - ?

- tips
  - ?
# draft

# dev-xp

## devops

- resources
  - [Get started | RAGFlow](https://ragflow.io/docs/dev/)
  - [Deploy local models | RAGFlow](https://ragflow.io/docs/dev/deploy_local_llm)

- this project provides a rag webapp that supports file uploading and asking questions about files with local/online models.
  - i have run this project fully locally without docker for local development and debugging, using Ollama chat/embedding models.
  - the backend starts by `source .env && bash docker/launch_backend_service.sh`, the frontend starts by `cd web && npm run dev`.

```sh
cd ~/Documents/opt/compiled/elasticsearch-8.11.3 && ./bin/elasticsearch

# Create bucket: ragflow
minio server --address :9000 --console-address :9001  ~/Documents/repos/libfwk/ai-llm/all-rag/ragflow/docker/data

OLLAMA_DEBUG=2 ollama serve

# backend
source .venv/bin/activate
export PYTHONPATH=$(pwd)
source .env
bash docker/launch_backend_service.sh

# frontend
cd web/
nvm use 22
npm install
npm run dev
```

# more
