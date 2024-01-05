---
title: lib-db-feat-jsonb-bson
tags: [binary, bson, encoding, format, jsonb, serdes]
created: 2024-01-01T04:11:29.771Z
modified: 2024-01-01T04:12:09.000Z
---

# lib-db-feat-jsonb-bson

# guide

- tips
  - pg-jsonb和sqlite-jsonb的实现细节是不同的, bson提供了格式说明
# dev

# blogs

## [What I think of jsonb_201403](https://pgeoghegan.blogspot.com/2014/03/what-i-think-of-jsonb.html)

- Jsonb is a new datatype for Postgres. 
  - It is distinct from the older json datatype in that its internal representation is binary, and in that it is internally typed. It also makes sophisticated nested predicates within queries on jsonb indexable.
- Jsonb is emphatically(着重的，强调的) not like the BSON format used by MongoDB. That format accepts input in such a way as to be backwards compatible with JSON, but I believe that BSON isn't really a practical interchange format, because the software development community at large is presumably disinclined(使人不愿意，使人不乐意) to buy into an interchange format that as yet is not described by any RFC, or any communiqué of a recognized standards body. 
  - In contrast, jsonb is a datatype that will only ever output valid textual JSON, and will only ever accept valid textual JSON (subject to the aforementioned obscure and practically irrelevant restrictions, and the caveat on automatically normalizing duplicate-keyed pairs within the same object). 
  - Jsonb also imposes an internal ordering on object pairs. Again, this is all anticipated and allowed for by the JSON RFC.

- it's important to note that the protocol or on-disk binary representation of jsonb is an implementation detail; we're not in competition with BSON, and this isn't a new standard. It's just a new Postgres datatype, with new indexing capabilities.
  - I think it's notable that BSON doesn't have a JSON-style universal number type. It has 32-bit and 64-bit integer types, and double precision 64-bit IEEE 754 floating point numbers. 

## [How FerretDB stores BSON in JSONB | FerretDB Blog_202211](https://blog.ferretdb.io/pjson-how-to-store-bson-in-jsonb/)

- At FerretDB, we are converting MongoDB wire protocol queries into SQL, to store information from BSON to PostgreSQL. 
  - To achieve this, we created our own mapping called PJSON which translates MongoDB's BSON format into PostgreSQL's JSONB.
- BSON holds a collection of field name/value pairs which is called a document. 
  - It contains length information allowing serializer/deserializer to utilize it for the performance benefit. Additionally, it preserves the order of the fields. 
  - BSON also supports additional data types such as DateTime and binary.
- At FerretDB, we use PostgreSQL as a database engine and we store JSON data in JSONB data type. In light of this, we need to store BSON equivalent information in JSON format without losing type information.

## 🆚️ [Postgres vs. MongoDB for Storing JSON Data — Which Should You Choose?_202110](https://community.sisense.com/t5/knowledge/postgres-vs-mongodb-for-storing-json-data-which-should-you/ta-p/111)

- JSON is unstructured, flexible, and readable by humans
  - JSON does, however, lack indexing — and the JSONB data format was created to tackle this problem. 
  - JSONB stores data in a binary format, instead of a simple JSON blob. Data input is a bit slower, but processing becomes a lot faster since the data doesn’t need to be re-parsed.
- Postgres and MongoDB both have functions for JSON and JSONB data storage (although MongoDB calls the latter “BSON”).

- There are differences
  - MongoDB limits its BSON format to a maximum of 64 bits for representing an integer or floating point number. 
    - Postgres’s JSONB format isn’t limited.
  - Postgres provides data constraint and validation functions, which help to ensure JSON documents are more meaningful. E.g. It stops you from storing alphabetical characters when only numerical values make sense.
  - MongoDB offers automatic database sharding, for easy horizontal scaling of JSON data storage; Postgres installation scaling is usually vertical. You can scale Postgres horizontally, but this tends to be trickier or takes third-party help.
  - MongoDB also lets you increase your write throughput by deferring writing to disk. You might lose some data that way, but it can be good for users who are le ss worried about persisting their data.

## 🆚️ [Jsonb: few more stories about the performance · Erthalion's blog_201712](https://erthalion.info/2017/12/21/advanced-json-benchmarks/)

- The main conclusion is that this is a damn interesting topic to research and I’m still continuing to do so
- Another interesting conclusion is that basically all the performance differences I’ve shown above were mostly caused by databases themselves, not by the way how they handle documents. 
# discuss-stars
- ## 

- ## 

