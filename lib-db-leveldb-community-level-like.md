---
title: lib-db-leveldb-community-level-like
tags: [community, level-like, leveldb, web]
created: 2022-12-18T09:56:37.193Z
modified: 2022-12-31T18:05:42.830Z
---

# lib-db-leveldb-community-level-like

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## [How does `Leveldb` compare with `Redis` or Riak or Tokyo Tyrant? - Stack Overflow](https://stackoverflow.com/questions/6101402/how-does-leveldb-compare-with-redis-or-riak-or-tokyo-tyrant)
- Redis is a server, while Leveldb is "a library that implements a fast persistent key-value store". 
  - Therefore, with Redis, you have to poll the server. 
  - With Leveldb, the database is stored on disk, making it a lot slower than Redis, which is stored in memory.
- Leveldb is only offers key/store. 
  - Redis has this as well, but also has a lot more functions and features

- [how does it compare to Redis?](https://news.ycombinator.com/item?id=14336973)

- Badger is designed to store data on disk (like RocksDB or LevelDB), while Redis is an in-memory storage which can't store data sets larger than memory.
  - You can store Redis on disk too. Not that you gain anything from doing so as persistence can be better achieved by clustering and I've never ran into issues where memory was a limiting factor, even with millions of records in Redis.
# discuss-foundationdb
- ## 

- ## 

- ## [How FoundationDB works and why it works (2021) | Hacker News_202309](https://news.ycombinator.com/item?id=37552085)
- 
- 
- 
- 
- 

# discuss-rocksdb
- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## 

- ## [如何看待基于redis实现的分布式锁redlock，以及kleppmann对redlock的分析？ - 知乎](https://www.zhihu.com/question/41395416/answers/updated)
- kleppmann是在理论上分析，而az更多在工程实现上反驳，二者纬度上不太一致，很难判断谁更有道理。
- 考虑到一个正确的分布式锁是很难有简单的实现，在redlock没有理论证明+实际数据支持之前，只能暂定它是一个分布式锁的简略实现。
  - 所以目前redlock（已有大量第三方语言实现）可以用在尽力锁场景（on a best-effort basis）下，锁偶尔失效也没有致命影响，这其实也挺契合redis的使用目标
- 我觉得就像kleppmann说的，如果仅要求高效，那一个节点简单的实现就够了。如果要求正确性高还是用现成的zk吧

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

- ## 🆚️ [LevelUp, LevelDown, LevelDB_201811](https://blog.elsdoerfer.name/2018/11/10/levelup-leveldown-leveldb/)
- This ecosystem is super confusing. Here is the low-down:
  - LevelDB is a (K/V-Store) database
  - leveldown is a NodeJS binding.
  - levelup is another NodeJS module, which wraps leveldown. However, it allows leveldown to be replaced with another backend.
- In this way, you can use a single library and API – levelup – but with all kinds of different storage backends, from Redis, to SQL databases.
