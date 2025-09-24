---
title: lib-saas-authentik-dev
tags: [auth, authentik]
created: 2025-09-23T13:06:53.251Z
modified: 2025-09-23T13:07:14.156Z
---

# lib-saas-authentik-dev

# guide

- pros
  - integrations: HedgeDoc, Kanboard, Mastodon, Nextcloud/owncloud, Wekan, Zulip, AppFlowy, OnlyOffice, BookStack, DokuWiki, Outline, Paperless-ngx, Wiki.js, Calibre-Web, Immich, Jellyfin, Seafile, Open WebUI, librechat, Grafana, Zoho
    - Coder, gitea, gitlab, Jenkins, MinIO, pgAdmin, RustDesk Server, Tailscale, PocketBase
    - Stripe, WordPress, 1Password, Linkwarden, Bitwarden

- cons
  - 核心功能是sso, 偏向于后端逻辑及账户管理, 在前端交互功能及定制很弱
  - 定制复杂度较高，缺少示例
  - logout退出登陆的逻辑及ui都很难定制

- features
  - Read Replicas: You can configure additional read replica databases to distribute database load and improve performance.
# draft
- authentik + lasuite-docs?

- ❓ how to register user on custom webapp?
# dev-xp
- authentik + gitea
  - gitea退出登陆后，无法切换用户登录，会以刚才的用户自动登录

- authentik + outline
  - outline退出后能跳转到authentik账户提示页，可以切换用户

- 实测github oauth支持测试localhost地址
  - 之前登录失败的callback URL配置为 http://localhost:9000/source/oauth/callback/github, 可正常登录的URL为 http://localhost:9000/source/oauth/callback/github2509, 需要查看idp的配置

- ✅ authentic + librechat: [LibreChat + Authentik](https://www.librechat.ai/docs/configuration/authentication/OAuth2-OIDC/authentik)
# devops
- [Full development environment](https://docs.goauthentik.io/developer-docs/setup/full-dev-environment/)
-[Configuration | authentik](https://docs.goauthentik.io/install-config/configuration/)

```shell
# Install the required native dependencies 
brew install  libxmlsec1 libpq krb5 pkg-config  golangci-lint

make node-install
make core-install

# uv run scripts/generate_config.py
make gen-dev-config

# -- createdb testdb, createdb is a command line utility
CREATE DATABASE authentik;

make migrate
# Generate the required schema files and TypeScript client
make gen

make web-watch

go mod download

make run-server
make run-worker
```

- frontend: http://localhost:9000/
  - https://localhost:9443/
# codebase

# integrations

- [Questions about self-hosted grist and authentik with OIDC - Ask for Help - Grist Creators _202406](https://community.getgrist.com/t/questions-about-self-hosted-grist-and-authentik-with-oidc/5250)

- [Nextcloud and OpenCloud : r/selfhosted](https://www.reddit.com/r/selfhosted/comments/1lrmj17/nextcloud_and_opencloud/)
  - I also have OpenCloud working with Authentik. Their documentation needs a lot of work and some of their integration variables/setup are a mess, but it does work if you're patient and persistent
# more
- [immich SSO with Authentik - DEV Community _202404](https://dev.to/rzumbado/immich-sso-with-authentik-2gi9)
  - a quick tutorial to help setting up immich single sign on (SSO) with authentik.
  - for this tutorial I will only focus on integrating them both for your convenience AFTER they are up and running.
  - https://github.com/rzumbado/immich-authentik-sample

- [Moving to our own authentication server | Nexirift Blog _202502](https://blog.nexirift.com/blog/moving-to-our-own-authentication-server)
  - During our development of the core Nexirift project's Nova API server, we encountered significant limitations when working with authentication services like Keycloak and Authentik. 
  - These providers offered insufficient control over data and event flows to our API, forcing us to implement workarounds and additional processing layers that added unnecessary complexity 
  - Problems that were encountered during the development of the Nova API server included:
    - Missing the ability to control user settings: Authentik did not provide a way to set user settings via a different server, such as the API or mobile app. This meant that we would have to redirect the end user to the Authentik settings page every time they wanted to change any of their user settings.
    - User data was not synchronized between services: The API server did not have access to the user data stored in Authentik, which meant that we had to use Authentik webhooks to synchronize Authentik data to the API. This added complexity to our codebase and meant that data may not be up-to-date in the API.
    - No way to implement user setting endpoints: Since we had no way of changing user settings without redirecting, there was no way for us to implement an endpoint on the API server that would allow developers to update user settings, this would require developers to use the Authentik API for user settings.
  - Since we have encountered all of these problems while building the API server, we have decided to migrate to a custom authentication server solution. 
  - Due to these new changes in our infrastructure, we are no longer using the Nexirift plugin-oidc package and have built a new one called plugin-better-auth.

- [Authentik 教程系列：简介和安装配置 - ECWU's Notebook](https://ecwuuuuu.com/post/authentik-tutorial-1-introduction-and-install/)
  - 当我们这些自部署的服务越来越多，去访问每一个服务都需要单独的账号和密码；如果用户不止你一人，多账号管理也会成为一个麻烦的事情。
  - 一种可行的方案是部署一个统一登录服务（SSO）。我们可以将部署的各种应用进行接入。那么当用户需要使用时，不再是在应用内进行登录，而是会被跳转到这个统一登录服务中，进行登录和鉴权
  - 通过这个统一登陆服务，你就可以实现一个账号访问所有接入的应用。而且也可以很方便的去管理或者创建新的用户，去控制每一个用户具体的权限。
  - [Authentik 视频教程 - 合集 _202408](https://ecwuuuuu.com/post/authentik-tutorial-video/)

- [authentik: Authentication, SSO, User Management & Password Reset for Home Networks](https://helgeklein.com/blog/authentik-authentication-sso-user-management-password-reset-for-home-networks/)