- ## 🛋️🌰 [Binary JSON format on-disk or in-memory - Couchbase Server - Couchbase Forums_202209](https://www.couchbase.com/forums/t/binary-json-format-on-disk-or-in-memory/34436)
  - I am working on a research project comparing several document-oriented databases. MongoDB has BSON, ArangoDB has VelocyPack, Postgresql has Jsonb, … 
  - Does Couchbase also have its own binary format to work with JSON documents, on disk or in memory?
- Data is typically stored as plain JSON, though binary documents can also be stored (though not manipulated).

- When Couchbase stores a JSON document, does it store the JSON text (possibly Snappy-compressed), or does it use some other binary JSON format internally?
  - AFAIK, it does depend on the bucket type, with Couchbase buckets being implemented with
- 💡 Certainly when couchstore is the storage, a document is just compressed using snappy, no other “re-formatting” occurs. So if a JSON document is written, it is just that JSON document stored after being snappy compressed, if a binary value is written, it is just that binary value stored after being snappy compressed.
# discuss-bson-binary
- ## 

- ## 

- ## 

- ## [Jsonb: Stories about performance | Hacker News_201712](https://news.ycombinator.com/item?id=15993768)
- 
- 
- 

- ## 💡 [Using PostgreSQL’s JSONB for NoSQL (2019) [video] | Hacker News_202109](https://news.ycombinator.com/item?id=28406334)
- I find this approach incredibly useful if any parts of your data don't have a uniform schema.
  - The one thing you need to look out for is developers putting stuff into JSON that belongs into proper columns. The Postgres JSON support is very powerful, but plain old relational queries are faster and often much easier to write.
  - Also for leftovers when scraping website data. Trendy SPAs usually have JSON endpoints, so I usually use some ID column, maybe timestamp column (to ease incremental syncing later on), some primary content columns, and the whole scraped JSON object is put into a data JSONB column in case some of it is needed in the future. :) Works amazingly.

- I have created an app with such a hybrid approach as the part if the model was very dynamic. The idea was that I would slowly migrate the stable bits to proper columns, but in practice that never happened. Partly also because it is not really broken, and the performance is actually quite good. You can add partial indexes etc to improve where needed.
  - But writing analytycal queries is definitely more complicated so the cost of not having a "normal" data model adds up over time. To allow business analysts to work with the data I endend up creating a a bunch of views om the data without JSONB fields as a quick fix. So though the approach worked, I am not sure I would do it again.

- I'm using the JSON mostly for parts that really have no fixed schema, e.g. fields that vary by customer. The alternative would be something like EAV, and JSON columns are far superior here.
  - Performance is perfectly reasonable with JSON, but there are many more ways to make it slow if you're not careful. Postgres has to read the entire JSON content even if you only access a small part of it, that alone can kill performance if your JSON blobs are large. The lack of true statistics can also be an issue with JSON columns. They're still easily fast enough for many purposes, they just have a few more caveats than plain columns you should be aware of.
- There's some other aspects that are not that intuitive, but also not a big deal once you know them. For example you can use a jsonb_path_ops GIN index to speed up queries for arbitrary keys and values inside your JSONB column
- What you did, in fact, was creating read models specific to use case. This is completely normal and allows one to optimize for different users: app's schema can be different than the one for analytics.

- I noticed a lot of people noting that they enjoy use some hybrid of JSON w/ their SQL. I do the same thing and I think this is an incredibly productive way to manage fast-changing things.
  - One trick I learned along the way is to **apply gzip to your JSON columns**. For us, we got over 70% reduction in column size and query performance actually increased. I presume because it is faster to read fewer IO blocks than more, esp when doing table scans (which you shouldnt but they happen).
  - The only caveat with this is if you want to query against something in the JSON, but I think this is where the balancing act comes into play regarding what is in (compressed) JSON and what is in a column.
- In Postgres you would generally use JSONB columns, those are stored as TOASTs and are automatically compressed. That compression isn't very good, but there is some work on adding other compression algorithms there.
  - PostgreSQL 14 will add lz4 compression for toast data. But if i remember correctly the first ~700 bytes are always stored inline and only the rest is compressed. But i could be wrong on this.

- The performance of JSONB is also surprisingly great. I played around with around 1M rows of data for a project using JSONB, and compared to traditional SQL, the complex queries were 500-800ms slower, which was totally reasonable for the use case.

