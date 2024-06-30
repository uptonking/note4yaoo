---
title: lib-notb-jupyter-latest-roadmap
tags: [jupyter, roadmap]
created: 2024-06-30T04:30:08.639Z
modified: 2024-06-30T04:30:21.107Z
---

# lib-notb-jupyter-latest-roadmap

# guide

# roadmap

# more

# discuss
- ## 

- ## 

- ## [Towards a new generic and composable server · Issue · jupyter-server/team-compass _202109](https://github.com/jupyter-server/team-compass/issues/11)
- The current jupyter_server project started as a split of the backend parts of the notebook repository
- Tornado was one of the earliest Python web servers to support WebSockets, and provided a modern async programming model long before asyncio existed. It was adopted broadly in the Jupyter stack, so much that e.g. ipykernel and jupyter_client depend on Tornado…
- However, in my opinion, Tornado has become a liability:
  - The async constructs are a compatibility layer on top of asyncio. However, there are some tricky corner cases that make it not great to work with.
  - Several of the recent versions of Tornado broke Jupyter in subtle ways, and we've had to patch various Jupyter subprojects to accommodate new versions.
  - It is not so actively developed compared to alternatives.
- The kernel protocol over WebSocket is inefficient
  - while ZMQ messages are serialised in a well-specified sequence of blobs of bytes, the WebSocket protocol communicates this content as a JSON object with keys for header, content, metadata etc. 
  - A consequence of that design is that all messages have to be parsed so that we can recompose the ZMQ messages.
  - If the WebSocket messages contained the same binary blobs as the ZMQ messages, we could directly route them to the right kernel (simply adding ZMQ identities and delimiter)... Such an approach would result in a considerably faster handling of kernel messages.

- A proposal for a new server
  - Drop Tornado and reboot the Jupyter server project with a FastAPI-based solution.
  - Adopt the “everything is a plugin” approach of JupyterLab to the architecture

- 202207: Jupyverse and FPS generally embrace modern Python technologies such as ASGI, and an ecosystem built around uvicorn/Starlette/FastAPI, which we see as the future of web development. In the near future, Jupyverse may take a different path than JupyterHub for a multi-user scenario.
  - JupyterHub is basically a server of servers. Each individually spawned Jupyter server is quite independent. 
  - We might scale Jupyverse differently, so that it remains the only server.
