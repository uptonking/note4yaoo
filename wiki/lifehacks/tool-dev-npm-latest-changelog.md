---
title: tool-dev-npm-latest-changelog
tags: [changelog, npm]
created: 2023-12-25T10:37:52.547Z
modified: 2023-12-25T10:38:05.986Z
---

# tool-dev-npm-latest-changelog

# guide

# roadmap
- [Today(20201119)'s npm OpenRFC recap](https://twitter.com/ruyadorno/status/1329164549140996100)
  - Workspaces noHoist option
  - Configurable cli default-command
  - Registry dependency specifier
# changelog
- ref
  - [v9 Changelog | npm Docs](https://docs.npmjs.com/cli/v9/using-npm/changelog)

## v

## [v10.0.0_v20230901](https://github.com/npm/cli/releases/tag/v10.0.0)

- require nodejs v18.17.0 || v20.5.0

- remove implicit `if-present` logic from run-script workspaces
  - npm no longer treats missing scripts as a special case in workspace mode. Use `if-present` to ignore missing scripts.
- remove "ci-name" config
- remove "tmp" config
- remove metric-registry config

## [v9.0.0_20221024](https://github.com/npm/cli/releases/tag/v9.0.0)

- require nodejs v14.17.0 || v16.13.0 || v18.0.0

- Our goal with this major release was to standardize appropriate defaults and clean up legacy configurations where possible.

- use v3 lockfiles by default
- `install-links` config defaults to "true"
  - `npm link` should override `--install-links`.
- deprecate boolean install flags in favor of `--install-strategy`.
  - add `--install-strategy=hoisted|nested|shallow`, deprecate --global-style, --legacy-bundling
- `npm access` subcommands have been renamed
- npm will no longer attempt to modify ownership of files it creates

- v9.4.0_20230126
  - Isolated mode RFC 终于得到了实现。
  - 在设置 `install-strategy=linked` 后，npm 也会像 pnpm 一样，只对显式声明的依赖通过链接的形式挂到 node_modules 下，而不再对所有依赖做无脑 flat

## v8.0.0_20211007

- require nodejs v10

- v8.3.0_20211209
  - introduces `overrides`: provide a way to replace a package in your dependency tree with another version

## v7.0.0_20201013

- [Presenting v7.0.0 of the npm CLI_202010](https://github.blog/2020-10-13-presenting-v7-0-0-of-the-npm-cli/)
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
# more
