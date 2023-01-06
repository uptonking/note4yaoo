---
title: lib-db-leveldb-community-level-like
tags: [community, level-like, leveldb, web]
created: 2022-12-18T09:56:37.193Z
modified: 2022-12-31T18:05:42.830Z
---

# lib-db-leveldb-community-level-like

# guide

# discuss
- ## 

- ## [fix: allow empty prefix option by achingbrain](https://github.com/Level/level-js/pull/184)
- To get around that - and be compatible with how leveldown behaves - level-js@5 converts string keys to binary keys before passing them to IndexedDB, so that string and binary keys are treated as the same. I.e. it effectively no longer sorts by type.

- ## [level.v8: Streams have moved](https://github.com/Level/level/blob/master/UPGRADING.md#streams-have-moved)
- Node.js readable streams must now be created with a new standalone module called `level-read-stream` rather than database methods like `db.createReadStream()` . 
  - For browsers you might prefer `level-web-stream` which does not require bundling the `buffer` or `readable-stream` shims. 
  - 👉🏻 Both `level-read-stream` and `level-web-stream` can be used in Node.js and browsers. 
  - The former is significantly faster (also compared to level@7, thanks to a new nextv() method on iterators). 
  - The latter is a step towards a standard library for JavaScript across Node.js, Deno and browsers.

- ## [Bite the bullet and remove WriteStream completely? · Level/levelup](https://github.com/Level/levelup/issues/199)

- levelup: db.createReadStream([options])
  - Returns a Readable Stream of key-value pairs.
  - By default it will stream all entries in the underlying store from start to end. 
- ❓ What happened to `db.createWriteStream`?
  - it has been removed in order to provide a smaller and more maintainable core.
  - The main driver for this was performance. While db.createReadStream() performs well under most use cases, db.createWriteStream() was highly dependent on the application keys and values. Thus we can't provide a standard implementation and encourage more write-stream implementations to be created to solve the broad spectrum of use cases.

- WriteStream is only there for the sake of symmetry but that's not a great reason in itself if there are better reasons for it not to be there. 
  - I think we're starting to realise that there are different use-cases that require different implementations and we're already seeing some alternative implementations so why not set them free to coexist and compete in user-land?

- ## [Decide on naming of modules · Level/abstract-level](https://github.com/Level/abstract-level/issues/6)
- With abstract-level, there is no "down" or "up" anymore. For example, memdown does not have to be wrapped with levelup. This means level-mem could just do module.exports = require('memdown') to export (largely) the same functionality as before.

- ## [LevelUp, LevelDown, LevelDB_201811](https://blog.elsdoerfer.name/2018/11/10/levelup-leveldown-leveldb/)
- This ecosystem is super confusing. Here is the low-down:
  - LevelDB is a (K/V-Store) database
  - leveldown is a NodeJS binding.
  - levelup is another NodeJS module, which wraps leveldown. However, it allows leveldown to be replaced with another backend.
- In this way, you can use a single library and API – levelup – but with all kinds of different storage backends, from Redis, to SQL databases.