- Been doing this for years now and it has proven itself to he a great solution. We use a hybrid approach: traditional columns in addition plus an entity/content type JSONB column.
- JSON blob + columns is the recommended approach for handling semi-structured data in ClickHouse. It's easy to add columns on the fly, since you just give the expression to haul out the data using a DEFAULT clause. ClickHouse applies it automatically on older blocks without rewriting them. For new blocks it materializes the data as rows are inserted.

- Had a great win this last week with JSONB. Basically I needed an aggregated materialized view for performance but still have access to the non-aggregated row data. Think aggregate by account ID but the query may access any given month of data for that account. It’s cheating a bit to use a non-relational structure, but the correlated subqueries I had to use before were 20x slower.

- PostgreSQL 14 is currently in beta and adds JSON subscripting

- ## 🛋️ [Fleece: A super-fast, compact, JSON-equivalent binary data format | Hacker News_202312](https://news.ycombinator.com/item?id=38544728)

- https://github.com/couchbase/fleece /303Star/apache2/202312/cpp
  - A super-fast, compact, JSON-equivalent binary data format
  - Its data model is a superset of JSON, adding support for binary values.
  - Very fast to read: No parsing is needed, and the data can be navigated and read without any heap allocation
  - Appendable: Fleece is what's known as a persistent data structure. 

- I went down the rabbit hole of trying to find the best binary JSON-ish format a couple of years ago, it's very interesting to compare their different design choices. Having read the specification, this looks to be a fresh and minimalist take on a binary format, which is great.
  - In general, it seems CBOR won the standardisation and support battle while also being one of the more complex and ambiguous (in terms of the number of ways to encode something) formats. 
  - I think MessagePack is nicer, though I still wish UBJSON caught on.

- How does it compare to: https://msgpack.org/index.html ?
  - It seems to be maybe a bit less compact in terms of absolute number of bytes, but faster to parse. 
  - That is, parsing is just one-pass validation, and then data can be read directly from the buffer without an intermediate structure, with random access. 
  - It also has a notion of "pointer" so you can introduce sharing (a smart-ish encoder might use that to reuse common keys or strings, making the result smaller).

- ## [Amazon open-sources Ion – a binary and text interchangable, typed JSON-superset | Hacker News_201604](https://news.ycombinator.com/item?id=11546098)
- A big problem with Avro, BSON, and many other "binary JSON" formats is that they're not isomorphic(同形的, 同态的) with JSON, they have a bunch of additional stuff added on. There's Avro documents that don't have direct JSON equivalents. Which means that when a human needs to read the data, you have to transform it into some third format.
  - It's a core feature of Ion that the text and binary representations are isomorphic. You can take any Ion binary document and pretty-print it as an Ion text document that is exactly equivalent. You can edit that document and send it into your application, which will be guaranteed to be able to read it. Or you can take your hand-authored text data and transcode it into binary, and know that any Ion application can handle it without any extra effort.

- Wasn't this solved already by the BSON specification - http://bsonspec.org ? Sure this allows you a definition of types, but this could easily be done using standard JSON meta data for each field. I find BSON simpler and more elegant.
- BSON is awful.
  * It doesn't have "true" types in the sense that Ion does. It's basically just a binary serialization of JSON, with extra stuff.
  * Despite being a binary format, it's actually bulkier than JSON in most situations.
  * It removes any semblance of canonicity from many representations. A number, for instance, can potentially be represented by any of at least 3 types (double, int32, and int64).
  * It has signed 32-bit length limits all over the place. Not that I'd want to be storing 2GB of data in a single JSON document either, but it's not even possible to do so with BSON!
  * It requires redundant null bytes in unpredictable places. For instance, all strings must be stored with a trailing null byte, which is included in their length. There's also a trailing null byte at the end of a document for no reason at all.
  * It is unabashedly Javascript-specific, containing types like "JavaScript code with scope" which are meaningless to other languages.
  * It also contains some MongoDB-specific cruft, such as the "ObjectID" and "timestamp" types (the latter of which, despite its name, cannot actually be used to store time values).
  * It contains numerous "deprecated" and "old" features (in version 1.0!) with no guidance as to how implementations should handle them.
- Yes, and not only that. It also inherently insecure, while JSON is together with msgpack the only fast and secure serialization format out there. The problem is the encoding of objects and code without any checksumming, so it can be trivially tampered with, leading to very nice exploits, mostly remotely.
- Most of this comes from BSON also being the internal storage format for a database server. For example, at least the redundant string NULs make it possible to use C library functions without copying, the unpacked ints allow direct dereferencing, etc.

