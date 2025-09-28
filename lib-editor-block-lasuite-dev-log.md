---
title: lib-editor-block-lasuite-dev-log
tags: [dev-log, lasuite-docs]
created: 2025-07-23T15:48:18.780Z
modified: 2025-07-23T15:48:28.642Z
---

# lib-editor-block-lasuite-dev-log

# guide

# ai-prompts

```md
- the architecture of this project is here `docs/architecture.md`
- i run most services/modules of project locally instead of from docker.
  - run nextjs frontend from `src/frontend/apps/impress`, it's at http://localhost:3000/
  - run django backend from `src/backend`, api swagger is at http://localhost:8071/api/v1.0/swagger.json
  - postgresql/redis/minio/nginx is all start locally
- only keycloak OIDC service is started from docker by `docker compose -f compose.yml up -d keycloak`, it's at http://localhost:8080/ ,also at http://localhost:8083/(because nginx forwarded) 

- Problem: 
- Problem: 
```

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

- ## ❓ 使用authentik登录时, 从主页跳转到登录页的请求为  "GET /api/v1.0/authenticate/ HTTP/1.1" 302 0 (keycloak登录时日志也是这个)

- lasuite-docs后端正常登录时的请求为
  - /api/v1.0/callback/?state=jsscAcf2x7b25prCoPIrQQcZb2V2Y5Eq&session_state=99cd15f8-f891-4d82-a5cb-47e2146673ec&iss=http%3A%2F%2Flocalhost%3A8083%2Frealms%2Fimpress&code=f21c993f-22ba-41e9-9674-b17d180ce737.99cd15f8-f891-4d82-a5cb-47e2146673ec.869481d0-5774-4e64-bc30-fedc7c58958f HTTP/1.1

- authentik异常的日志为
  - The request fails due to a missing, invalid, or mismatching redirection URI (redirect_uri). [authentik.providers.oauth2.views.authorize] auth_via=unauthenticated cause=redirect_uri_no_match domain_url=localhost host=localhost:9000 pid=9615 request_id=ef442b8797b1443ea6731283404b6d8c schema_name=public
  - HTTP GET /application/o/authorize/?response_type=code&scope=openid+email&client_id=DyADizAP1Q5rlDqNqeBbzRgLFI5GpujpahrbkxgA&redirect_uri=http%3A%2F%2Flocalhost%3A8071%2Fapi%2Fv1.0%2Fcallback%2F&state=IPGmFHqvq7c7WclpdbYKnr18i62ck5jU&acr_values=eidas1&nonce=UGK75ddeexQ3ryeBHj6Co6pWOnKrz6R2 400 [0.04, 127.0.0.1:53032] [django.channels.server]

- 有个疑问，keycloak登录的url为 http://localhost:8083/realms/impress/protocol/openid-connect/auth?response_type=code&scope=openid+email&client_id=impress&redirect_uri=http%3A%2F%2Flocalhost%3A8071%2Fapi%2Fv1.0%2Fcallback%2F&state=jHa4OitdbWHfEV6uao3ehuL5gHHoDJzu&acr_values=eidas1&nonce=otplOUD0GDEynkHomSLDdV9A0GOKBdFF
  - 而authentik登录的url为 http://localhost:9000/application/o/authorize/?response_type=code&scope=openid+email&client_id=orgK14kskvU9UCETRbaqKE6kMCeR211uC4hRKFe4&redirect_uri=http%3A%2F%2Flocalhost%3A8071%2Fapi%2Fv1.0%2Fcallback%2F&state=T3RYXqrc6APnys1wMgeWNDaC8jwXjfgJ&acr_values=eidas1&nonce=hbcoG328CA9iNhkxeL6dnYeJP2KQJkIq
    - 为什么不是8083端口而是9000

- [Grafana Redirect URI Error · Issue · goauthentik/authentik _202402](https://github.com/goauthentik/authentik/issues/8673)
  - I suspect that Grafana is being operated behind a reverse proxy. If that's the case, you should update the Grafana container by adding the following environment variable `GF_SERVER_ROOT_URL: "https://grafana.domain.com"`

- ## Problem: my login is auto invalidated every day, so I have to login every day. is there any environment variables to configure the login token time limit? 
  - maybe you have to read keycloak documentation https://www.keycloak.org/documentation.html

- Looking at the Keycloak realm configuration, I can see the current token timeout settings:
  - "ssoSessionIdleTimeout": 1800 (30 minutes)
  - "ssoSessionMaxLifespan": 36000 (10 hours)
- If you prefer to configure this via environment variables instead of modifying the realm file, you can also set these in your Keycloak container environment.

- I also noticed in your Django settings that you have:
  - SESSION_COOKIE_AGE = values. PositiveIntegerValue( default=60 * 60 * 12, environ_name="SESSION_COOKIE_AGE", environ_prefix=None ) // 12h
  - SESSION_COOKIE_AGE=604800  # 7 days
  - ensures both `Keycloak` and `Django` sessions have compatible timeouts.

- ## 本地django-dev-server获取本地minio中的内容失败 An error occurred (502) when calling the GetObject operation (reached max retries: 4): Bad Gateway. _20250725
- ai帮着加了几个aws相关的环境变量
  - 实际最后是撤消了所有ai添加的变量，将localhost改为 127.0.0.1，然后正确 source bin/dev-env.sh 来设置环境变量解决

```sh
AWS_S3_ENDPOINT_URL=http://127.0.0.1:9000
# localhost not working, use 127.0.0.1
# AWS_S3_ENDPOINT_URL=http://localhost:9000
```

- localhost can resolve to both IPv4 (127.0.0.1) and IPv6 (::1) addresses
  - MinIO was listening on both IPv4 and IPv6, but there was likely a configuration or networking issue with the IPv6 stack.

- ### 🆕0726 prosemirror编辑器内图片的url未正常显示图片
- 图片url通过nginx转发到minio，转发时 需要将 `proxy_pass http://localhost:9000/impress-media-storage/;` 改为 `proxy_pass http://127.0.0.1:9000/impress-media-storage/; `

- ## login: "GET /api/v1.0/callback/?error=invalid_scope&error_description=Invalid+scopes%3A+%22openid+email%22&state=zGWy6oJBntayvzTeCbQXGGHjHtagTiou HTTP/1.1" 302 0 

- 在 common.local 中，设置 OIDC_RP_SCOPES=email ， 而不是 OIDC_RP_SCOPES="openid email", 但此时仍不可运行
  - 💡 🤔 最后可行的设置为 OIDC_RP_SCOPES=openid email

- Docker vs Local Environment Differences
  - Docker Compose `env_file` processing automatically handles quote stripping
  - Shell environment variable processing treats quotes as literal characters
  - Django's `values.Value()` doesn't strip quotes - it uses the raw environment value
  - This is a common gotcha when moving between Docker and local development environments!
