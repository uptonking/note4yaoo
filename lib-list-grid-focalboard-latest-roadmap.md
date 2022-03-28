---
title: lib-list-grid-focalboard-latest-roadmap
tags: [focalboard, roadmap]
created: '2022-03-16T20:46:32.687Z'
modified: '2022-03-16T20:46:53.277Z'
---

# lib-list-grid-focalboard-latest-roadmap

# guide

# changelog
- merge permissions feature branch
  - commit 2022-03-22 aa540e73ce669a1acd491a5edd7d55199ef1b87c
  - [pr: Permissions feature branch](https://github.com/mattermost/focalboard/pull/2578)
# discuss

## [Feature Idea: Role-Based Permissions](https://github.com/mattermost/focalboard/issues/584)

- phase 1
  - add concept of "admin" and "non-admin" users; admin user is first to register with app
- phase 2
  - add sophisticated RBAC as per table above

- [Upcoming changes to the Mattermost Boards permission system](https://github.com/mattermost/focalboard/discussions/2436)
  - Currently in Mattermost Boards, access to each workspace is tied to a particular channel’s membership, and channel members have full edit access to all boards in that workspace.
  - We are working on changing this so that each board has independent permission settings. Roles can be set for each board: admins and editors to start with, and additional roles (e.g. viewers) coming later. This will remove the “workspace” concept entirely, and boards will be scoped to a team in Mattermost. In addition, boards can be made accessible to everyone in a team, with a default role
  - You’ll see the list of boards per team in the sidebar
  - These changes apply to Mattermost Boards. Personal Desktop and Personal/Development Server will continue to behave the same, with all users having edit access to boards in the system.

## [Feature Idea: Focalboard API](https://github.com/mattermost/focalboard/issues/1116)

- Right now, the current API is block-based (boards, cards, etc. are blocks with different types). 
  - We are open to input on how to refactor this in the future, but the current API is fully functional, and should be able to support the scenarios mentioned above.

## [Feature Request: Single page/wiki/note/folder without board](https://github.com/mattermost/focalboard/issues/166)

- Such pages would be really useful for high-level briefs and team documentation.
  - Markdown-like is fine but it would be great to have links between pages and cards as a first-class citizen. 
  - Having backlinks for instance would make things very useful.

## [Feature Idea: Auto-sync card with GitLab](https://github.com/mattermost/focalboard/issues/2597)

- It would be great to have a card be automatically created when an issue is created on a Github repo; 
  - and conversely, a Github issue be created when we create a card in MM.
