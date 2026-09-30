---
title: lib-aikit-skills-dev
tags: [agent-skills]
created: 2026-09-29T23:45:24.906Z
modified: 2026-09-29T23:45:32.152Z
---

# lib-aikit-skills-dev

# guide

# issues

# draft

# dev-xp

# skills-providers

## vercel [The Agent Skills Directory ](https://www.skills.sh/)

- npm-style registry-plus-leaderboard for SKILL.md files

- The `find-skill` CLI (on PyPI) doesn't replace skills.sh so much as search it alongside 13 other sources at once — it aggregates 4, 835 skills across 14 sources, ranked by trust score (GitHub stars × source priority), with skills.sh itself as the largest single source at nearly 4, 000 skills.

- https://github.com/vercel-labs/skills-handler /202601/ts
  - A framework-agnostic handler for serving Agent Skills via well-known URIs. 
  - Implements the Agent Skills Discovery specification.

- A static .well-known index is the most direct way to get npx skills add working against your own host. 
  - It follows an open Cloudflare RFC: you serve /.well-known/agent-skills/index.json listing each skill. 
  - The npx skills installer reads it when given your full https URL, and verifies a SHA-256 digest before installing.

- 
- 
- 

## [ClawHub ](https://clawhub.ai/)

- it uses vector-based semantic search on OpenAI embeddings so you can search in natural language instead of exact package names, and anyone with a week-old GitHub account can publish to it.

- 
- 
- 
- 
- 

## skills-hub-collections

- 讯飞 [Astron SkillHub ](https://skill.xfyun.cn/search)

- [Skills Directory - Secure, Verified Agent Skills for Claude AI ](https://www.skillsdirectory.com/)
  - Security-focused directories
  - 574, 698 indexed skills(202609)
  - runs every listed skill through automated scanning for prompt injection, credential theft, and data exfiltration before it shows up
  - SkillShield is a narrower, newer entrant doing something similar — a 4-layer analysis (manifest, static code, dependency, and LLM behavioral checks) producing 0–100 trust scores, though it's a much smaller, newer project.

- [localskills.sh · Share Agent Skills Across Your Team ](https://localskills.sh/)
  - Create, share, and install agent skills across Cursor, Claude Code, Windsurf...
  - SSO, SCIM, and team controls built in.

- 
- 
- 
- 
- 
- 
- 

# more
