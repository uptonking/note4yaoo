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

- ## 

- ## 

- ## [How to insert an async uploaded image?](https://discuss.prosemirror.net/t/how-to-insert-an-async-uploaded-image/589)
- view is a mutable object that has its `state` property updated when you call `updateState` or `update` , 
  - and **state objects are persistent immutable values that are recreated (sharing as much of the old structure as possible) when updated**

- ## [Plugin's appendTransaction should be "appended" by definition](https://discuss.prosemirror.net/t/plugins-appendtransaction-should-be-appended-by-definition/1331)
  - It seems that when appending a transaction via plugin, to the array of current transactions, by definition it should be part of the same history block
  - In the history module, appendedTransactions are still dependent of the time between changes

- ## [How similar is PM architecture to a React/Redux architecture?_201804](https://discuss.prosemirror.net/t/how-similar-is-pm-architecture-to-a-react-redux-architecture/1265)
- It’s similar to Redux, but not quite the same — our transactions are a somewhat different thing than Redux actions—they have a uniform shape, rather than being a kind of sum type.

- ## [💡 Discussion: The limits of actions and reducers_201612](https://discuss.prosemirror.net/t/discussion-the-limits-of-actions-and-reducers/551)
  - In 0.11, ProseMirror moved to a linear dataflow architecture, where the editor state isn’t imperatively updated, but only changes in response to actions that must be explicitly applied to a state to get a new state
  - it has had amazing effects on how easy it is to write robust extensions, and on how clean it allows the implementation of the view to be. 

- The main complicating requirement is modularity.
  - Most of the literature around Elm or Redux assumes that the action types and reducers that act on a given piece of state are designed and written as a single coherent(有条理的；清楚易懂的) module. 
  - But ProseMirror’s plugin architecture means that plugins can define new action types, add state fields with their own reducers, and may need to respond to actions that influence other parts of the state (the document or selection, usually).

- Actions to _Trans_actions
  - Drop the concept of an ‘action’ as a raw object with a type property
  - Define a Transaction class that fills its role instead, while also replacing the EditorTransform class. 
  - These are objects that represent any kind of atomic change in the editor state. They are still applied, much like actions currently are, but instead of being interpreted by reducers they rather explicitly declare the kind of changes they embody. 

- ## [🤔 Should I use a state based plugin or a view based one?](https://discuss.prosemirror.net/t/should-i-use-a-state-based-plugin-or-a-view-based-one/5214)
  - We’re in the process of doing a proof of concept for pagination (e.g. painting page dividers + #page) using Tiptap / Prosemirror. 
  - In order to do this, we’re using decorations + custom plugin. 

- 👉🏻 Decorations that rely on DOM measurements are definitely tricky in that they create a data dependency cycle 
  - (the rendering of the doc uses decorations as input, the measuring needs the doc to be rendered, and the decorations are computed from the measures). 
  - **So you’ll probably need to schedule your own re-measures somewhere outside the editor’s own update cycle**.
- **Decorations have to go into the state (or be recomputed on the fly)**, so you’ll need a state field to store them. 
  - The general approach here would be to, in the state field apply method, try to preserve the old page break decorations by mapping them, and in a plugin view update method, see if the page breaks have to be re-checked/recomputed, and if so, schedule a process that measures the doc and determines appropriate page breaks, compare those to the existing page breaks, and update a transaction that updates the state if they differ.

- Even if we forget about the scheduling problem part of this, I think there is a bigger problem that we just recently found. This is, tables. We’re relying on this tiptap custom extension that allow us to paint table elements in the doc. Following above approach causes a bunch of scenarios to pain divider / pagebreak inside a cell, reason being that `posAtCoords` is content agnostic, so it can return a pos inside of a table cell, and that’s where we paint the divider which is no bueno(Yes or affirmative).

- Google docs (and probably also the online MS office tools) do their own layout entirely, rather than relying on the browser’s DOM/CSS. And probably included pagination in their layout design from the start.
  - They compute where things are in JavaScript, rather then letting DOM/CSS control the positioning. Of course, I don’t know a lot, since none of this is open source.

- ## not a big fan of the prosemirror schema myself
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

- [Propose direct view plugins_202109](https://github.com/ProseMirror/rfcs/pull/17)
  - Allow plugins to be passed directly to the view, without storing them in the state.
  - Merged and released as part of prosemirror-view 1.20.0

- ## Generalized State Architecture
- https://discuss.prosemirror.net/t/generalized-state-architecture/3908
  - I realized that I really liked the architecture of ProseMirror (the plugin system is awesome) and I wanted to see if I could generalize an entire React frontend state management with a similar structure and actually route all transactions through a global state system.
- 🤔 **why is `EditorState` a class as opposed to a plain JSON object**?
  - It seems like the only reason to use a class is to add helper methods to the classes for syntactic convenience. Is that correct?
  - In practice, I can imagine that using classes is really convenient when the state model is really complicated. 
  - I was hoping maybe you (@marijn) could share some of your thoughts on these trade-offs. Did you consider a pure-functional approach and if so, what led you to your decision to use classes?

- It seems like the only reason to use a class is to add helper methods to the classes for syntactic convenience. Is that correct?
  - 👉🏻 No, it is also **so that we can control the internal data structures used in order to optimize functional updates** and possibly other things. 
  - See for example the use of `rope-sequence` in the undo history, and at one point I was planning to use a representation other than a flat array for very long fragments (though that turned out to not be enough of a win to justify the complexity).

- I see. So you things like serializing to a JSON array but but using a LinkedList internally. That makes sense!
