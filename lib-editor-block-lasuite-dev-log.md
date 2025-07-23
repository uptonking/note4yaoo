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

- ## login: "GET /api/v1.0/callback/?error=invalid_scope&error_description=Invalid+scopes%3A+%22openid+email%22&state=zGWy6oJBntayvzTeCbQXGGHjHtagTiou HTTP/1.1" 302 0 

- 在 common.local 中，设置 OIDC_RP_SCOPES=email ， 而不是 OIDC_RP_SCOPES="openid email", 但此时仍不可运行
  - 💡 🤔 最后可行的设置为 OIDC_RP_SCOPES=openid email

- Docker vs Local Environment Differences
  - Docker Compose `env_file` processing automatically handles quote stripping
  - Shell environment variable processing treats quotes as literal characters
  - Django's `values.Value()` doesn't strip quotes - it uses the raw environment value
  - This is a common gotcha when moving between Docker and local development environments!
