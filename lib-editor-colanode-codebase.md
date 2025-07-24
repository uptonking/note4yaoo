---
title: lib-editor-colanode-codebase
tags: [codebase, colanode]
created: 2025-06-21T19:12:41.819Z
modified: 2025-06-21T19:12:59.931Z
---

# lib-editor-colanode-codebase

# guide

- self-host
  - pgvector: postgres://user:pass@localhost:5432/colanode_db
  - minio: http://localhost:9000
    - http://localhost:52119/ (minioadmin)
  - redis: redis://127.0.0.1:6379
  - AI_ENABLED
  - When you go to the login screen of Colanode, open the servers dropdown and click 'Add new server'. 
    - http://localhost:3000/config

```shell
# backend
minio server /Users/yaoo/Documents/runappdata/miniocolanodedata

cd cd apps/server
npm run dev

# frontend 
# http://localhost:4000/
cd apps/web
npm run dev

cd apps/desktop
npm run dev
```

# overview

# frontend

# backend

# more
