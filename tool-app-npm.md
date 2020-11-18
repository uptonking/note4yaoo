---
title: tool-app-npm
tags: [npm, tool]
created: '2020-11-18T10:18:22.406Z'
modified: '2020-11-18T10:18:33.526Z'
---

# tool-app-npm

## workspace

- ref
  - [docs: workspaces](https://docs.npmjs.com/cli/v7/using-npm/workspaces)
  - [rfc: npm workspaces](https://github.com/npm/rfcs/blob/latest/implemented/0026-workspaces.md)

- Workspaces is a generic term that refers to the set of features in the npm cli that provides support to managing multiple packages from your local files system from within a singular top-level, root package.
  - This set of features makes up for a much more streamlined workflow handling linked packages from the local file system. 
  - Automating the linking process as part of `npm install` and avoiding manually having to use `npm link` in order to add references to packages that should be symlinked into the current `node_modules` folder.
  - We also refer to these packages being auto-symlinked during `npm install` as a single workspace, 
  - meaning it's a nested package within the current local file system that is explicitly defined in the `package.json` `workspaces` configuration.

## npm-blog

- ### [Presenting v7.0.0 of the npm CLI](https://github.blog/2020-10-13-presenting-v7-0-0-of-the-npm-cli/)
- npm 7 comes with some long-awaited and requested features including:
  - Workspaces
  - package-lock v2 and support for yarn.lock
  - Automatically installing peer dependencies
- The internals of npm have been significantly refactored for separating concerns. 
  - the inspection and management of the node_modules tree has been moved to the module Arborist
- Breaking changes in npm 7.0.0 include:
  - Automatically installing peer dependencies 
  - `npx` has been completely rewritten to use the `npm exec` command
  - npm uses the `package.exports` field making it no longer possible to require() npm’s internal modules.

- ### [npm v7 Series - Introduction](https://blog.npmjs.org/post/617484925547986944/npm-v7-series-introduction)
- Vision
  - Reduce noise that is not actionable.
    - We’ve gone through the entire project from the data management to the presentation layers, stripping output that doesn’t provide worthwhile information.
  - Manage your packages for you.
  - Strict separation of concerns. 
    - npm CLI itself is becoming strictly the user-interface layer, 
    - and we’ve moved out all complex tree management and registry interactions to @npmcli/arborist, pacote, and the various libnpm* modules.
  - Be as fast as possible while behaving correctly.
- Coming Attractions
- RFC Process

## ref

- [npm v7 Series - Beta Release!](https://blog.npmjs.org/post/626173315965468672/npm-v7-series-beta-release-and-semver-major)
