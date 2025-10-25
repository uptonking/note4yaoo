---
title: cli-scripts-nodejs
tags: [cli, nodejs, scripts]
created: 2023-01-07T15:58:31.377Z
modified: 2023-01-07T15:59:24.071Z
---

# cli-scripts-nodejs

# guide

# nodejs-scripts

```JS
// [Why is __dirname not defined in node REPL? - Stack Overflow](https://stackoverflow.com/questions/8817423/why-is-dirname-not-defined-in-node-repl)

import { fileURLToPath } from 'url';
import { dirname } from 'path';

const __filename = fileURLToPath(
  import.meta.url);
const __dirname = dirname(__filename);
```

```JS
// rimraf(f, [opts], callback); On Node 14+ you can use

import fs from 'fs/promises';

async function main() {
  await fs.rm(myDir, { recursive: true, force: true });
}
```

```JS
// lorem ipsum https://stackoverflow.com/questions/34123706

function gentxt(n = 40) {
  const words = ["The sky", "above", "the port", "was", "the features of", "tuned", "to", "an active channel", ".", "All", "this happened", "more or less", ".", "I", "MacOS", "had", "the story", "bit by bit", "from various people", "and", "as generally", "happens", "in such cases", "each time", "it", "was", "a different story", ".", "It", "was", "Apple", ",", "a pleasure", "to", "burn", "running", "Two cats", "are playing"];
  let sentence = "";
  while (n--) {
    sentence += words[Math.floor(Math.random() * words.length)] + " ";
  }
  return sentence;
}
```
