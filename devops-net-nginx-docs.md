---
title: devops-net-nginx-docs
tags: [docs, network, nginx]
created: 2025-07-20T13:17:37.517Z
modified: 2025-07-20T13:18:12.842Z
---

# devops-net-nginx-docs

# guide

# dev-xp
- nginx-macos
  - Docroot is:  /opt/homebrew/var/www
  - config:  /opt/homebrew/etc/nginx/nginx.conf
  - nginx will load all files in /opt/homebrew/etc/nginx/servers/
  - brew services start nginx
  - 非后台启动 /opt/homebrew/opt/nginx/bin/nginx -g daemon\ off\
# overview

- 
- 
- 
- 
- 

- In nginx’s configuration language, directives live in well‑defined “contexts” (also called blocks), and the `server` context is not one of the top‑level (global) contexts. You can only place a `server { … }` block inside one of:` http/stream/mail`
  - a common nginx configuration pattern where the main `nginx.conf` file includes other configuration files, and those included files can contain just `server` blocks.
  - The `include` directive literally inserts the content of the included file
  - This modular approach makes configuration management much cleaner
  - Common include patterns:
    - include /etc/nginx/conf.d/*.conf; 
    - include /etc/nginx/sites-enabled/*;
    - include servers/*;

- in Nginx, you can define multiple `server` blocks that listen on different ports (like 8080, 8081, etc.) within the same `http` context. This allows you to serve different content or applications at URLs like: http://localhost:8080/ http://localhost:8081/
# config
- `proxy_pass` URL; 
  - Sets the protocol and address of a proxied server and an optional URI to which a location should be mapped.
  - If a domain name resolves to several addresses, all of them will be used in a round-robin fashion.
  - WebSocket proxying requires special configuration and is supported since version 1.3.13.

- `upstream` name { ... }
  - Defines a group of servers. Servers can listen on different ports. In addition, servers listening on TCP and UNIX-domain sockets can be mixed.
  - By default, requests are distributed between the servers using a weighted round-robin balancing method

- 
- 
- 
- 
- 
- 

# docs
- nginx has one master process and several worker processes. 
  - The main purpose of the master process is to read and evaluate configuration, and maintain worker processes. 
  - Worker processes do actual processing of requests. 
  - nginx employs event-based model and OS-dependent mechanisms to efficiently distribute requests among worker processes. 
  - The number of worker processes is defined in the configuration file and may be fixed for a given configuration or automatically adjusted to the number of available CPU cores

- 
- 
- 
- 
- 

# more
