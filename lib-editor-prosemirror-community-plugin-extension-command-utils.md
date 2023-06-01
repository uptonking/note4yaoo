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

- ## [Plugin's appendTransaction should be "appended" by definition](https://discuss.prosemirror.net/t/plugins-appendtransaction-should-be-appended-by-definition/1331)
  - It seems that when appending a transaction via plugin, to the array of current transactions, by definition it should be part of the same history block
  - In the history module, appendedTransactions are still dependent of the time between changes



- ## [Discussion: The limits of actions and reducers - discuss. ProseMirror_201612](https://discuss.prosemirror.net/t/discussion-the-limits-of-actions-and-reducers/551)
  - In 0.11, ProseMirror moved to a linear dataflow architecture, where the editor state isn’t imperatively updated, but only changes in response to actions that must be explicitly applied to a state to get a new state

- The main complicating requirement is modularity. 
  - Most of the literature around Elm or Redux assumes that the action types and reducers that act on a given piece of state are designed and written as a single coherent module. 
  - But ProseMirror’s plugin architecture means that plugins can define new action types, add state fields with their own reducers, and may need to respond to actions that influence other parts of the state (the document or selection, usually).
- Decoupling state transitions from reducers
  - This has downsides too.

- ## [Should I use a state based plugin or a view based one? - Show - discuss. ProseMirror](https://discuss.prosemirror.net/t/should-i-use-a-state-based-plugin-or-a-view-based-one/5214)
- Decorations that rely on DOM measurements are definitely tricky in that they create a data dependency cycle 
  - (the rendering of the doc uses decorations as input, the measuring needs the doc to be rendered, and the decorations are computed from the measures). 
  - So you’ll probably need to schedule your own re-measures somewhere outside the editor’s own update cycle.

- Decorations have to go into the state (or be recomputed on the fly), so you’ll need a state field to store them. The general approach here would be to, in the state field apply method, try to preserve the old page break decorations by mapping them, and in a plugin view update method, see if the page breaks have to be re-checked/recomputed, and if so, schedule a process that measures the doc and determines appropriate page breaks, compare those to the existing page breaks, and update a transaction that updates the state if they differ.

- Even if we forget about the scheduling problem part of this, I think there is a bigger problem that we just recently found. This is, tables. We’re relying on this tiptap custom extension that allow us to paint table elements in the doc. Following above approach causes a bunch of scenarios to pain divider / pagebreak inside a cell, reason being that posAtCoords is content agnostic, so it can return a pos inside of a table cell, and that’s where we paint the divider which is no bueno.

- ## not a big fan of the prose mirror schema myself
- https://twitter.com/_mql/status/1615796336070168584
- Re ProseMirror, I actually like the explicit programmatic definition of the nodes. Rather than some plugin mechanism, that leads to late failing of code.
  - Navigating the model programmatically is tricky though, because it has only flat positions.

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
