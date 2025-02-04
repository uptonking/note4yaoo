---
title: lib-excel-focalboard-latest-roadmap
tags: [focalboard, roadmap]
created: 2022-03-16T20:46:32.687Z
modified: 2022-08-21T09:57:10.547Z
---

# lib-excel-focalboard-latest-roadmap

# guide

# changelog
- merge permissions feature branch
  - commit 20220322 aa540e73ce669a1acd491a5edd7d55199ef1b87c
  - [pr: Permissions feature branch](https://github.com/mattermost/focalboard/pull/2578)

- [Adding the new blocks based editor_20221115](https://github.com/mattermost/focalboard/pull/3825)
  - webapp/src/components/blocksEditor/blocksEditor.tsx
  - 仍然基于draftjs
  - This adds the new blocks based editor behind a feature flag.
  - it supports, drag and drop, different block types (h1, h2, h3, video, attachment, images, dividers, list items, checkboxes and quotes)
# discuss

## [Time tracking](https://github.com/mattermost/focalboard/discussions/207)

- I'd like to add that this kind of feature shall be accompanied with expenses, as both are used to track the money spent on any project.

- [Would a time tracking feature fit the projects vision?](https://github.com/mattermost/focalboard/discussions/874)

- [Feature Idea: Task time tracking](https://github.com/mattermost/focalboard/issues/1982)
  - I was expecting something like YouTrack has: allow setting Estimate (estimate time to finish a task) and Time Spend. 

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

- [The state of the APIs, and changes coming_202201](https://github.com/mattermost/focalboard/discussions/2139)

## [Feature Request: Single page/wiki/note/folder without board](https://github.com/mattermost/focalboard/issues/166)

- Such pages would be really useful for high-level briefs and team documentation.
  - Markdown-like is fine but it would be great to have links between pages and cards as a first-class citizen. 
  - Having backlinks for instance would make things very useful.

## [Feature Idea: Auto-sync card with GitLab](https://github.com/mattermost/focalboard/issues/2597)

- It would be great to have a card be automatically created when an issue is created on a Github repo; 
  - and conversely, a Github issue be created when we create a card in MM.

- [Feature Idea: create card/task from Mattermost channel](https://github.com/mattermost/focalboard/issues/382)
  - `/card @tom Buy cookies`

## [Feature Idea: Timeline / Gantt](https://github.com/mattermost/focalboard/issues/662)

- We plan to work card dependencies first and potentially consider gantt charts for later next year.
