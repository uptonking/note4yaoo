---
title: web-events-keyboard
tags: [keyboard-event]
created: 2023-03-19T20:03:10.361Z
modified: 2023-03-19T20:03:32.594Z
---

# web-events-keyboard

# guide

# blogs

## [How Discord Implemented App-Wide Keyboard Navigation – Bram.us](https://www.bram.us/2020/12/24/how-discord-implemented-app-wide-keyboard-navigation/)

## [How to Create Custom Keyboard Shortcuts using JavaScript _201903](https://ralzohairi.medium.com/adding-custom-keyboard-shortcuts-to-your-website-b4151fda2e7a)

- 💡 只在事件中处理dom相关操作和参数，可将业务逻辑提取到与dom无关的工具方法

- The keydown event is fired when a key is pressed and the keyup event is fired when a key is released.

- firstly create a boolean reference to help us track whether the key is clicked or not. 
  - However, it would be a little too much to create a variable for each key. 
  - For that reason, an object is created with a property for each key code that you want to track down. A key code is usually the ASCII code.
# utils
- https://github.com/jamiebuilds/tinykeys /3.8kStar/MIT/202408/ts/体积小
  - https://jamiebuilds.github.io/tinykeys/
  - A tiny (~650 B) & modern library for keybindings
  - In some instances, tinykeys will alias keys depending on the platform to simplify cross-platform keybindings on international keyboards.
  - Keybindings are made up of a sequence of presses. A press can be as simple as a single key which matches against KeyboardEvent.code and KeyboardEvent.key (case-insensitive).
  - The purpose of the `AltGraph` key is to type "Alternate Graphics", so you will often want to use the `event.code` (KeyS) for letters instead of `event.key` (S)

- https://github.com/webNeat/ctrl-keys /MIT/202406/ts/NoDeps
  - A tiny, super fast, typescript library to handle keybindings efficiently.
  - Handles multi-keys sequences like `ctrl+k ctrl+b` (Inspired by vscode keybindings).
  - Does not add global listeners to the window, instead it lets you create multiple handlers and bind them to any DOM elements.
  - Dynamically add, remove, enable, and disable keybindings.
  - Typescript autocomplete for keybindings

- https://github.com/jaywcjlove/hotkeys-js /MIT/202406/js/NoDeps
  - https://jaywcjlove.github.io/hotkeys-js
  - A robust Javascript library for capturing keyboard input. 
  - react-hotkeys is the React component that listen to keydown and keyup keyboard events, defining and dispatching keyboard shortcuts. 

- https://github.com/ssleptsov/ninja-keys /MIT/202207/ts/inactive
  - Keyboard shortcut interface for your website that works with Vanilla JS, Vue, and React.

- https://github.com/fabiospampinato/shosho /MIT/202309/ts/inactive
  - A modern and powerful shortcuts management library.
  - largely built on top of KeyboardEvent#code and KeyboardEvent#key, for great compatibility across browsers, platforms, languages and layouts.
  - It is fast. Almost always this library will do O(1) registrations, O(1) disposals, O(1) lookups and O(1) resetting.
  - https://github.com/fabiospampinato/shortcuts
    - a thin wrapper over ShoSho that provides a VSCode-like interface for managing shortcuts.

- https://github.com/RobertWHurst/Keystrokes /MIT/202409/ts
  - Keystrokes as an easy to use library for binding functions to keys and key combos. 
  - It can be used with any TypeScript or JavaScript project, even in non-browser environments

- https://github.com/ccampbell/mousetrap /apache2/202001/js/NoDeps/inactive
  - Simple library for handling keyboard shortcuts in Javascript
  - It has support for keypress, keydown, and keyup events on specific keys, keyboard combinations, or key sequences.
  - It works with international keyboard layouts
  - You can programatically trigger key events with the trigger() method
  - [Are there any alternatives to mousetrap? _202201](https://github.com/ccampbell/mousetrap/issues/512)
# more

# discuss-stars

- ## 

- ## 

- ## [macos - Why does Javascript drop keyUp events when the metaKey is pressed on Mac browsers? - Stack Overflow](https://stackoverflow.com/questions/11818637/why-does-javascript-drop-keyup-events-when-the-metakey-is-pressed-on-mac-browser)
- Although `event.metaKey` returns `false` , `event.keyCode` and event.key are still populated.

- [macos - Keyup event not firing when meta key is held (Mac OSX only?) - How to handle in javascript? - Stack Overflow](https://stackoverflow.com/questions/73412298/keyup-event-not-firing-when-meta-key-is-held-mac-osx-only-how-to-handle-in)
# discuss
- ## 

- ## 

- ## 

- ## [Getting mouse position in keyboard event - Stack Overflow](https://stackoverflow.com/questions/7562503/getting-mouse-position-in-keyboard-event)
- Cache mouse position in a global variable in every `mousemove` event and use it when a key event fires
