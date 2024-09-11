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
# discuss-async-plugin/ext
- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## [CM6 StreamParser - v6 - discuss. CodeMirror _202101](https://discuss.codemirror.net/t/cm6-streamparser/2842)
  - I’m noticing that there’s a collection of “CodeMirror 5 modes” which uses the StreamParser extension 
  - In my understanding, this acts as some kind of shim to port existing CM5 modes to CM6 with minimal changes.
  - is it meant to be generally usable and long-term supported?
  - First, I’ve made a fork of StreamParser to support lookAhead because apparently the old markdown parser uses that. It’s probably not great for performance though.
- Yes. But it has some limitations—for example it doesn’t support nesting modes, and won’t emit proper syntax trees that, for example, the code folding can work with. If your mode descends from the old GFM mode (which is a wrapper around the old Markdown mode), then it is probably not going to be easy to port to this system. I have plans to make the new Lezer-tree-emitting CommonMark parser extensible, but that hasn’t been a priority so far.
- 
