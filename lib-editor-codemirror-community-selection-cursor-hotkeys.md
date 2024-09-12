---
title: lib-editor-codemirror-community-selection-cursor-hotkeys
tags: [codemirror, community, cursor, hotkeys, selection]
created: 2024-08-11T06:46:13.704Z
modified: 2024-08-11T06:46:39.843Z
---

# lib-editor-codemirror-community-selection-cursor-hotkeys

# guide

# discuss-stars
- ## 

- ## 

- ## [Codemirror 6: Move cursor to specific line and mark its text - discuss. CodeMirror](https://discuss.codemirror.net/t/codemirror-6-move-cursor-to-specific-line-and-mark-its-text/4388)

# discuss-hotkeys
- ## 

- ## 💡 [Shortcut mode starting with ESC - v6 - discuss. CodeMirror _202204](https://discuss.codemirror.net/t/shortcut-mode-starting-with-esc/4246)
  - I am looking for a general idea of how to go about implementing a shortcut mode where you press ESC and then another key to trigger a function. I currently see that ESC is used as a trigger to switch between indent and focus change.
- You can use multi-stroke key bindings for something like this, but I don’t recommend using escape for this purpose because, indeed, it’ll mess with the tab handling.

- Is there a good way to create a binding for escape that doesn’t mess with the tab handling? Or to selectively handle escape based on some editor state?
  - You could provide another way to move focus out of the editor. Or, if your esc binding only applies in certain situations, it will be usable with tab in cases where your handler returns false.

- ## [searchKeymap: own handling of "Escape" key - v6 - discuss. CodeMirror _202408](https://discuss.codemirror.net/t/searchkeymap-own-handling-of-escape-key/8538)
  - I have the problem that I have a widget that surrounds the cm6 editor and it handles the Escape key. I want to change the handling within the search addon so that the event doesn’t bubble up the DOM if I press the Escape key while focus is within the search panel’s input fields
- The recommended approach is to check for `event.defaultPrevented` in your outer handlers, and ignore events that have already been prevented. 
  - If that’s not practical, add a (low precedence) keydown handler to your editor that calls stopPropagation on all events that have their default behavior prevented.

# discuss-cursor
- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## 

- ## 

- ## [Determine if selection is inside of markdown code block - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/determine-if-selection-is-inside-of-markdown-code-block/4272)
- https://replit.com/@replitfaris/is-in-codeblock#index.ts

- ## [Line background color and selection layering - v6 - discuss. CodeMirror _202212](https://discuss.codemirror.net/t/line-background-color-and-selection-layering/5413)
  - In v5, you could select a line or wrap element to apply a class to a full line. By choosing the wrap class, you could style the containing element of some lines and apply, e.g., a background color to it. Then, if you selected something, you could first see the line’s background color, then the selection, and finally the text.
  - With the more lean DOM that v6 produces, there is no more wrapping, and hence the background color must be applied directly to the text layer.

- Have to use transparent backgrounds, or use the layer feature to display a separate element behind the selection layer.
