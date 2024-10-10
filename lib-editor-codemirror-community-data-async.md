---
title: lib-editor-codemirror-community-data-async
tags: [codemirror, community, data-sync]
created: 2024-08-11T03:32:40.184Z
modified: 2024-08-11T03:35:16.823Z
---

# lib-editor-codemirror-community-data-async

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 🤔🔀 [Should dispatched transactions be added to a queue? - v6 _202206](https://discuss.codemirror.net/t/should-dispatched-transactions-be-added-to-a-queue/4610)
- I was slightly surprised to find that the dispatch method doesn’t put transactions on a queue for processing.
  - While it would be easy enough to add a queue in a custom dispatch function, I’m wondering whether that would be a bad idea for any reason, particularly in a way that explains why it isn’t implemented as a queue by default.

- 👉 When creating a transaction, you are basing it on the current editor state. It would often not make any sense anymore when applied from a different state. Also dispatching transactions is synchronous, so a queue seems needless complexity.

- Would it not be correct to say that whenever something asynchronous happens which ends with a call to view.dispatch, there’s always a chance that the view will already be processing an update at that time, which would result in an error being thrown?
  - The way to write asynchronous stuff that dispatches is to do the async action, and then figure out how it applies to the current state. This may in some cases involve mapping a position known at the start of the action forward through updates (which is why it is convenient to define this kind of stuff as a view plugin).

- 🤔 I think I see the flaw in my reasoning - thanks for helping to work through it. It’s because the transaction processing is synchronous, any asynchronous code which calls view.dispatch will be run from the microtask queue and can only happen once the current transaction processing has finished.
  - In which case it’s only calls to view.dispatch that are triggered by updates within a CodeMirror cycle that we need to worry about, and these can be wrapped in setTimeout (or, perhaps, queueMicrotask).
# discuss-async-plugin/ext
- ## 

- ## 

- ## 
# discuss
- ## 

- ## 🌰 [async StateField.define provide extension - v6 - discuss. CodeMirror _202306](https://discuss.codemirror.net/t/async-statefield-define-provide-extension/6731)
  - I have a StateField extension with async value
  - 可行的方案是在viewPlugin.update中执行异步逻辑后再更新stateField

- ## [CM6 StreamParser - v6 - discuss. CodeMirror _202101](https://discuss.codemirror.net/t/cm6-streamparser/2842)
  - I’m noticing that there’s a collection of “CodeMirror 5 modes” which uses the StreamParser extension 
  - In my understanding, this acts as some kind of shim to port existing CM5 modes to CM6 with minimal changes.
  - is it meant to be generally usable and long-term supported?
  - First, I’ve made a fork of StreamParser to support lookAhead because apparently the old markdown parser uses that. It’s probably not great for performance though.
- Yes. But it has some limitations—for example it doesn’t support nesting modes, and won’t emit proper syntax trees that, for example, the code folding can work with. If your mode descends from the old GFM mode (which is a wrapper around the old Markdown mode), then it is probably not going to be easy to port to this system. I have plans to make the new Lezer-tree-emitting CommonMark parser extensible, but that hasn’t been a priority so far.
- 
