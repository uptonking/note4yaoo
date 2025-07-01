---
title: lib-editor-blocknote-dev
tags: [block-editor, blocknote, notion-like, prosemirror, tiptap-editor]
created: 2022-10-21T21:01:26.654Z
modified: 2023-02-05T19:03:27.729Z
---

# lib-editor-blocknote-dev

# guide

- pros-BlockNote

- cons-BlockNote

- pros-SuiteDocs
  - version-history
  - collab

- cons-SuiteDocs
  - 本地开发的环境配置过于复杂
  - 编辑器标题按enter回车键时光标不会自动进入内容区
# draft

# dev-xp

# more

# suite-docs

- features
  - pin docs
  - doc-toc

- editor
  - slash-menu /
# suite-docs-draft
- ❓
  - 分析文章内容数据持久化在哪里了，impress_document 这张表似乎没有具体内容
  - 不同的浏览器打开时，存在数据不一致的情况

- 使用简化版的oidc替代keycloak
# suite-docs-dev-xp

# suite-docs-codebase
- urls
  - webapp http://localhost:3000/
  - admin http://localhost:8071/admin
    - user: admin@example.com ,  pass: admin

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
  "content": "AUyjnPnrBgAIAShkb2MtMzljYWRhYWEtNGQ5Ni00MGYxLWI4NjQtNDkxNTU0ZGUwNTc0AnczYnJvYWRjYXN0OiBkb2MtMzljYWRhYWEtNGQ5Ni00MGYxLWI4NjQtNDkxNTU0ZGUwNTc0dzNicm9hZGNhc3Q6IGRvYy0zOWNhZGFhYS00ZDk2LTQwZjEtYjg2NC00OTE1NTRkZTA1NzQHAQ5kb2N1bWVudC1zdG9yZQMKYmxvY2tHcm91cAcAo5z56wYCAw5ibG9ja0NvbnRhaW5lcgcAo5z56wYDAwlwYXJhZ3JhcGgHAKOc+esGBAYEAKOc+esGBQEjKACjnPnrBgQNdGV4dEFsaWdubWVudAF3BGxlZnQoAKOc+esGAwJpZAF3DmluaXRpYWxCbG9ja0lkKACjnPnrBgMJdGV4dENvbG9yAXcHZGVmYXVsdCgAo5z56wYDD2JhY2tncm91bmRDb2xvcgF3B2RlZmF1bHSHo5z56wYDAw5ibG9ja0NvbnRhaW5lcgcAo5z56wYLAwlwYXJhZ3JhcGgoAKOc+esGDA10ZXh0QWxpZ25tZW50AXcEbGVmdCgAo5z56wYLAmlkAXckYWE3ZTM1MjctODhjMy00ZDlhLWIwNDEtNDE1N2ZjY2I5ODY5KACjnPnrBgsJdGV4dENvbG9yAXcHZGVmYXVsdCgAo5z56wYLD2JhY2tncm91bmRDb2xvcgF3B2RlZmF1bHRHo5z56wYEAwdoZWFkaW5nKACjnPnrBhENdGV4dEFsaWdubWVudAF3BGxlZnQoAKOc+esGEQVsZXZlbAF9ASgAo5z56wYRDGlzVG9nZ2xlYWJsZQF5BwCjnPnrBhEGBACjnPnrBhUFcmljaC2Eo5z56wYaBHRleHSEo5z56wYeBmVkaXRvcsejnPnrBgOjnPnrBgsDDmJsb2NrQ29udGFpbmVyBwCjnPnrBiUDCXBhcmFncmFwaCgAo5z56wYmDXRleHRBbGlnbm1lbnQBdwRsZWZ0KACjnPnrBiUCaWQBdyQ3ZjI4ODk2Yi0wZTA5LTRkMzAtOWYyMC04ZmI5OTg0NDkwMTkoAKOc+esGJQl0ZXh0Q29sb3IBdwdkZWZhdWx0KACjnPnrBiUPYmFja2dyb3VuZENvbG9yAXcHZGVmYXVsdMejnPnrBiWjnPnrBgsDDmJsb2NrQ29udGFpbmVyBwCjnPnrBisDCXBhcmFncmFwaCgAo5z56wYsDXRleHRBbGlnbm1lbnQBdwRsZWZ0KACjnPnrBisCaWQBdyRkYWQ2NjA1MS1lZGZkLTQ4NGItOWM2Yy05YmI4ODFiYWE1MDAoAKOc+esGKwl0ZXh0Q29sb3IBdwdkZWZhdWx0KACjnPnrBisPYmFja2dyb3VuZENvbG9yAXcHZGVmYXVsdAcAo5z56wYsBgQAo5z56wYxASNHo5z56wYsAwdoZWFkaW5nKACjnPnrBjMNdGV4dEFsaWdubWVudAF3BGxlZnQoAKOc+esGMwVsZXZlbAF9ASgAo5z56wYzDGlzVG9nZ2xlYWJsZQF5BwCjnPnrBjMGBACjnPnrBjcFdGFibGXHo5z56wYro5z56wYLAw5ibG9ja0NvbnRhaW5lcgcAo5z56wY9AwlwYXJhZ3JhcGgoAKOc+esGPg10ZXh0QWxpZ25tZW50AXcEbGVmdCgAo5z56wY9AmlkAXckNmU2MDQzZjAtOWVlMS00YWZmLTk1OTItYmNjM2MzNTBmMjZkKACjnPnrBj0JdGV4dENvbG9yAXcHZGVmYXVsdCgAo5z56wY9D2JhY2tncm91bmRDb2xvcgF3B2RlZmF1bHTHo5z56wY9o5z56wYLAw5ibG9ja0NvbnRhaW5lcgcAo5z56wZDAwlwYXJhZ3JhcGgoAKOc+esGRA10ZXh0QWxpZ25tZW50AXcEbGVmdCgAo5z56wZDAmlkAXckZGJhZDM0YTItZjkyOC00NDgyLThhZTktM2U0MWFjMWVkYWFiKACjnPnrBkMJdGV4dENvbG9yAXcHZGVmYXVsdCgAo5z56wZDD2JhY2tncm91bmRDb2xvcgF3B2RlZmF1bHQHAKOc+esGRAYEAKOc+esGSQEjR6Oc+esGRAMHaGVhZGluZygAo5z56wZLDXRleHRBbGlnbm1lbnQBdwRsZWZ0KACjnPnrBksFbGV2ZWwBfQEoAKOc+esGSwxpc1RvZ2dsZWFibGUBeQcAo5z56wZLBgQAo5z56wZPBWltYWdlx6Oc+esGQ6Oc+esGCwMOYmxvY2tDb250YWluZXIHAKOc+esGVQMJcGFyYWdyYXBoKACjnPnrBlYNdGV4dEFsaWdubWVudAF3BGxlZnQoAKOc+esGVQJpZAF3JGE0MmRmYTE4LTIwODktNGQyMi04NDBmLWYzNmExZTAxOTJlYigAo5z56wZVCXRleHRDb2xvcgF3B2RlZmF1bHQoAKOc+esGVQ9iYWNrZ3JvdW5kQ29sb3IBdwdkZWZhdWx0x6Oc+esGVaOc+esGCwMOYmxvY2tDb250YWluZXIHAKOc+esGWwMJcGFyYWdyYXBoKACjnPnrBlwNdGV4dEFsaWdubWVudAF3BGxlZnQoAKOc+esGWwJpZAF3JGZmMWNjZjU5LWM1ODUtNDk3Ni1hM2FjLTc5ZGMwYTM1YTFiZSgAo5z56wZbCXRleHRDb2xvcgF3B2RlZmF1bHQoAKOc+esGWw9iYWNrZ3JvdW5kQ29sb3IBdwdkZWZhdWx0AaOc+esGBgQEGwQsAjECRAJJAg==",
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

# suite-docs-documentation
- [La Suite Docs – System & Requirements](https://github.com/suitenumerique/docs/blob/main/docs/system-requirements.md)
  - RAM – start at 8 GB dev / 16 GB staging / 32 GB prod. Postgres and Keycloak are the first to OOM; scale them first.
  - Frontend: Uses pre-built Next.js static assets served by Nginx (no Node.js runtime needed)
  - Object Storage: External services (S3, Azure Blob) or self-hosted solutions (MinIO) are both viable
  - Scaling: Horizontal scaling is recommended for Django API and Y-Provider services
# more-suite-docs
