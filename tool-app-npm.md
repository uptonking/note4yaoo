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

- Managing individual versions in a monorepo is really hard. 
  - https://twitter.com/devongovett/status/1294367192754950144
  - Even tools like lerna basically assume you bump all changed packages in lock-step.
  - Feels like a case where an actual UI is better than a CLI. Started building a basic one for our needs.
- Have a look at Microsoft Rush. It has versioning, changelogs and monorepos absolutely nailed. I've completely dropped lerna.
  - How much does it require you to buy into their way of doing things? Would it be difficult to move over from yarn workspaces/lerna?
  - It depends how complex your setup with lerna is. It supports pnpm, yarn and npm. I would say that it's fairly opinionated, but the opinions are quite in line with lerna's usage patterns. The docs focus on a migration making testing it out with minimal work easy
  - What is a bit different is the publish steps. Open a PR, make changes 'rush change' to generate diff and change log + define versions.
    - Then you publish and it makes changelogs, tags, merges... So smooth and robust.
    - Doing the same with lerna always felt like fingers crossed!
- Combination of commitizen and conventional commits allowed my last team to determine versions automatically, 
  - it actually worked really well - but you have to be a stickler about commit messages
- If modules leave in a single repo, they are probably very coupled and it makes sense to release them all together.
  - If that's not the case, should they move into separate repos?
- I ended up ditching lerna for a custom publish script that determines the changed package from the changed directory, 
  - and the semver bump based on the commit message. 
  - Works pretty well because each version is an aggregate of many commits, I just don't need to think about it.

- pnpm has built-in support for monorepos (a.k.a. multi-package repositories, multi-project repositories, or monolithic repositories). 
  - You can create a workspace to unite multiple projects inside a single repository.
  - A workspace must have a pnpm-workspace.yaml file in its root.

### lerna

- 优点
  - 提升依赖
  - bump version：若package A变了，依赖A的其他package也会变
  - publish：可配置registry
    - I'd like to use conventional commits for changelogs, not atlassian/changesets
  - 批量执行命令，如build

- 缺点
  - monorepo难以利用tsc的增量编译
  - babel

- Ah I'd very  much encourage you to move from having lerna manage the monorepo to having yarn workspaces do it. 
  - You can still use all the other lerna helpers, but yarn handles the inter-package links way better. 
  - I almost never have to delete node_modules any more.

- I'm using Lerna  currently, but the way its change detection works results in lots of unnecessary publishes.

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
