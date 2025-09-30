---
title: lib-saas-filebrowser-community
tags: [cloud-drive, community, filebrowser]
created: 2025-09-30T08:58:10.657Z
modified: 2025-09-30T09:00:23.492Z
---

# lib-saas-filebrowser-community

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 
# discuss-roadmap
- ## 

- ## 

- ## [Stable Release & 0.9.0 update _202509](https://github.com/gtsteffaniak/filebrowser/discussions/1293)
  - A breakdown of some things to expect in 0.9.x:
  - jobs / async task
  - introduction of SQLite database: Initially, this will be primarily for job status information. eventually, this could enable RAM-free indexing and replace the existing simple (but very fast) database.

- ## [Investigate optimize for memory _202506](https://github.com/gtsteffaniak/filebrowser/issues/807)
  - Investigate and implement an option to index to the database instead of memory.

- The current database implementation (bolt) is incapable of supporting this feature. However, I could implement an SQLite temporary database to properly support a queryable database to accomplish this.

- in-memory indexing will still be ideal for `simple` and `normal` filesystem complexities, but many `complex` filesystems that require large memory footprints could take advantage of this.
# discuss-internals
- ## 

- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## 

- ## [Keycloak OIDC: 'failed to exchange token: oauth2: "invalid_grant" "Code not valid"' _202506](https://github.com/gtsteffaniak/filebrowser/issues/737)
- 本地keycloak异常日志 ERROR [org.keycloak.services] (executor-thread-6) KC-SERVICES0093: Invalid parameter value for: scope

- 💡 将配置`scopes: "email openid profile groups"`中groups去掉可登录