- ## [Universal Binary JSON Specification | Hacker News_201201](https://news.ycombinator.com/item?id=3432759)
- The reason the spec does not explicitly include a binary data type is because Smile and BJSON already do this (as well as BSON if you want to include all the extra types it adds); none of these specifications have been widely adopted with BSON being the most successful only because 10gen's success with Mongo.
- JSON's fast and wide adoption was due to two things: simplicity and compatibility.

- You didn't convinced me. The only reason I need binary encoding for JSON, is to be able to efficiently transfer binary fields. With UBJSON I will need to encode them as BASE64. There are lots of libraries for BSON, so I will continue to use it, even if it's not a pure JSON.

- ## [Son: A minimal subset of JSON for machine-to-machine communication | Hacker News_201712](https://news.ycombinator.com/item?id=15890904)
- CBOR, FlatBuffers, ProtoBuf, MsgPack, BSON - so many better choices. 
  - Please do not make JSON a standard for M2M communication, it's as bad as calling Electron apps "native".
- It's already a standard for M2M communication, unless you see someone writing JSON by hand when doing anything on the web.

- I didn't know CBOR, but it looks similar to BSON and MessagePack, or is there a significant difference?
  - I say that a bit tongue in cheek, but really: BSON has a monstrous amount of basic data types, some of which make very little sense and are very difficult to round-trip through other formats; and MessagePack had crippling basic sanity issues with what-are-bytes-vs-strings in its early history and that's something you simply can't recover from without declaring game over and making a new spec.
  - CBOR has neither of these issues. It's almost completely isomorphic to json, plus supports byte arrays. It's very nice.

- ## 🪶 [JSONB has landed | Hacker News_202312](https://news.ycombinator.com/item?id=38540421)

- > The "JSONB" name is inspired by PostgreSQL, but the on-disk format for SQLite's JSONB is not the same as PostgreSQL's. The two formats have the same name, but they have wildly different internal representations and are not in any way binary compatible.
  - Originally JSONB used only offsets, but that made it incompressible. That held up a PostgreSQL release for some time while they figured out what to do about it.

- Lots of confusion on what JSONB is.
  - To your application, using JSONB looks very similar to the JSON datatype. You still read and write JSON strings—Your application will never see the raw JSONB content. The same SQL functions are available, with a different prefix ( `jsonb_` ). Very little changes from the application's view.
  - The difference is that the JSON datatype is stored to disk as JSON, whereas the JSONB is stored in a special binary format. 
  - With the JSON datatype, the JSON must be parsed in full to perform any operation against the column. With the JSONB datatype, operations can be performed directly against the on-disk format, skipping the parsing step entirely.
  - If you're just using SQLite to write and read full JSON blobs, the JSON datatype will be the best pick. If you're querying or manipulating the data using SQL, JSONB will be the best pick.
- SQLite has a surprisingly small number of types: null, integer, real, text, and blob. That’s it. There is no json data type ! If you are just storing json blobs, then the BLOB or TEXT data types will be the best picks.

- BSON (and others?) seem to have different goals.
  - SQLite's format seems to minimise conversion/parsing (eg. it has multiple TEXT types depending on how much escaping is needed; BSON has one fully-parsed UTF-8 string type). 
  - BSON is more complex: includes many types not supported by json (dates, regexs, uuids...) and has a bunch of deprecated features already.
  - SQLite's on disk-format is something they intend to support "forever", and as with the rest of SQLite, they enjoy pragmatic simplicity.

- AFAIK jsonb is not a specific format, it’s just a generic term for “a json equivalent binary representation”. The sqlite blurb says jsonb is generally smaller than json, but IIRC from when postgres added jsonb postgres’ is generally slightly larger.
- PG's JSONB has a specification (well, inside PG, not a standard), and they won't change it except in backwards compatible ways (or, really, at all).
  - So does sqlite's. An implementation detail, even a necessarily stable one, does not a format make.

- ## 🚀🪶 [SQLite Forum: JSONB has landed_202312](https://sqlite.org/forum/forumpost/fa6f64e3dc1a5d97)
- was there a specific reason to create JSONB instead of using an existing format like CBOR, BJSON, BSON, UBSON? Formats that have existing libraries in several languages.
  - The purpose of SQLite-JSONB is to expose the underlying parse tree for JSON strings, so that the parse can be saved in the database and not need reparsing every time the JSON is used. 
  - This makes some kinds of operations on large JSON strings about 3x faster, according to measurement scripts in the test/json subdirectory of the source tree. In addition to running about 3x faster, SQLite-JSONB also has the interesting property of being about 5 to 10% smaller than text JSON, thus taking up less disk space.
  - SQLite-JSONB is not intended to be an interchange format. It is not intended to be used by any other programming languages. It is not intended to be used by application developers. Application developers should consider JSONB to be an opaque blob. JSONB is an internal format for use by the SQLite implementation only.
