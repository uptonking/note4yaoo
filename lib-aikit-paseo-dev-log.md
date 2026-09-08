---
title: lib-aikit-paseo-dev-log
tags: [dev-log, paseo]
created: 2026-09-08T04:45:08.195Z
modified: 2026-09-08T04:45:17.635Z
---

# lib-aikit-paseo-dev-log

# guide

# discuss
- ## 

- ## 

- ## 

- ## 

- ## When you select "Direct connection", you should NOT enter any host, port, or URL.
  - "Direct connection" means the UI will automatically connect to the same daemon that served the web page.
  - "Direct connection" means "connect to the daemon that served this page" - it should be automatic.
  - The form fields should be empty or grayed out.
  - The auto-detection is failing - it's falling back to ws://localhost:6767/ws instead of detecting wss://aichor.aichorage.de
- The problem is that your reverse proxy (Caddy) isn't forwarding the necessary headers.
