---
title: lib-ide-vscode-community-usage
tags: [community, usage-xp, vscode]
created: 2024-08-24T16:52:42.107Z
modified: 2024-08-24T16:52:53.996Z
---

# lib-ide-vscode-community-usage

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 
# discuss-diff
- ## 

- ## 

- ## [Opening new multi-file diff view? _202411](https://github.com/microsoft/vscode-discussions/discussions/2398)
  - Is there any way for an extension to open the new built-in multi-file diff view as seen here?

- You can use the `vscode.changes` command, which was missing in the document
# discuss
- ## 

- ## 

- ## 

- ## vscode 准备支持内置 terminal 的 zsh/bash 补全列表了
- https://x.com/YuTengjing/status/1834076948089454896

- ## 🐛 [Extremely High RAM and CPU usage · Issue · microsoft/vscode-eslint \_202109](https://github.com/microsoft/vscode-eslint/issues/1336)
- I am pretty sure that this is caused by `@typescript-eslint/eslint-plugin` and the fact that some rules more or less require a full TS type checker run
  - Your analysis is correct that the eslint server very likely crashes (with OOM) and the extension restarts it.

- The issue seems to be resolved by adding the following ignore pattern to the .eslintrc.json file: `"ignorePatterns": [ "node_modules*/", "e2e/", "dist/" ]`

- [high ram/memory usage \_201910](https://github.com/microsoft/vscode-eslint/issues/782)

- ## [Process explorer as a separate renderer window ](https://github.com/microsoft/vscode/issues/41045)
- Move the vscode-process extension inside of VSCode. Like the process reporter, launch it as a separate window.

- ## [macos - Code Helper process by VS Code eating my cpu - Stack Overflow](https://stackoverflow.com/questions/74851227/code-helper-process-by-vs-code-eating-my-cpu)
- I disabled all extensions installed and the problem is gone. So i enabled one by one until i found the culprit. In my case the problem was the extension "Settings sync". I will leave it disabled for a while until a new update is out.

- [VS Code - Code Helper process using more than 100% CPU on macOS - Ask Different](https://apple.stackexchange.com/questions/351761/vs-code-code-helper-process-using-more-than-100-cpu-on-macos)
  - I suggesting disabling extensions, one by one, until you find the problematic one.
