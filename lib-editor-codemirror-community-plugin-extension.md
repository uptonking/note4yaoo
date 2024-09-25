---
title: lib-editor-codemirror-community-plugin-extension
tags: [codemirror, community, extensions, plugin-system]
created: 2024-08-11T06:42:26.160Z
modified: 2024-08-11T06:42:41.903Z
---

# lib-editor-codemirror-community-plugin-extension

# guide

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
