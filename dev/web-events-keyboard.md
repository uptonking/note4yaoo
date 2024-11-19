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

# utils
- https://github.com/jamiebuilds/tinykeys /3.8kStar/MIT/202408/ts/体积小
  - https://jamiebuilds.github.io/tinykeys/
  - A tiny (~650 B) & modern library for keybindings
  - In some instances, tinykeys will alias keys depending on the platform to simplify cross-platform keybindings on international keyboards.
  - Keybindings are made up of a sequence of presses.

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
