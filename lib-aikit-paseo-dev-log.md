---
title: lib-aikit-paseo-dev-log
tags: [dev-log, paseo]
created: 2026-09-08T04:45:08.195Z
modified: 2026-09-08T04:45:17.635Z
---

# lib-aikit-paseo-dev-log

# guide

# devops
- locations
  - /opt/apps/llm-hub-lite/shared/data/prod/aichor/workspace

- Browser connection succeeds using host aichor.aichorage.de, port 443, SSL enabled.
# discuss-stars
- ## 

- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## 

- ## 

- ## 

- ## 

- ## 

- ## 

- ## where is location for "Search for directory" ?
- /workspace is the intended persistent project area. It survives Aichor/container/VPS restarts and is separate from Paseo’s internal state.
  - /opt/apps/llm-hub-lite/shared/data/prod/aichor → /home/paseo
  - /opt/apps/llm-hub-lite/shared/data/prod/aichor/workspace → /workspace
- Choose Add project → Search for directory
  - Enter the full container path: /workspace/my-project

- ## the hostname shows as 04226b5abf73 . is there any way to edit the connection info and change the host name to a semantic host name?
  - Do not enter wss:// or /ws in the Host field. The UI constructs the WebSocket URL itself. Entering a complete WebSocket URL there is what causes the Invalid URL error.

- ## When you select "Direct connection", you should NOT enter any host, port, or URL.
  - "Direct connection" means the UI will automatically connect to the same daemon that served the web page.
  - The form fields should be empty or grayed out.
  - "Direct connection" means "connect to the daemon that served this page" - it should be automatic.
  - The auto-detection is failing - it's falling back to ws://localhost:6767/ws instead of detecting wss://aichor.aichorage.de
- The problem is that your reverse proxy (Caddy) isn't forwarding the necessary headers.
