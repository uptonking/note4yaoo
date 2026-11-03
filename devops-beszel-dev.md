---
title: devops-beszel-dev
tags: [beszel, devops]
created: 2026-08-28T17:47:21.904Z
modified: 2026-08-28T17:49:14.333Z
---

# devops-beszel-dev

> Lightweight server monitoring with historical data, docker stats, and alerts.

# guide
- pros
  - license: MIT
  - Lightweight: Smaller and less resource-intensive than leading solutions.
  - Automatic backups: Save to and restore from disk or S3-compatible storage.

- cons
  - ?

- features
  - Docker stats: Tracks CPU, memory, and network usage history for each container.
    - either use the Podman API or the Docker API, but not both at the same time.
  - GPU: monitor GPU usage, temperature, memory, and power draw for various GPU vendors and platforms.
  - Alerts: Configurable alerts for CPU, memory, disk, bandwidth, temperature, fan speed, load average, and status.
    - Notifications in Beszel are defined using Shoutrrr URL schemas.
  - Multi-user: Users manage their own systems. Admins can share systems across users.
  - OAuth / OIDC: Supports many OAuth2 providers. Password auth can be disabled.
  - S. M. A. R. T.: Disk health data and notifications on drive failure.
    - Beszel parses S.M.A.R.T. data from `smartctl` . On Linux, Beszel also reports eMMC wear/EOL indicators and mdraid array health.
  - REST API: Use or update your data in your own scripts and applications.
  - Additional Disks: use Beszel to monitor disks, partitions, or remote mounts.

- tips
  - ?
# draft

- 
- 

- 
- 

- theming
  - 类似cf探针的样式， 如 https://tzdd.66655888.xyz
# dev-xp

# more

# docs-beszel

## overview

- Beszel consists of two main components: the hub and the agent.
  - Hub: A web application built on `PocketBase` that provides a dashboard for viewing and managing connected systems.
  - Agent: Runs on each system you want to monitor and communicates system metrics to the hub.

- Beszel can send periodic outbound pings to an external monitoring endpoint (e.g., BetterStack, Uptime Kuma, Healthchecks.io). This allows you to monitor the health of your Beszel instance and the systems it tracks without exposing the hub to the internet.

- 
- 
- 
- 
- 

## docs

- Connecting hub and agent on the same system using Docker
  - When connecting to a local agent, localhost will not work because the containers are in different networks. The recommended way to connect them is to use a unix socket.

- Beszel uses a scratch image with no shell. This means you can't use `docker exec -it <container> /bin/sh` to debug from inside the container.
  - However, you can use the build option with a custom Dockerfile to move the binary into the base image of your choice.

- 
- 
- 
- 
- 

- Beszel uses PocketBase for user management. It is important to understand that regular user accounts and PocketBase superuser accounts are entirely separate.

- The agent collects data for systemd services that have been active at least once (including failed or exited ones), showing: Service status (active, inactive, failed, etc.), CPU and memory usage

- Beszel can be served behind a reverse proxy. The reverse proxy should be configured to proxy WebSocket connections in order for agents setup with a universal token to connect to the hub.

- Why host network mode?
  - The agent must use host network mode to access the host's network interface stats. This automatically exposes the port
  - If you don't need host network stats, you can remove that line from the compose file and map the port manually.
