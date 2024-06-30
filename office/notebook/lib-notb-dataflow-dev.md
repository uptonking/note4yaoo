---
title: lib-notb-dataflow-dev
tags: [dataflow, lib, notebook]
created: 2021-05-14T17:34:46.937Z
modified: 2024-06-30T03:18:40.809Z
---

# lib-notb-dataflow-dev

# guide

# codebase
- src/content/core.js由src/client/core.js通过esbuild压缩输出esm，compile和run两种任务都会用到

## compileNotebook

- 简单ojs文件的compile输出有5个文件
  - sha.js为 unofficial-compiler 编译输出的文件
  - core.js是从src/content/core.js复制到输出目录
  - index.js为动态生成的文件，内容简单 `export {default} from "./${sha}.js"; `
  - stdlib.js为简单复制或生成的附加stdlib.js
  - index.html为内置的默认预览页面

```JS
// 编译ojs的流程的入口
async function compileNotebook(inPath, output, options) {
  const { treeShake = null, bundle = true } = options;
  // 对于默认的简单场景，执行这里就返回结束了！！！
  if (bundle) return compileBundle(inPath, output, options);

  // 后面默认不会执行

  const source = readFileSync(inPath, "utf8");
  const compiled = compileSingleNotebook(source, treeShake);
  writeFileSync(output, compiled, "utf8");
}
```

## runServer
