---
title: lang-js-webpack-dev-error
tags: [error, rspack, toolchain, webpack]
created: 2023-12-25T19:31:27.612Z
modified: 2024-01-02T07:52:35.676Z
---

# lang-js-webpack-dev-error

# guide

# done

# errors

- ## 

- ## 

- ## 

- ## 

- ## [Webpack: Bundle.js - Uncaught ReferenceError: process is not defined - Stack Overflow](https://stackoverflow.com/questions/41359504/webpack-bundle-js-uncaught-referenceerror-process-is-not-defined)

```JS
// webpack.config.js
const webpack = require('webpack')
const dotenv = require('dotenv')

// this will update the process.env with environment variables in .env file
dotenv.config();

module.exports = {
  //...
  plugins: [
    // ...
    new webpack.DefinePlugin({
      'process.env': JSON.stringify(process.env)
    })
    // ...
  ]
  //...
}

// Access environment variables in your source code:
alert(process.env.NODE_ENV)
```

- ## [WARNING in DefinePlugin Conflicting values for 'process.env. NODE_ENV'](https://github.com/nrwl/nx/issues/7924)
- Turns out Webpack's mode parameter sets process.env. NODE_ENV via DefinePlugin [0]. So, if you use both mode: 'development' and an instance of DefinePlugin, process.env. NODE_ENV can get set with conflicting values...
