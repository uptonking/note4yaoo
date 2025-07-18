---
title: lib-editor-block-lasuite-codebase
tags: [codebase, lasuite-docs]
created: 2025-07-17T14:40:19.493Z
modified: 2025-07-17T14:40:30.038Z
---

# lib-editor-block-lasuite-codebase

# guide

- services(14)
  - django-celery-dev
    - app-dev
      - postgresql
      - redis
      - mailcatcher
      - createbuckets
        - minio
  - y-provider
  - nginx
    - keycloak
      - kc_postgresql
  - frontend-dev, node, crowdin

```shell
# start lasuite-docs

# webapp
cd ./src/frontend/apps/impress
yarn
yarn dev

# backend - django

```

- urls
  - webapp http://localhost:3000/
  - admin http://localhost:8071/admin
    - user: admin@example.com ,  pass: admin
# overview

# frontend

# backend
- 获取文档内容的Get请求 http://localhost:8071/api/v1.0/documents/39cadaaa-4d96-40f1-b864-491554de0574/
  - 返回的文档内容是编码过的，不是原始内容

```JS
{
  "id": "39cadaaa-4d96-40f1-b864-491554de0574",
  "abilities": {
    "accesses_manage": true,
    "accesses_view": true,
    "ai_transform": true,
    "ai_translate": true,
    "attachment_upload": true,
    "media_check": true,
    "children_list": true,
    "children_create": true,
    "collaboration_auth": true,
    "cors_proxy": true,
    "descendants": true,
    "destroy": true,
    "duplicate": true,
    "favorite": true,
    "link_configuration": true,
    "invite_owner": true,
    "move": true,
    "partial_update": true,
    "restore": true,
    "retrieve": true,
    "media_auth": true,
    "link_select_options": {
      "restricted": [
        "reader",
        "editor"
      ],
      "authenticated": [
        "reader",
        "editor"
      ],
      "public": [
        "reader",
        "editor"
      ]
    },
    "tree": true,
    "update": true,
    "versions_destroy": true,
    "versions_list": true,
    "versions_retrieve": true
  },
  "content": "AUyjnPnrBgAIAShkb2MtMzljYWRhYWEtNGQ5Ni00MGYxLWI4NjQtNDkxNTU0ZGUwNTc0AnczYnJvYWRjYXN0OiBkb2MtMzljYWRhYWEtNGQ5Ni00MGYxLWI4NjQtNDkxNTU0ZGUwNTc0dzNicm9hZGNhc3Q6IGRvYy0zOWNhZGFhYS00ZDk2LTQwZjEtYjg2NC00OTE1NTRkZTA1NzQHAQ5kb2N1bWVudC1zdG9yZQMKYmxvY2tHcm91cAcAo5z56wYCAw5ibG9ja0NvbnRhaW5lcgcAo5z56wYDAwlwYXJhZ3JhcGgHAKOc+esGBAYEAKOc",
  "created_at": "2025-06-30T16:44:08.056098Z",
  "creator": "8a13e640-dc00-4b50-8379-dfb65841cdd7",
  "depth": 1,
  "excerpt": null,
  "is_favorite": true,
  "link_role": "reader",
  "link_reach": "restricted",
  "nb_accesses_ancestors": 1,
  "nb_accesses_direct": 1,
  "numchild": 0,
  "path": "000000o",
  "title": "🧪 test-editor0701-0045",
  "updated_at": "2025-06-30T16:45:01.247711Z",
  "user_roles": [
    "owner"
  ]
}
```

# more
