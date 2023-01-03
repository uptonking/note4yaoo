---
title: lib-search-database-api
tags: [api, database, search]
created: 2023-01-03T14:53:27.909Z
modified: 2023-01-03T14:53:44.738Z
---

# lib-search-database-api

# guide

- 返回值类型改为cursor
# database-search-api

## RxDB search based on search-index

> 异步

```JS
import { addRxPlugin } from 'rxdb';
import rxdbSearch from 'rxdb-search';

addRxPlugin(rxdbSearch);

// `collection.search` is just a shortcut/an alias to `si.QUERY` using just the AND operator, that accepts a string as the `query` parameter.
const { RESULT, RESULT_LENGTH } = await collection.search(query: string, siQUERYoptions ? : {});

// This is a costly operation and it should be done only once. 
// Indexes add themselves up afterwards when new documents are added.
const ids = ['id1', 'id2'];
await collection.index(ids);
```

## pouchdb-quick-search using lunr.js

> 异步

```JS
var pouch = new PouchDB('myDb');
var doc = { _id: 'myDoc', title: "Guess who?", text: "It's-a me, Mario!" };

pouch.put(doc).then(() => {
  return pouch.search({
    query: 'mario',
    fields: ['title', 'text'],
    include_docs: true,
    highlighting: true
  });
}).then((res) => {
  console.log(res.rows[0].doc.text); // "It's-a me, Mario!"
  console.log(res.rows[0].highlighting); // {"text": "It's-a me, <strong>Mario</strong>!"}
});
```

## full-text search standalone or with Loki

> 纯内存，同步

```typescript

FullTextSearch.register(); // add fts in common module

db = new Loki("MyDB"); // get fts from common module
coll = db.addCollection<User>("User", {fullTextSearch: [{field: "name"}]});

coll.insert([  {name: "quark", id: 1} ]);

let query: Query = {query: {type: "fuzzy", field: "name", value: "quak", fuzziness: 1}};
  expect(coll.find({"$fts": query}).length).toBe(3);
```

## yunodb

```JS
const cursor = db.search('tortoise', (err, results) => {
  if (err) throw err

  // first 50 results
  console.log(results)

  cursor.next((err, results) => {
    // next page in here
  })
})
```
