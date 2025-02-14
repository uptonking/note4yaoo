---
title: lang-js-test-mocha-chai
tags: [chai, lang-js, mocha, testing]
created: 2024-01-17T04:00:37.371Z
modified: 2024-01-17T04:01:01.983Z
---

# lang-js-test-mocha-chai

# guide

# dev-mocha

## cli

```shell
mocha --config rc.config.cjs
```

- [How to require multiple modules?](https://github.com/mochajs/mocha/issues/2250)
  - `--require module --require module2 --require another_module`

- [Passing Flags to Node.js](https://github.com/mochajs/mocha/issues/3060)
  - The flags Mocha will pass to Node are in `bin/mocha` (whereas Mocha's own flags are in `bin/_mocha`). 
  - `node --experimental-modules node_modules/mocha/bin/_mocha \"test/**/*_test.js\"`
- [Preserve symbolic link in mocha js - Stack Overflow](https://stackoverflow.com/questions/61132438/preserve-symbolic-link-in-mocha-js)
  - `node --preserve-symlinks ./node_modules/.bin/mocha --opts mocha.opts --timeout 30000 \"test/unit/**/*.js\"`

## config

- By default, mocha looks for the glob `"./test/*.{js,cjs,mjs}"`.
  - If you want to include subdirectories, use `mocha --recursive "./spec/*.js"`.
  - the following is the same as passing --recursive, use `mocha "./spec/**/*.js"`

- You should always quote your globs in npm scripts

- Mocha will also merge any options found in package.json into its run-time configuration

## esm

- NODE. JS NATIVE ESM SUPPORT
  - New in v7.1.0
  - either ending the file with a `.mjs` extension, or, if you want to use the regular `.js` extension, by adding `"type": "module"` to your package.json
- LIMITATIONS
  - Watch mode does not support ES Module test files
  - Custom reporters and custom interfaces can only be CommonJS files
  - Configuration file can only be a CommonJS file (.mocharc.js or .mocharc.cjs)

- [Support --require of ESM_202006](https://github.com/mochajs/mocha/pull/4304)
  - As of v7.3.0, Mocha supports `--require` for [NodeJS native ESM](#nodejs-native-esm-support). There is no separate `--import` flag.

- [typescript with ts-node and ESM support · mochajs/mocha-examples](https://github.com/mochajs/mocha-examples/issues/47)
  - mocha --loader=ts-node/esm/transpile-only --experimental-specifier-resolution=node --extensions ts, tsx 'tests/**/*.test.ts' --reporter spec --timeout 10000

## mocha-browser

- Every release of Mocha will have new builds of `./mocha.js` and `./mocha.css` for use in the browser.
# dev-chai

```JS
import { assert } from 'chai';
import { expect } from 'chai';

import { should } from 'chai';
should(); // Modifies `Object.prototype`
```

# more

# discuss-jest

- ## 

- ## 

- ## A bit weird how Jest doesn't seem to support parallelizing test execution at the "describe" level other than at the file level 🤔 Maybe I can't find the option for it?
- https://x.com/fabiospampinato/status/1888601040741937476
  - It seems kind of a worst of both world situation, enough parallelization to complicate the implementation, not enough parallelization to actually take full advantage of it.

- I see so many tests in the wild are going to break if this change will happen
  - It would be opt-in presumably, but not having the option at all seems weird for Jest.
# discuss-mocha
- ## 

- ## 

- ## 
