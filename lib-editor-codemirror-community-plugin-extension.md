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

- ## 
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
