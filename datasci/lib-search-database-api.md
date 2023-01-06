---
title: lib-search-database-api
tags: [api, database, search]
created: 2023-01-03T14:53:27.909Z
modified: 2023-01-03T14:53:44.738Z
---

# lib-search-database-api

# guide

- 自动索引 vs 单独索引
  - 自动索引使用更方便
  - 单独索引可扩展性更强

- 添加索引的时机，insideInsert要具体到insert前或后
  - 入库前，pre insert，如loki
  - 入库后, post insert，如rxdb/yunodb
  - 搜索时, inside search，如pouchdb

- roadmap
  - 返回值类型改为cursor
# database-search-api

## RxDB search based on search-index

> 支持单独添加索引和insert时自动索引，postInsert, 异步搜索

```JS
// https://github.com/doriandrn/rxdb-search

import { addRxPlugin } from 'rxdb';
import rxdbSearch from 'rxdb-search';

addRxPlugin(rxdbSearch); // add search plugin, tree shakable

// 在普通insert的postInsert钩子中自动添加索引，bulkInsert没有钩子需要手动添加索引
await collection.insert(doc);

// `collection.search` is just a shortcut/an alias to `si.QUERY` using just the AND operator, that accepts a string as the `query` parameter.
const { RESULT, RESULT_LENGTH } = await collection.search(query: string, siQUERYoptions ? : {});

// This is a costly operation and it should be done only once. 手动添加，且只指定id
// Indexes add themselves up afterwards when new documents are added.
const ids = ['id1', 'id2'];
await collection.index(ids);

// under the hood, 第2个参数是series/parallel
// https://rxdb.info/middleware.html
myRxCollection.postInsert(function addIndex(plainData, rxDocument){
si.PUT()
}, true);
```

## pouchdb-quick-search using lunr.js

> 无需单独添加索引，insideSearch, 异步搜索

```JS
// https://github.com/pouchdb-community/pouchdb-quick-search

var pouch = new PouchDB('myDb');
var doc = { _id: 'myDoc', title: "Guess who?", text: "It's-a me, Mario!" };

pouch.put(doc).then(() => {
  // 在search方法中才开始添加索引
  return pouch.search({
    query: 'mario',
    fields: ['title', 'text'],
    include_docs: true,
    highlighting: true,
    build: true // To avoid slow performance, you can explicitly tell the search plugin to build up the index 
  });
}).then((res) => {
  console.log(res.rows[0].doc.text); // "It's-a me, Mario!"
  console.log(res.rows[0].highlighting); // {"text": "It's-a me, <strong>Mario</strong>!"}
});
```

## full-text search standalone or with Loki

> 支持单独添加索引和insert时自动索引，触发时机在preInsert后Insert前，纯内存同步操作

```typescript
// https://github.com/LokiJS-Forge/LokiDB/blob/master/packages/full-text-search/spec/generic/full_text_search.spec.ts

FullTextSearch.register(); // add fts to common module

db = new Loki("MyDB"); // get fts from common module
coll = db.addCollection<User>("User", {fullTextSearch: [{field: "name"}]});

coll.insert([  {name: "quark", id: 1} ]);

let query: Query = {query: {type: "fuzzy", field: "name", value: "quak", fuzziness: 1}};
expect(coll.find({"$fts": query}).length).toBe(3);
```

## yunodb

> 无需单独添加索引，postInsert，异步搜索，返回cursor

```JS
// https://github.com/blahah/yunodb

db.add(docs, { text: trim }, doneAdding);

const cursor = db.search('tortoise', (err, results) => {
  if (err) throw err

  // first 50 results
  console.log(results)

  cursor.next((err, results) => {
    // next page in here
  })
})
```
