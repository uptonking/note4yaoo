---
title: lib-aikit-skills-examples
tags: [agent-skills, examples]
created: 2026-09-29T23:48:12.963Z
modified: 2026-09-29T23:48:33.701Z
---

# lib-aikit-skills-examples

# popular

# vendors-skills

# skills-hub

- https://github.com/openclaw/clawhub /9.5kStar/MIT/202609/ts
  - https://clawhub.ai/
  - Skill + Plugin Registry for OpenClaw
  - publish, version, and search text-based agent skills (a SKILL.md plus supporting files). 
  - It's designed for fast browsing + a CLI-friendly API, with moderation hooks and vector search. 
  - It also exposes a native OpenClaw package catalog for code plugins, bundle plugins
  - Web app: TanStack Start (React, Vite/Nitro).
  - Backend: Convex (DB + file storage + HTTP actions) + Convex Auth (GitHub OAuth).
  - Search: OpenAI embeddings (text-embedding-3-small) + Convex vector search.
  - The dependencies are the catch: Convex for the backend, GitHub OAuth for login, and OpenAI embeddings for search. it isn't fully offline because of the OpenAI dependency. 

- https://github.com/iflytek/skillhub /5.2kStar/apache2/202609/java/ts
  - https://skill.xfyun.cn/
  - Self-hosted, open-source agent skill registry for enterprises. 
  - Publish & version skill packages, govern with RBAC and audit logs, deploy on-premise with Docker or Kubernetes.
  - Spring Boot + React, backed by Postgres/Redis/S3, deployable via docker

- https://github.com/skael-dev/skael /apache2/202609/go/ts/astro
  - https://skael.dev/
  - One registry for your team's AI skills — across every agent and every project.
  - Why not just a git repo?  git folder gives you a folder. It doesn't place skills into Cursor and Codex and OpenCode, doesn't sync across machines
  - Skael is the layer that turns a folder of markdown into managed infrastructure — and unlike Claude's native org sharing (Claude.ai/Desktop, paid tiers only), it's vendor-neutral across every agent your team runs.
  - skael add picks what you want, skael sync keeps them up to date. There's no "sync everything" default; your ~/.skael/config.json tracks exactly which skills you've chosen to install (like package.json). 
  - score contest runs candidates against one suite, in one job, on one panel, on the same day. A skill only gets scored if it has a registered evaluation suite
  - Auto-sync hooks run skael sync in the background with 30-minute debouncing so your agents always have the latest versions 
  - Every install lands in one of two places: user scope puts a skill in your home directory, available to you in every project on that machine. Project scope puts it inside the current repo, so anyone who checks out that repo and runs skael sync gets it too. The default is project. 
  - Single Go binary embeds the API server and a React dashboard (served from the same process). Backed by Postgres for skill metadata, full-text search, and activation events. 
  - Skill archives stored on local filesystem or S3-compatible object storage.
  - Ownership rules decide who may publish to a skill name
  - whetstone: authoring and linting skills

- https://github.com/luna-prompts/skillnote /MIT/202609/python/ts
  - https://www.lunaprompts.com/
  - The open-source skill registry for AI coding agents. Create, manage, and distribute SKILL.md files across Openclaw, Claude Code, Cursor, Codex, OpenHands, Antigravity, and more.
  - Self-host your team's SKILL.md library. Version it, scope it, and ship it to Claude Code and OpenClaw from one CLI.

- https://github.com/lynnzc/skify /apache2/202603/ts
  - skify is a private skill registry you can deploy in minutes. 
  - Host your own skill packages for AI coding agents — keep proprietary workflows private, ensure team consistency, and maintain full control.
  - One-click deploy	Cloudflare Workers (free) or Docker
  - Full registry	Publish, version, search, and install skills
  - CLI	npx skify add/publish/sync
  - Web UI	Browse and search skills visually

- https://github.com/runkids/skillshare /2.7kStar/MIT/202609/go/ts
  - https://skillshare.runkids.cc/
  - One source of truth for AI CLI skills, agents, rules, commands & more. 
  - Sync everywhere with one command — from personal to organization-wide.
  - One source, every agent — sync to Claude, Cursor, Codex & 60+ more with skillshare sync
  - More than skills — manage rules, commands, prompts & any file-based resource with extras
  - If what you actually want is to avoid depending on Vercel's index rather than to run a registry, this sidesteps the question entirely: it's a single binary that treats any git host — including your own self-hosted GitLab/Gitea/Codeberg — as the source of truth, with bidirectional sync and its own local security-audit engine. No web UI or leaderboard, just CLI.

- https://github.com/netclaw-dev/skill-server /apache2/202607/csharp
  - A self-hosted skill server that provides versioned skill feeds for use by agents.
# utils

# more
