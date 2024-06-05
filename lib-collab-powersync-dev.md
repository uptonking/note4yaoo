---
title: lib-collab-powersync-dev
tags: [collaboration, powersync]
created: 2024-02-12T03:22:27.021Z
modified: 2024-02-12T03:22:45.261Z
---

# lib-collab-powersync-dev

# guide

- license
  - [PowerSync Licensing](https://www.powersync.com/legal/overview)
  - [PowerSync Pricing for open/enterprise edition](https://www.powersync.com/pricing)
# dev

# examples

- https://github.com/guillempuche/localfirst_react_server /202403/ts
  - React app using local-first web SQLite and cloud Postgres database Neon. 
  - Sync with PowerSync. Authentication via Stytch.
  - By leveraging PowerSync for local data management and integrating cloud database synchronization, this setup is also extendable to React Native applications. 
  - For database services, I use Neon. However, any Postgres provider is suitable.
  - PowerSync requires JWKS tokens for authentication. 
  - We use Stytch for authentication due to its compatibility with React and React Native, and its cost-effectiveness.
  - https://discord.com/channels/1138230179878154300/1176567090124165191/1218636496844886186
    - I finished a local-first React web demo _20240317
# more
