---
title: lib-db-feat-jsonb-blog
tags: [blog, jsonb, mongodb]
created: 2024-02-02T09:57:54.012Z
modified: 2024-02-02T09:58:04.895Z
---

# lib-db-feat-jsonb-blog

# guide

# blogs-mongodb-sql

## [A JSON use case comparison between PostgreSQL and MongoDB _201810](https://portavita.github.io/2018-10-31-blog_A_JSON_use_case_comparison_between_PostgreSQL_and_MongoDB/)

- Conclusions
- Mongo can hold the same amount of data in half the space used by Postgres. 
  - This is important to keep in mind if you are holding a big amount of data. Therefore if disk space is a constraint, then Mongo has less restrictive requirements.
- Also there are some aspects to take into consideration about disk and RAM. If a table takes more space, more space is needed when loading data in memory.
  - So the bigger the table/index, the more need for RAM.
- About query speed, we can see that if data is loaded in cache/RAM then Postgres is faster than Mongo in returning an output.
  - Differently, if data is not in cache, Mongo performs better.
- There is no definitive winner because both provide advantages and disadvantages depending on your use case.
- Does your database entirely fit in RAM? Then Postgres is faster.
- Is disk space a big constraint because you are storing a lot of data? Mongo will save you ½ of the space in comparison with Postgres.
- Do you have a big database, you are not concerned about disk space and you usually only query a fraction of that data which also fits your RAM? Then go for Postgres.

- Today’s comparison is only based on a few simple parameters and that’s it.
  - we are willingly not taking into consideration a very wide range of decisional aspects like the easiness of writing a query, the possibility to use Postgres extensions, the possibility to read from secondary on Postgres, or use sharding (Postgres and Mongo), table partitioning (Postgres) or maybe decouple some fields for our JSON data and insert it on a Postgres column of our JSON table.
- About how data was indexed, something worth noticing, is that we used a generic index on ‘data’ for Postgres which takes a lot of space but also is a kind of silver bullet because it covers a lot of use cases (the whole data is in there).
  - The downside is its size, in our case 1/3 of the table size. (15 MB index on a 45 MB table).
- On Mongo we took into consideration only an index on ‘MarriageDate’, which has rather a restrictive usage.
# blogs-jsonb-bson

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
# more
