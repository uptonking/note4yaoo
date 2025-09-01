---
title: lib-aikit-librechat-docs
tags: [docs, librechat]
created: 2025-09-01T05:52:42.917Z
modified: 2025-09-01T05:52:50.865Z
---

# lib-aikit-librechat-docs

# guide

# overview

# docs-librechat

## mcp

- MCP servers can be configured to use different transport mechanisms:
- STDIO Servers
  - Work wells for local, single-user environments
  - Not scalable for remote or cloud deployments
- Server-Sent Events (SSE) Servers
  - Remote transport mechanism but not recommended for production environment
- Streamable HTTP Servers
  - Uses HTTP POST for sending messages and supports streaming responses
  - Supports both basic requests and streaming via Server-Sent Events (SSE)
  - More performant alternative to the legacy HTTP+SSE transport
  - Operates as an independent process that can handle multiple client connections
  - Supports proper multi-user server configurations
- For production environments, only MCP servers with “Streamable HTTP” transports are recommended. 
  - Unlike SSE which maintains long-running connections, Streamable HTTP offers stateless options that are better suited for scalable, multi-user deployments.

- 
- 

# docs-open-webui

# more
