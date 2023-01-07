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
// rimraf(f, [opts], callback); On Node 14+ you can use

import fs from 'fs/promises';

async function main() {
  await fs.rm(myDir, { recursive: true, force: true });
}
```
