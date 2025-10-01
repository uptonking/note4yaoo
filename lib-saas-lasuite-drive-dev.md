---
title: lib-saas-lasuite-drive-dev
tags: [cloud-drive, lasuite-drive]
created: 2025-09-30T08:59:06.599Z
modified: 2025-09-30T08:59:30.846Z
---

# lib-saas-lasuite-drive-dev

# guide
- pros
  - license: MIT
  - Share files and folders with your team members

- cons
  - 未实现 usage quota

- features
  - Granular access control to ensure your information is secure and only shared with the right people
  - Create workspaces to organize team collaboration and manage shared resources

- tips
  - ?
# draft

# dev-xp

# devops

```shell
# start lasuite-docsdrive
source ./bin/dev-env.sh

MINIO_ROOT_USER=impress MINIO_ROOT_PASSWORD=password minio server --address :9090 --console-address :9001  /Users/yaoo/Documents/repos/saas/lasuite-drive/data/media

# mc alias set ALIAS URL ACCESSKEY SECRETKEY
mc alias set drive http://localhost:9090 impress password

cd ~/Documents/opt/compiled/keycloak &&  ./bin/kc.sh start-dev --features=preview --import-realm --hostname=http://localhost:8083 --hostname-strict=false --http-port=8088 --http-management-port=9037 --health-enabled=true --metrics-enabled=true --proxy-headers forwarded --db postgres --db-url-database keycloak_ladrive2510 --db-url-host localhost --db-username dinum --db-password pass --bootstrap-admin-username admin --bootstrap-admin-password admin

cd ./src/frontend/
yarn install

# webapp
cd ./src/frontend/apps/drive/
yarn dev

# backend - django
cd src/backend/
# 检查并注释掉 WOPI 相关的环境变量
uv sync --all-extras
# uv run python manage.py migrate
uv run python manage.py runserver 0.0.0.0:8071

```

# more
