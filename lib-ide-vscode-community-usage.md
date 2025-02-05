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
# discuss-ide-comparisons 🆚️ 
- ## 

- ## 

- ## 

- ## [Reflections on IDEA vs VS Code | Hacker News _202103](https://news.ycombinator.com/item?id=26367410)
- I used to think VS Code was going to be a threat to JetBrains IDEs considering how fast its iterative development was (thanks in large part to the productivity of JS + Web renderer) but its never seems to quite be able to reach the feature-set, polish & intelligence of JetBrains IDEs.
  - Every IDE function appears to be better implemented in JetBrains, whether it's Code Analysis, Refactoring, Navigation, Running/Debugging, Running Tests, adding new files, git integration or contextual functionality like adding package references etc. Everything is just better in JetBrains.

- 
- 
- 

# discuss-habit 🤼🏻
- ## 

- ## 

- ## 

- ## [why programmers reluctant to use auto save feature on text editors? : r/learnprogramming _202105](https://www.reddit.com/r/learnprogramming/comments/ndrc5b/why_programmers_reluctant_to_use_auto_save/)
- It mainly comes down to the warning your editor will give when you try and close an unsaved file. With autosave, this will never happen
- One of the points is to save only working code. With Autosave, one has no control over the timing.
- it probably depends on what era of programming you are from. i used to use manual saves until i used intellij for work, where auto saves happen.

- I love auto save. For everything else. But not when I'm programming.

- I prefer autosave, however it's not uncommon to have some automatic actions harken on save, like auto formatting or relaunching a dev server. 

- I love autosave because I am the sort of person to have forgotten I've saved
# discuss
- ## 

- ## 

- ## 

- ## 

- ## 

- ## [I can't stand using VSCode so I wrote my own | Hacker News _202404](https://news.ycombinator.com/item?id=40106157)
- This is the way. Anytime I have had issues with an open source project, creating a PR even if it's not great will often have it taken over, improved and merged.

- VSCode is still on the top of accessibility, so when you can claim that you work perfectly with a screen reader, you will convince me to switch.
  - people often overlook accessibility and other essential features of a modern editor, you telling me that your rudimentary rust editor is faster than vscode? and? people don't use it because it's fast (it's not).

- One of the benefits of Electron is being able to build the same app for multiple operating systems. When writing GUI app using native OS calls, how does one make sure the code is compatible with all three major operating systems?
  - Folks did this plenty prior to Electron, either by using cross-platform GUI toolkits (GTK and Qt both run on Windows, Java's been doing this forever with Swing and JavaFX, etc), or by writing GUIs for multiple toolkits/OSes that work with the same/similar core application logic.
  - Electron makes it easier to build cross-platform apps, and certainly cheaper, but it's not like it's the only way to do it.


- ## 🔍 [Visual Studio Code: Secrets of Regular Expression Search | by Nikhilbaxi | Medium _202309](https://medium.com/@nikhilbaxi3/visual-studio-code-secrets-of-regular-expression-search-71723c2ecbd2)
- (.+) : This is used to find the content between the unknown. For example, we need to find where the API call is defined.
  - `/api/user/${userId}/address/` or `/api/user/123/address/` ; 
  - `/api/user/(.+)/address/`

- To find all lines with both “apple” and “banana”:
  - `(apple.*banana)|(banana.*apple)`

- ## vscode 准备支持内置 terminal 的 zsh/bash 补全列表了
- https://x.com/YuTengjing/status/1834076948089454896

- ## 🐛 [Extremely High RAM and CPU usage · Issue · microsoft/vscode-eslint \_202109](https://github.com/microsoft/vscode-eslint/issues/1336)
- I am pretty sure that this is caused by `@typescript-eslint/eslint-plugin` and the fact that some rules more or less require a full TS type checker run
  - Your analysis is correct that the eslint server very likely crashes (with OOM) and the extension restarts it.

- The issue seems to be resolved by adding the following ignore pattern to the .eslintrc.json file: `"ignorePatterns": [ "node_modules*/", "e2e/", "dist/" ]`

- [high ram/memory usage _201910](https://github.com/microsoft/vscode-eslint/issues/782)

- ## [Process explorer as a separate renderer window ](https://github.com/microsoft/vscode/issues/41045)
- Move the vscode-process extension inside of VSCode. Like the process reporter, launch it as a separate window.

- ## [macos - Code Helper process by VS Code eating my cpu - Stack Overflow](https://stackoverflow.com/questions/74851227/code-helper-process-by-vs-code-eating-my-cpu)
- I disabled all extensions installed and the problem is gone. So i enabled one by one until i found the culprit. In my case the problem was the extension "Settings sync". I will leave it disabled for a while until a new update is out.

- [VS Code - Code Helper process using more than 100% CPU on macOS - Ask Different](https://apple.stackexchange.com/questions/351761/vs-code-code-helper-process-using-more-than-100-cpu-on-macos)
  - I suggesting disabling extensions, one by one, until you find the problematic one.