- CBOR and UBJSON are even worse than JSON for random access. Containers have optional member counts (much less useful than actual byte sizes), which complicates skipping over an item: you need a stack of incomplete object member counts. To skip over a JSON item, a single integer tracking the container nesting level suffices.
  - CBOR, BJSON, and BSON add extra data types that don't exist in JSON. If you choose an externally specified format, people will expect your code to support the full specification and complain when it doesn't.

- Jens Alfke's Fleece seems to have similar properties to JSONB: very fast to read: No parsing is needed, and the data can be navigated and read without any heap allocation

- ## 🚀🐘 [PostgreSQL: Jsonb has committed | Hacker News_201403](https://news.ycombinator.com/item?id=7457197)
- tl; dr storing json in a way that doesn't mean repeatedly parsing it to make updates

- What's the difference between jsonb and bson? They look so similar to each other...
  - BSON actually was considered as the JSON storage format for PostgreSQL, but was discarded once people figured out that BSON stores `["a", "b", "c"] `as `{0: "a", 1: "b", 2: "c"}` which is just silly.
- jsonb is the name of a data type used in postgres in order to store, index and update JSON. bson is the same used by MongoDB and also made a semi-official standard.

- ## 🆚️✉️ [PostgreSQL: Re: additional json functionality_202311](https://www.postgresql.org/message-id/flat/CAM-w4HMnBpK%3Dg2R%3DzydeXHPKk%2BdQfwHskVCcqc082tVAViu-PA%40mail.gmail.com#59b6ccc048be67573d0d7beaecf96895)
- Both MongoDB and Postgres are very capable of handling JSON. 
  - MongoDB stores JSON using its own invented BSON, while Postgres uses a different JSONB format. 
  - For those interested, there is a lengthy discussion around whether to choose BSON or JSONB in Postgres.
- MongoDB has 2 advantages:
  - Built-in schema validator.
  - Its integration with the Node.js/frontend ecosystem. MongoDB is a favored choice among full-stack developers who commonly utilize Node.

- The world is full of self-describing binary formats: BSON, MessagePack, protobuf, hierarchical H-Store is coming along. 

- 🤔 could we just implement BSON and leave json alone?
  - In short?  No. For one thing, our storage format is different from theirs (better, frankly), and as a result is not compliant with their "standard". That's a reason why we won't use the name BSON, either, since it's a trademark of 10gen
- What is more, it has restrictions which we do not wish to have. 👉🏻 See for example its treatment of numerics.

- 🆚️ Not being super familiar with either BSON or JSONB, what advantages are we gaining from the difference?
- To start with, it doesn't support arbitrary precision numerics. That means that right off the bat it's only accepting a subset of what the JSON spec allows. 

- We have the JSONB/Hstore2 format *now*, and it can go into 9.4.  This makes it inherently superior to any theoretical format.  So any further discussion (below) is strictly academic, for the archives.
- Leaving aside that we don't want to implement 10gen's spec (because of major omissions like decimal numbers), the fundamental issue with binary-update-in-place is that nobody (certainly not 10gen) has devised(想出，设计) a way to do it without having ginormous amounts of bloat in value storage.  
  - The way BSON allows for binary-update-in-place, as I understand it, is to pad all values with lots of zero bytes and to prohibit compression, either of which are much larger losses for performance than serialization is. 
  - In other words, binary-update-in-place seems like a clear win for heirarchical data storage, but practically it's not.
- 🐛 BSON assumes, for example, that all integers fit in 64-bits and all floating point values can be accurately represented as float8.  So not all JSON objects can be represented as BSON without loss of information.
  - 🐛 BSON also adds a bunch of extra types that are not part of JSON, like timestamps, regular expressions, and embedded documents.  So not all BSON objects can be represented as JSON without loss of information.
  - While it's tempting to think that BSON is a serialization format for JSON, and the name is meant to suggest that, it really isn't. It's just a serialization format for approximately whatever the authors thought would be useful, which happens to be kinda like JSON.

- Hi everyone. I used to work on a project storing large quantities of schema-less data, initially using MongoDB, then Postgres with JSON, and eventually I implemented BSON support for Postgres to get the best of both worlds: https://github.com/maciekgajewski/postgresbson
  - I don't think that JSONB is a good idea. There is a lot to learn from MongoDB's mistakes in this area.
