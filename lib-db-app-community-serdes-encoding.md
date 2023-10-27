---
title: lib-db-app-community-serdes-encoding
tags: [community, database, encoding, serdes]
created: 2023-09-17T17:43:41.484Z
modified: 2023-10-27T07:04:15.549Z
---

# lib-db-app-community-serdes-encoding

> about database serdes

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 
# discuss-column-json
- ## 

- ## [JSON and Virtual Columns in SQLite | Hacker News_202205](https://news.ycombinator.com/item?id=31396578)

- ## [Reducing logging cost by two orders of magnitude using CLP | Hacker News_202209](https://news.ycombinator.com/item?id=33032996)
- The interesting part about the article isn't that structured data is easier to compress and store, its that there's a relatively new way to efficiently transform unstructured logs to structured data. 
  - For those shipping unstructured logs to an observability backend, this could be a way to save significant money

- 👉🏻 This just in, Uber rediscovers what all us database people already knew, **structured data is usually way easier to compress and store and index and query** than unstructured blobs of text, which is why we kept telling you to stop storing json in your databases.
- There's nothing wrong with storing json in your database if the tradeoffs are clear and it's used in a sensible way.
  - Having structured data and an additional json/jsonb column where it makes sense can be very powerful. There's a reason every new release of Postgres improves on the performance and features available for the json data type. 
- Json has a huge structural problem: it's an ASCII representation of a schema+value list, where the schema is repeated with each value. It improved on xml because it doesn't repeat the schema twice, at least...
  - It's nonsensical most of the time: do a table, transform values out of the db or in the consumer.
  - The reason postgres does it is because lazy developers overused the json columns and then got fucked and say postgres is slow (talking from repeated experience here). Yeah searching in random unstructured blob is slow, surprise.
  - I dont dislike the idea to store json and structured data together but... you dont need performance then. Transferring a binary representation of a table and having a binary to object converter in your consumer (even chrome) is several orders of magnitudes faster than parsing strings, especially with json vomit of schema at every value.

- If your use case it to search / query on it often then jsonb column is the wrong choice. You can have an index on a json key, which works reasonably well but I'd probably not put it in the hot path
- Couldn't agree more. Not to mention timestamps that JSON simply doesn't handle and is essential for event data. The raijin database has an clever approach to solving the schema rigidity problem
- Storing JSON is so often the most direct and explicit way of accruing technical debt: "We don't really know what structure the data we'll get should have, just specify that it's going to be JSON"

- Postgres has excellent JSON support, it's one of my favorite features, it's a nice middle ground between having a schema for absolutely everything or standing up mongodb beside it because it's web scale. Us in particular, we leverage json-schema in our application for a big portion json data and it works great.
- MongoDB actually doesn't store JSON. It stores a binary encoding of JSON called BSON (Binary JSON) which encodes type and size information. 
  - This means we can encode objects in your program directly into objects in the database. It also means we can natively encode documents, sub-documents, arrays, geo-spatial coordinates, floats, ints and decimals. This is a primary function of the driver.
  - This also allows us to efficiently index these fields, even sub-documents and arrays.
  - All MongoDB collections are compressed on disk by default.

- Does anyone have a simple explanation of how it structures the log data?
  - 1) Use Zstandard with a generated dictionary kept separate from the data, but moreover:
  - 2) Organize the log data into tables with columns, and then compress by column (so, each column has its own dictionary). This lets the compression algorithm perform optimally, since now all the similar data is right next to itself. (This reminds me of the Burrows-Wheeler transform, except much more straightforward, thanks to how similar log lines are.)
  - 3) Search is performed without decompression. Somehow they use the dictionary to index into the table- very clever. I would have just compressed the search term using the same dictionary and do a binary search for that, but I think that would only work for exact matches.
# discuss
- ## 

- ## 

- ## 

- ## 🔥 [Database character sets and collations explained – why utf8 is not UTF-8 | Hacker News_202201](https://news.ycombinator.com/item?id=29793916)
- 
- 
- 
