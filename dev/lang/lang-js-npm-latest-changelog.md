---
title: lang-js-npm-latest-changelog
tags: [changelog, lang-js, npm]
created: 2023-12-25T10:37:52.547Z
modified: 2024-01-02T07:50:05.847Z
---

# lang-js-npm-latest-changelog

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

## [v12.0.0 _20260709](https://github.com/npm/cli/releases/tag/v12.0.0)

- npm now supports node ^22.22.2 || ^24.15.0 || >=26.0.0

- The default license for `npm init` has been changed from "ISC" to an empty string.

- [Preparing for npm v12: install scripts and non-registry sources become opt-in  _202606](https://github.com/orgs/community/discussions/198547)
  - Install scripts are off by default. preinstall, install, and postinstall from dependencies won't run unless explicitly allowed.
  - allow-git and allow-remote now default to "none"; set them to "all" (or "root") to install git or user-supplied tarball-URL dependencies.
  - --allow-file and --allow-directory exist too, but their defaults are not changing in v12.
  - root `preinstall` now runs before dependencies are installed.
- 💡 可临时使用旧版npm `npm i -g install npm@11.15.0`

- unknown configs in .npmrc, unknown CLI flags, abbreviated flags, and single-hyphen multi-char shorthands now throw instead of warning.

- npm view --json now always returns an array.
- The npm pkg output is no longer forced to json. 
- the --json output of npm pack and npm publish have changed. They are now always consistent, and in the same format.
- npm shrinkwrap is removed, the shrinkwrap config alias is removed, and npm-shrinkwrap.json is no longer loaded or honored at the project root or from inside dependency tarballs. 
  - Rename project-root npm-shrinkwrap.json to package-lock.json; 
  - use `bundleDependencies` if you need to ship a locked dependency tree.
- the star, stars and unstar commands have been removed

- Preserve https protocol when working with git

- 
- 
- 

## [v11.0.0 _20241217](https://github.com/npm/cli/releases/tag/v11.0.0)

- npm now supports node ^20.17.0 || >=22.9.0

- When publishing a package with a pre-release version, you must explicitly specify a tag.
- --ignore-scripts now applies to all lifecycle scripts, include prepare
- The `npm hook` command has been removed

- 
- 

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

- [`v9.x` FAQ · npm/cli](https://github.com/npm/cli/issues/5844)
  - npm@9 changed the default value of install-links from false to true.
  - This means that npm will now attempt to install directories by default instead of symlinking them.
  - Note that workspaces will always be symlinked, so the latest workspaces changes will always be reflected in your package.

## v8.0.0_20211007

- require nodejs v10

- v8.3.0_20211209
  - introduces `overrides`: provide a way to replace a package in your dependency tree with another version

## v7.0.0_20201013 (对应node.v14)

- [Presenting v7.0.0 of the npm CLI_202010](https://github.blog/2020-10-13-presenting-v7-0-0-of-the-npm-cli/)
- npm 7 comes with some long-awaited and requested features including:
  - Workspaces
  - ✨ package-lock v2 and support for yarn.lock. Prior to npm 7 yarn.lock files were ignored, the npm cli can now use yarn.lock as source of package metadata and resolution guidance.
  - Automatically installing peer dependencies
- The internals of npm have been significantly refactored for separating concerns. 
  - the inspection and management of the node_modules tree has been moved to the module Arborist
- Breaking changes in npm 7.0.0 include:
  - Automatically installing peer dependencies 
  - `npx` has been completely rewritten to use the `npm exec` command
  - npm uses the `package.exports` field making it no longer possible to require() npm’s internal modules.
# more
- [npm trusted publishing with OIDC is generally available - GitHub Changelog _202507](https://github.blog/changelog/2025-07-31-npm-trusted-publishing-with-oidc-is-generally-available/)
