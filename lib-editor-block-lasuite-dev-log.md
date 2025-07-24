---
title: lib-editor-block-lasuite-dev-log
tags: [dev-log, lasuite-docs]
created: 2025-07-23T15:48:18.780Z
modified: 2025-07-23T15:48:28.642Z
---

# lib-editor-block-lasuite-dev-log

# guide

# discuss-stars
- ## 

- ## 

- ## 
# discuss-usage/tips
- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## 

- ## 

- ## 本地django-dev-server获取本地minio中的内容失败 An error occurred (502) when calling the GetObject operation (reached max retries: 4): Bad Gateway.
- ai帮着加了几个aws相关的环境变量
  - 实际最后是撤消了所有ai添加的变量，将localhost改为 127.0.0.1，然后正确 source bin/dev-env.sh 来设置环境变量解决

```sh
AWS_S3_ENDPOINT_URL=http://127.0.0.1:9000
# localhost not working, use 127.0.0.1
# AWS_S3_ENDPOINT_URL=http://localhost:9000
```

- localhost can resolve to both IPv4 (127.0.0.1) and IPv6 (::1) addresses
  - MinIO was listening on both IPv4 and IPv6, but there was likely a configuration or networking issue with the IPv6 stack.

- ## login: "GET /api/v1.0/callback/?error=invalid_scope&error_description=Invalid+scopes%3A+%22openid+email%22&state=zGWy6oJBntayvzTeCbQXGGHjHtagTiou HTTP/1.1" 302 0 

- 在 common.local 中，设置 OIDC_RP_SCOPES=email ， 而不是 OIDC_RP_SCOPES="openid email", 但此时仍不可运行
  - 💡 🤔 最后可行的设置为 OIDC_RP_SCOPES=openid email

- Docker vs Local Environment Differences
  - Docker Compose `env_file` processing automatically handles quote stripping
  - Shell environment variable processing treats quotes as literal characters
  - Django's `values.Value()` doesn't strip quotes - it uses the raw environment value
  - This is a common gotcha when moving between Docker and local development environments!
