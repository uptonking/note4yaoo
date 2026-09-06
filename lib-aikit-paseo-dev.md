---
title: lib-aikit-paseo-dev
tags: [agent, paseo]
created: 2026-09-05T00:27:22.306Z
modified: 2026-09-05T00:27:42.212Z
---

# lib-aikit-paseo-dev

# guide
- pros
  - license: apache2
  - remote control: local server, remote server
  - existing coding agents, use it  on your own device
  - Providers: Bring your own
  - plugins: add server-side functionality, modify the client with custom components
  - parallel work with optional git worktree: Per-worktree services. Each worktree gets allocated ports for dev servers and databases, 
  - automation: cli, mcp
  - Can I get banned for using Paseo? Paseo is designed to use each provider's officially supported integration and does not attempt to bypass its terms of service

- cons
  - Paseo manages other agents, it doesn't ship one.

- [features](https://paseo.sh/docs/why)
  - clients: The native mobile app has full feature parity with desktop.
  - integrations: GitHub, Slack, Discord
  - Voice runs locally on your device by default.
  - You can use the hosted relay (end-to-end encrypted, Paseo can't read your traffic), set up your own tunnel (Tailscale, Cloudflare Tunnel, etc.), or expose the daemon port directly. 

- tips
  - ?
# draft
- cowork/workbuddy-like
  - implement integrations for google-docs/msoffice like github/gitea

- sandbox

- paseo-relay server
  - ts, go

- 
- 
- 
- 
- 

- integrations
  - qq
  - telegram

- 
- 
- 
- 

# dev-xp

# more

# docs
- Paseo follows a client-server architecture, similar to Docker. 
  - The daemon runs on your machine and manages your coding agents. 
  - Clients (the mobile app, CLI, or web interface) connect to the daemon to monitor and control those agents.
- The Paseo daemon can run anywhere you want to execute agents: your laptop, a Mac Mini, a VPS, or a Docker container. 
- Clients connect to the daemon over WebSocket. There are two ways to establish this connection:
  - Relay connection (recommended), The daemon connects outbound to our relay server, and clients meet it there. No open ports required.
  - Direct connection, The daemon listens on a network address and clients connect directly.

- The Paseo CLI lets you manage agents from your terminal. It's the same interface exposed by the daemon's API, so anything you can do in the app you can do from the command line.
  - You can tell coding agents to use the Paseo CLI to spawn and manage other agents. 
  - CLI-created workers get the same workspace and parent defaults as MCP-created workers.
- The CLI is designed to be used by agents themselves. You can instruct an agent to spawn sub-agents for parallel work

- You'll also want the GitHub CLI (gh) installed and authenticated, Paseo uses it for PR-aware worktrees and a few orchestration features.

- Connectivity
  - SSH: SSH transport connects to an existing daemon through your local OpenSSH client.
  - Paseo relay: works without Tailscale, port forwarding, or network configuration
  - Tailscale: Install Tailscale on the daemon machine and your phone. Sign in to the same tailnet on both devices.

- Relay connections
  - The relay is the simplest way to connect from your phone. It requires no VPN setup, no port forwarding, and no firewall configuration. 
  - The daemon can stay bound to localhost or a socket file, it connects outbound to the relay, and your phone meets it there. 
  - The official relay server is the open-source Elixir service at getpaseo/paseo-relay.
  - The relay is designed to be untrusted. All traffic between your phone and daemon is end-to-end encrypted. The relay server cannot read your messages, see your code, or modify traffic without detection. Even if the relay is compromised, your data remains protected.
- Relay is off on new installations. 
  - Choosing not to enable relay leaves the daemon available for direct TCP, Tailscale, or other VPN connections and does not create a pairing QR code. 

- Direct connections
  - By default, the daemon listens on 127.0.0.1:6767 (localhost only). 
  - For maximum isolation, you can configure the daemon to listen on a Unix socket file instead of a TCP port. This prevents any network access entirely, only processes on the same machine can connect. The CLI supports this mode, but the mobile app and web interface require a network connection.

- The official Paseo Docker image runs the daemon and serves the bundled browser UI from the same HTTP origin. 
- The official Docker image runs the daemon and bundled web UI in one container. 
  - It binds to 0.0.0.0:6767 inside the container so Docker port publishing and reverse proxies work normally.

- 
- 
- 
- 
- 
- 
- 
- 
- 
