---
title: lib-editor-codemirror-community-plugin-extension
tags: [codemirror, community, extensions, plugin-system]
created: 2024-08-11T06:42:26.160Z
modified: 2024-08-11T06:42:41.903Z
---

# lib-editor-codemirror-community-plugin-extension

# guide

# discuss-architecture
- ## 

- ## 

- ## 

- ## [Proposal: Coarser Module Structure - v6 - discuss. CodeMirror _202204](https://discuss.codemirror.net/t/proposal-coarser-module-structure/4243)
  - 似乎未实现，有争议
  - The ‘core’ library (not including the language packages) currently consists of 24 different packages. Setups usually don’t need all of them, but you’ll still easily end up with almost 20 of them, plus language support, for a typical editor project.
  - what I’m currently leaning towards is to move a bunch of the smaller packages into other packages, to get a structure that is still modular, but not annoyingly modular. The interface as a whole of course doesn’t get smaller, but needing to install and import from fewer different packages should reduce cognitive load for developers somewhat.
- With y-codemirror.next I’d like to replace the default rangeset, history, and collab implementations with data structures that work on the Yjs CRDT. I feel these modules shouldn’t be part of the state & commands package which are used by everyone.

- ## 🏘️🤔 [Request: View plugin method that runs at the same phase as update listeners - v6 - discuss. CodeMirror _202404](https://discuss.codemirror.net/t/request-view-plugin-method-that-runs-at-the-same-phase-as-update-listeners/8113)
  - At Replit, we have this pattern which is used in a lot of our plugins
  - postUpdate is helpful in a lot of situations. It enables you to make update listeners that have internal state, without using something like closures.
  - For us, it’s often needed because an extension needs to manage some part of the editor’s state, but that management logic just can’t go into something like a StateField.
  - 🌰 This is our most common use case, e.g. our inline AI suggestions use this. Most of the suggestion state is in a StateField, but most of the logic for updating that field lives in a view plugin because that’s the only reasonable place to do asynchronous requests.
  - 🌰 Another use case for us is updating things outside the editor, which then may have reactive effects which cause editor dispatches. It is desirable to avoid this entirely, but for our React-inside-of-CodeMirror library, we definitely needs this, or at least workarounds similar to this.
  - We could do something like `queueMicrotask(() => view.dispatch({ ... })` instead of using an update listener, but this has issues with making view updates sort of slightly asynchronous. 
  - if you called view.dispatch, and then immediately accessed view.state afterwards, that state won’t yet reflect anything queued up by queueMicrotask yet. 
  - Using update listeners avoids this, by basically letting a single dispatch turn into multiple dispatches.
  - So, our request here is pretty simple: add a method very similar to update that runs after update and only when it is safe to do dispatches to the view, just like update listeners. The only real drawback I can think of to adding this method is maybe confusion about what method to use when learning the API, and the possibility of infinite update loops. The latter is already possible with update listeners, so IMO it’s fine.

- 👷 In my own code I’ve been pretty successful at avoiding this pattern where a dispatch immediately triggers another dispatch. 
  - Cascading updates are a bit wasteful, in that they run through the view update logic multiple times for what should be an atomic update. 
  - You can often set things up so that the state update plans the asynchronous actions, and a plugin update method actually activates/schedules them, without updating the state. 
  - Or in some cases you can dispatch multiple transaction at once by passing them to dispatch as an array.
  - Note that even though the code after the dispatch would see the updated state if you had this feature, the update listeners or postUpdate hooks will have situations where the update they are looking at is not actually the most recent update anymore, because another such listener dispatched a transaction. I sort of feel that doing this kind of cascading dispatch asynchronously might be less error-prone than doing it synchronously.
- I spent a lot of effort trying to make it so that the system can avoid the imperative-cascade-of-updates pattern, since that leads to a lot of wasted CPU work and subtle bugs around state inconsistency and update timing. I’m aware that this can be a hard system to fit some types of features into. I do think it’s worth doing anyway, though.

- You can usually avoid it, and you should if you can. But it’s still useful for us. It feels like a missing lifecycle method with view plugins. I will say not every use case we have for this is just about dispatching.

- I’d say you clearly would want to save information about the cursor you are following in a state field. Where else are you storing it?
  - The selected cursor is just a prop in the view plugin’s class. It really could be in a state field, but doing this as plugin instance property is much more obvious than doing as stateField
  - what should be in a state field versus something internal to the plugin is sometimes hard to determine.
# discuss-stars
- ## 

- ## 

- ## [Toggling Extensions - discuss. CodeMirror _202207](https://discuss.codemirror.net/t/toggling-extensions/4667)
  - I want to provide editor settings to a user
  - I understand creating compartments and reconfiguring those compartments, but what’s the best way to trigger reconfiguration based on outside user input?
  - Is there a better way to dispatch an update to a compartment based on an outside change?
  - I don’t like using `ViewPlugin` in this way, but that’s the only way I’ve found that I can both listen to an effect and asynchronously send a view.dispatch. Seems like this is pretty inefficient for a dozen settings.
  - `EditorState.transactionExtender` doesn’t allow async, the effect change has to be done right away. It also doesn’t work for multiple settings at once. It only seems to allow one transactionExtender to change the effects, overriding all the others

# discuss-ext-showcase
- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## [CM6: Dynamically change extensions based on state field - discuss. CodeMirror](https://discuss.codemirror.net/t/cm6-dynamically-change-extensions-based-on-state-field/2941)
- You need to reconfigure them, probably using a labeled extension
- I’m also looking for a way to do this. It seems like the dispatch effect → statefield update → facet combine chain is working fine, but there isn’t a transaction after the facet has recalculated, so there’s nothing for the transaction extender to process, so it never gets to dispatch a new effect to reconfigure a compartment containing the theme.
  - The editor configuration cannot depend on facets—that would be nice to have, but I found it pretty much impossible to implement in a reasonable way. So you’ll have to notice the conditions you’re interested in elsewhere, for example in a view plugin, and fire a new transaction when the configuration has to change.
