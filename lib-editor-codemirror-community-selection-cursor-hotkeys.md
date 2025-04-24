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

- ## 🌰 [Triple click behavior - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/triple-click-behavior/4051)
  - I’m dealing with a case where triple clicking a line will select everything on the line + the newline character at the very end.
  - It seems that this deviation from standard text selection behavior is generally intended for code editors because it helps with workflows involving copy-pasting blocks of code.

- ## 🌰 [Codemirror 6: Move cursor to specific line and mark its text - discuss. CodeMirror](https://discuss.codemirror.net/t/codemirror-6-move-cursor-to-specific-line-and-mark-its-text/4388)

# discuss-hotkeys
- ## 

- ## 

- ## 

- ## 💡 [Codemirror shortcut capturing - discuss. CodeMirror _202405](https://discuss.codemirror.net/t/codemirror-shortcut-capturing/8236)
- CodeMirror does not preventDefault or stopPropagation keyboard events that it doesn’t have a keymap binding for. So it shouldn’t interfere with other shortcuts, if you listen for the keys on the outer DOM elements or the window, even when the editor is focused.

- 🧐 It was the hotkeysjs blocking shortcut in input/textarea

- ## [overriding certain default keymaps - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/overriding-certain-default-keymaps/6181)
  - I’d like to keep majority of the default keymaps and override some of them. 
- You can tweak the precedence of your keymap using `Prec` to tweak the order of execution of your key bindings

- ## [stopPropagation doesn't work if key Ctrl is used instead of Mod - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/stoppropagation-doesnt-work-if-key-ctrl-is-used-instead-of-mod/7990)
- custom commands has to return true to make stopPropagation work
- Will Compartment() work for dynamic keymaps also? I’ve a scenario where I want to reconfigure the shortcuts dynamically based on user preference.
  - Yes, compartments work for all types of extensions.

- ## [How does the autocomplete module prevent default key effects? - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/how-does-the-autocomplete-module-prevent-default-key-effects/5439)
  - what should preventDefault do in the case run returns false?
  - preventDefault⁠: When set to true (the default is false), this will always prevent the further handling for the bound key, even if the command(s) return false.
- It prevents the browser’s default behavior, not any other handlers from running.

- ## 💡 [Shortcut mode starting with ESC - v6 - discuss. CodeMirror _202204](https://discuss.codemirror.net/t/shortcut-mode-starting-with-esc/4246)
  - I am looking for a general idea of how to go about implementing a shortcut mode where you press ESC and then another key to trigger a function. I currently see that ESC is used as a trigger to switch between indent and focus change.
- You can use multi-stroke key bindings for something like this, but I don’t recommend using escape for this purpose because, indeed, it’ll mess with the tab handling.

- Is there a good way to create a binding for escape that doesn’t mess with the tab handling? Or to selectively handle escape based on some editor state?
  - You could provide another way to move focus out of the editor. Or, if your esc binding only applies in certain situations, it will be usable with tab in cases where your handler returns false.

- ## [searchKeymap: own handling of "Escape" key - v6 - discuss. CodeMirror _202408](https://discuss.codemirror.net/t/searchkeymap-own-handling-of-escape-key/8538)
  - I have the problem that I have a widget that surrounds the cm6 editor and it handles the Escape key. I want to change the handling within the search addon so that the event doesn’t bubble up the DOM if I press the Escape key while focus is within the search panel’s input fields
- The recommended approach is to check for `event.defaultPrevented` in your outer handlers, and ignore events that have already been prevented. 
  - If that’s not practical, add a (low precedence) keydown handler to your editor that calls stopPropagation on all events that have their default behavior prevented.

# discuss-selection/cursor
- ## 

- ## [Event on End of Selection? - discuss. CodeMirror _202010](https://discuss.codemirror.net/t/event-on-end-of-selection/2671)
- No, this doesn’t exist. You might be able to cobble something together by combining a debounced "change" event listener with "mousedown"/"mouseup" handlers that track the mouse button state.

- ## [Selections and Life Cycle - v6 - discuss. CodeMirror _202206](https://discuss.codemirror.net/t/selections-and-life-cycle/4501/5)
- The editor was losing focus (when you click a button that gets focus) and the document change was causing the DOM selection to get mangled(严重损毁; 使变形; 破坏). But because the editor didn’t consider the DOM selection to be under its control when it isn’t focused, it didn’t repair that. Attached patch adjusts the logic for when to manage the DOM selection to avoid situations like this.

# discuss
- ## 

- ## 

- ## 

- ## [Multiple cursor by clicking - v6 - discuss. CodeMirror _202206](https://discuss.codemirror.net/t/multiple-cursor-by-clicking/4463)
- For future multi-cursor users’ reference:
  - Click to Create Multiple Cursors (EditorView.clickAddsSelectionRange ). Bound to Ctrl (macOS: Cmd) + Click by default.
  - Drag to Create Multiple Cursors ( rectangularSelection() ). Bound to Alt (macOS: Option) + Drag.

- This differs from VS Code which is
  - Click to Create Multiple Cursors: Bound to Alt (macOS: Option) + Click.
  - Drag to Create Multiple Cursors: Bound to Alt (macOS: Option) + Shift + Drag.

- ## 🌰 [Is it possible deleteTab command - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/is-it-possible-deletetab-command/4453)
  - I want delete tab when I use Shift-Tab shortcut. But I can’t find any StateCommand
  - indentMore and indentLess command affects line. It doesn’t help me.

- Commands are just functions. Writing one that deletes a tab before the cursor shouldn’t be hard.

- ## [Moving of cursor with different size mark decoration and replace decoration issues - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/moving-of-cursor-with-different-size-mark-decoration-and-replace-decoration-issues/4198)
- Arrow key motion is implemented with regular key bindings in defaultKeymap, so you can create custom commands that implement this type of vertical motion and bind them to the arrow keys (don’t forget to also create a selection-extending version for when shift is held down).

- ## 🌰 [Determine if selection is inside of markdown code block - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/determine-if-selection-is-inside-of-markdown-code-block/4272)
- https://replit.com/@replitfaris/is-in-codeblock#index.ts

- ## [Line background color and selection layering - v6 - discuss. CodeMirror _202212](https://discuss.codemirror.net/t/line-background-color-and-selection-layering/5413)
  - In v5, you could select a line or wrap element to apply a class to a full line. By choosing the wrap class, you could style the containing element of some lines and apply, e.g., a background color to it. Then, if you selected something, you could first see the line’s background color, then the selection, and finally the text.
  - With the more lean DOM that v6 produces, there is no more wrapping, and hence the background color must be applied directly to the text layer.

- Have to use transparent backgrounds, or use the layer feature to display a separate element behind the selection layer.
