---
title: lib-editor-block-lasuite-codebase
tags: [codebase, lasuite-docs]
created: 2025-07-17T14:40:19.493Z
modified: 2025-07-17T14:40:30.038Z
---

# lib-editor-block-lasuite-codebase

# guide

- urls
  - webapp http://localhost:3000/
  - admin http://localhost:8071/admin
    - user: admin@example.com ,  pass: admin
  - django-api http://localhost:8071/api/v1.0/swagger.json

- make-bootstrap
  - pre-bootstrap: @touch env.d/development, @mkdir -p data/media
  - build: fe, be, yjs-provider
  - post-bootstrap:
    - migrate: uv run python manage.py migrate
    - resetdb: 
      - uv run python manage.py flush --no-input
      - uv run python manage.py createsuperuser --email admin@example.com --password admin
    - demo: uv run python manage.py create_demo 
    - back-i18n-compile:: uv run python manage.py compilemessages --ignore=".venv/**/*"
  - run: fe, django-be, yjs-provider, nginx

```shell
# start lasuite-docs
source ./bin/dev-env.sh

docker compose up -d keycloak
brew services start nginx
brew services start postgresql@17
brew services start redis

MINIO_ROOT_USER=impress MINIO_ROOT_PASSWORD=password minio server --console-address :9001  /Users/yaoo/Documents/repos/saas/lasuite-docs/data/media

mc alias set impress http://localhost:9000 impress password 

# webapp
cd ./src/frontend/apps/impress/
yarn dev

# collab
cd src/frontend/servers/y-provider/
yarn dev

# backend - django
cd src/backend/
uv sync --all-extras
uv run python manage.py runserver 0.0.0.0:8071

uv run celery -A impress.celery_app worker -l DEBUG

# stop-services
brew services stop --all
```

- keycloak
  - 登录时前端会location.replace http://localhost:8071/api/v1.0/authenticate
  - 接着django-lasuite会redirect到 http://localhost:8083/realms/impress/protocol/openid-connect/auth

- services(14)
  - django-celery-dev
    - app-dev-8071
      - postgresql16-15432
      - redis-6371
      - mailcatcher-1081
      - createbuckets
        - minio-9000/9001
  - y-provider-4444
  - nginx-8083 还转发路由 /media/, /media-auth
    - keycloak-8080 转发
      - kc_postgresql14-5433
  - frontend-dev-3000, node, crowdin
# overview

# frontend

# backend

## content

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

## version-history

- 👉 获取版本历史列表 /api/v1.0/documents/1150f3fb-9d1c-445f-a984-12a156b67a06/versions/?version_id=
  - 若版本很多，滚动时会拉取更多旧版本，此时api默认会变为如 ?version_id=1c7e8f4d-540a-4001-acc9-701586c8ec01
  - `get_versions_slice`: Get document versions from object storage with pagination and starting conditions
  - default_storage.connection.meta.client.list_object_versions(bucket, file_key, maxSize)
    - 这里涉及django-storages和boto3的api
    - https://github.com/jschneier/django-storages/blob/master/storages/backends/s3.py

- every call to `storage.save("reports/quarterly.pdf", …)` creates a new immutable version rather than overwriting.
  - 实际保存多版本执行的是 obj.upload_fileobj(content, ExtraArgs=params, Config=self.transfer_config)

- 👉 获取某个版本的内容 /api/v1.0/documents/1150f3fb-9d1c-445f-a984-12a156b67a06/versions/6cf08154-3041-4c3c-861b-5fe7a5834821/
  - 实际执行 default_storage.connection.meta.client.get_object(**params)
  - params参数包括 Bucket, file_key, VersionId
# more
