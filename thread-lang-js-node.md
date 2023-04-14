---
title: thread-lang-js-node
tags: [js, lang, nodejs, thread]
created: 2021-07-29T15:44:58.716Z
modified: 2022-12-19T01:48:01.974Z
---

# thread-lang-js-node

# discuss

- ## 

- ## Trying Node.js test runner: Gleb Bakhmutov examines capabilities of new built-in test runner that became stable from Node.js v20
- https://twitter.com/forweb_en/status/1646587007399854081

- ## Node v18 now has compilation of a Node.js script into a single-executable application using `npx postject` .
- https://twitter.com/karlhorky/status/1646421904205463554
- Any idea if they fixed Node's `fetch` leaking?g

- ## An experimental API for command-line argument parsing landed in @nodejs v18.3.0 - the `util.parseArgs` method. Very cool 👌 
- https://twitter.com/simonplend/status/1532304908585779201
  - intended for developers of simple CLI tools, ad-hoc scripts, deployed Node.js applications, and learning materials.

- ## Node.js now has a built-in test runner
- https://twitter.com/rauschma/status/1516456272215826432
  -  import test from 'node:test'; 
  -  import * as assert from 'assert/strict'; 

- ## Node.js: Best way for an app to run itself from the current(!) source on disk?
- https://twitter.com/rauschma/status/1420839210387394564
  - One option: start a new Node.js instance via child_process.execSync().
- Use case: A Node.js script runs for a long time, watches the file system to detect if its own code is changed and then runs itself (recursively).
  - Slightly weird, but makes sense in the context of static site generation.
- You're talking hot reload? There are tools that will do that for you already - just use one of them.
- If using an external tool is ok I'd recommend nodemon, or, I have to mention it, monex (https://github.com/fabiospampinato/monex). 
  - Otherwise spawning a child (of monex) should work. If you need to talk to the child I can recommend jayson for ipc 

- ## I used `fs·watch()` and found out that it always reports two changes whenever I save a file in VS Code. 
- https://twitter.com/rauschma/status/1420739486892191744
  - Consensus on the web seems to be: Avoid it and use other libraries that fix its issues.
- `fs.watch()` is not wrong, like most modern editors, VSCode uses “safe” or “atomic” writes, which do more than one IO operation to save a file (save to temp file, then rename to overwrite original file).
Using another library that abstracts this is useful, though.
- I've written a little comparison between that and chokidar/nsfw/node-watch in the readme too.
  - I'm saying that my package isn't, chokidar is, and nsfw is probably in the middle. It is pretty vague, but chokidar has 1000000x more downloads than mine, I'm basically the only person using mine, so I think that's potentially a significant downside that should be highlighted.
