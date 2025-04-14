---
title: lib-editor-app-community-keyboard-hotkeys
tags: [community, editor, hotkeys, keyboard-event]
created: 2024-11-25T09:16:50.568Z
modified: 2024-11-25T09:17:18.678Z
---

# lib-editor-app-community-keyboard-hotkeys

# guide

- macos下难以覆盖的快捷键
  - chrome cmd/ctrl+N 浏览器保留快捷键
  - mac cmd+M 会缩小窗口
  - mac cmd+, 会打开设置页

## common-hotkeys

- resources
  - [DefKey](https://defkey.com/)
  - [keycombiner Search Shortcuts](https://keycombiner.com/collecting/collections/public/search/)
  - [shortcutworld for Windows, Mac OS, Linux.](https://shortcutworld.com/)
  - [Shortcuts.design | Every shortcut for designers in one place](https://shortcuts.design/)

- go to definition
  - F12
  - ctrl + G: spyder
  - ctrl + T: geany, brackets
  - alt + G: UE5
# discuss-stars
- ## 

- ## 

- ## 

- ## [Any way to override Ctrl+N to open a new window in Chrome? - Stack Overflow](https://stackoverflow.com/questions/38838302/any-way-to-override-ctrln-to-open-a-new-window-in-chrome)
- There is no way to override Ctrl+N, Ctrl+T, or Ctrl+W in Google Chrome since version 4 of Chrome (shipped in 2010).
  - In Chrome4, certain control key combinations have been reserved for browser usage only and can no longer be intercepted by the client side JavaScript in the web page.
  - 💡 Only known workaround is to open your webpage/extension as a Chrome app where it will again have permission to override these blacklisted key combos

# discuss-macos-hotkeys
- ## 

- ## [macos - How to prevent Command+Option+M from minimizing Safari - Stack Overflow](https://stackoverflow.com/questions/40249043/how-to-prevent-commandoptionm-from-minimizing-safari)
- Change this default shortcut at: System Prefs > Keyboard > Shortcuts > App Shortcuts > [+]

# discuss-hotkeys
- ## 

- ## 

- ## 🤔 [Chrome - global keyboard shortcut not actually global - Stack Overflow](https://stackoverflow.com/questions/34366233/chrome-global-keyboard-shortcut-not-actually-global)
- It could be this: Chrome cannot read keyboard shortcuts for applications running as Administrator, unless Chrome is also ran as administrator. 
  - I learned this in figuring out why Google Play music shortcuts weren't working in Steam games.
