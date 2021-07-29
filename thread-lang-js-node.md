---
title: thread-lang-js-node
tags: [js, lang, node, thread]
created: '2021-07-29T15:44:58.716Z'
modified: '2021-07-29T15:45:36.816Z'
---

# thread-lang-js-node

# discuss

- ## 

- ## 

- ## 

- ## 

- ## 

- ## 

- ## I used `fs·watch()` and found out that it always reports two changes whenever I save a file in VS Code. 
- https://twitter.com/rauschma/status/1420739486892191744
  - Consensus on the web seems to be: Avoid it and use other libraries that fix its issues.
- `fs.watch()` is not wrong, like most modern editors, VSCode uses “safe” or “atomic” writes, which do more than one IO operation to save a file (save to temp file, then rename to overwrite original file).
Using another library that abstracts this is useful, though.
- I've written a little comparison between that and chokidar/nsfw/node-watch in the readme too.
  - I'm saying that my package isn't, chokidar is, and nsfw is probably in the middle. It is pretty vague, but chokidar has 1000000x more downloads than mine, I'm basically the only person using mine, so I think that's potentially a significant downside that should be highlighted.
