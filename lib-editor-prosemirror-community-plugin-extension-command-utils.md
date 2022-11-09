---
title: lib-editor-prosemirror-community-plugin-extension-command-utils
tags: [community, extensions, plugin-system, prosemirror, utils]
created: 2022-08-30T22:05:05.301Z
modified: 2022-08-30T22:07:26.164Z
---

# lib-editor-prosemirror-community-plugin-extension-command-utils

# guide

# discuss
- ## 

- ## 

- ## Remove contenteditable completely?_201901
- https://discuss.prosemirror.net/t/remove-contenteditable-completely/1766
- All the editing apps need to use contenteditable to some extent because certain text editing features (IME, etc.) don’t really work without it. 

- ## How to update plugin state from handleKeydown props
- https://discuss.prosemirror.net/t/how-to-update-plugin-state-from-handlekeydown-props/3420
  - I’m struggling to figure out how to mutate the plugin’s state from the `handleKeyDown` callback props.
- The typical way to do this is to have your plugin state’s `apply` method check the transaction for some specific metadata property, and update based on that. Your key handler would then dispatch a transaction with that metadata property.

- ## Separating state and view plugins__202108
- https://discuss.prosemirror.net/t/separating-state-and-view-plugins/3970
- It wouldn’t be too difficult to add a field that allows the injection of additional plugins to DirectEditorProps. 
  - But that does mean the ordering of view versus state plugins would be fixed—you can’t fine-tune their order, since they don’t appear in the same array. 
  - 👉🏻️ View plugins would either always take precedence, or never take precedence (not sure which would be more appropriate).

- ## Generalized State Architecture
- https://discuss.prosemirror.net/t/generalized-state-architecture/3908
  - I wanted to see if I could generalize an entire React frontend state management with a similar structure and actually route all transactions through a global state system.
- why is EditorState a class as opposed to a plain JSON object?
  - It seems like the only reason to use a class is to add helper methods to the classes for syntactic convenience. Is that correct?
  - I was hoping maybe you (@marijn) could share some of your thoughts on these trade-offs. Did you consider a pure-functional approach and if so, what led you to your decision to use classes?
- No, it is also so that we can control the internal data structures used in order to optimize functional updates and possibly other things. 
  - See for example the use of `rope-sequence` in the undo history, and at one point I was planning to use a representation other than a flat array for very long fragments (though that turned out to not be enough of a win to justify the complexity).

- I see. So you things like serializing to a JSON array but but using a LinkedList internally… That makes sense!
