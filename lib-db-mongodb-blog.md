---
title: lib-db-mongodb-blog
tags: [blog, mongodb]
created: 2023-01-02T08:26:10.469Z
modified: 2023-01-02T08:26:21.177Z
---

# lib-db-mongodb-blog

# guide

# blogs-stars

## 💡💡 [6 Rules of Thumb for MongoDB Schema Design_201406](https://www.mongodb.com/blog/post/6-rules-of-thumb-for-mongodb-schema-design)

- 设计表时考虑
  - 属性值的基数有多大，是否embed/referencing
  - 是否要直接获取或查询属性值或子文档
  - 读写频率

- How do I model a one-to-N relationship?
- MongoDB has a rich and nuanced vocabulary for expressing what, in SQL, gets flattened into the term “One-to-N.” Let me take you on a tour of your choices in modeling One-to-N relationships.

- Many beginners think that the only way to model “One-to-N” in MongoDB is to embed an array of sub-documents into the parent document, but that’s just not true. 
- When designing a MongoDB schema, you need to start with a question that you’d never consider when using SQL and normalized tables: What is the cardinality(基数) of the relationship? 
  - Put less formally: You need to characterize your “One-to-N” relationship with a bit more nuance: Is it “one-to-few, ” “one-to-many, ” or “one-to-squillions”? 
  - Depending on which one it is, you’d use a different format to model the relationship.

- Basics: Modeling one-to-few
  - You’d put the addresses in an array inside of your Person object
  - The main advantage is that you don’t have to perform a separate query to get the embedded details; 
  - the main disadvantage is that you have no way of accessing the embedded details as stand-alone entities.
  - 对于查询子文档相关的计算可能不方便

- Basics: One-to-many
  - Each product may have up to several hundred replacement parts, but never more than a couple thousand or so
  - This is a good use case for referencing. 
  - You’d put the ObjectIDs of the parts in an array in product document. 
  - This style of referencing has a complementary set of advantages and disadvantages to embedding. 
  - Each Part is a stand-alone document, so it’s easy to search them and update them independently. 
  - One trade off for using this schema is having to perform a second query to get details about the Parts for a Product. (But hold that thought until we get to denormalization.)

- Basics: One-to-squillions
  - An example of “one-to-squillions” might be an event logging system for different machines. 
  - This is the classic use case for “parent-referencing.” You’d have a document for the host, and then store the ObjectID of the host in the documents for the log messages.
  - You’d use a (slightly different) application-level join to find the most recent 5, 000 messages for a host

- Recap
- You need to consider two factors:
  - Will the entities on the “N” side of the One-to-N ever need to stand alone?
  - What is the cardinality of the relationship: Is it one-to-few; one-to-many; or one-to-squillions?
- Based on these factors, you can pick one of the three basic One-to-N schema designs:
  - Embed the N side if the cardinality is one-to-few and there is no need to access the embedded object outside the context of the parent object.
  - Use an array of references to the N-side objects if the cardinality is one-to-many or if the N-side objects should stand alone for any reasons.
  - Use a reference to the One-side in the N-side objects if the cardinality is one-to-squillions.

- Intermediate: Two-way referencing
  - 类似使用3张表。There’s a “people” collection holding Person documents, a “tasks” collection holding Task documents, and a One-to-N relationship from Person to Task. 
  - Putting in the extra "owner" reference into the Task document means that its quick and easy to find the task’s owner, but it also means that if you need to reassign the task to another person, you need to perform two updates instead of just one. 
  - using this schema design over a normalized database model means that it is no longer possible to reassign a Task to a new Person with a single atomic update. 
  - This is OK for our task-tracking system; you need to consider if this works with your particular use case

- Intermediate: Database denormalization with one-to-many relationships
  - you can also add denormalization into your schema. This can eliminate the need to perform the application-level join for certain cases, at the price of some additional complexity when performing updates.
  - 示例1，在子文档不仅存放id，还存放最常用的字段值如name/title，减少join
  - but you would have to perform that join if you needed any other information about a part.
  - Denormalization saves you a lookup of the denormalized data at the cost of a more expensive update since you're adding a little data redundancy to the database
  - when you update the Part name you must also update every place it occurs in the "products" collection.
  - Denormalization only makes sense when there’s an high ratio of reads to updates. If you’ll be reading the denormalized data frequently, but updating it only rarely, it often makes sense to pay the price of slower write performance
  - As updates/writes become more frequent relative to queries, the savings from denormalization decreases.
  - if you denormalize a field, you lose the ability to perform atomic and isolated updates on that field.
  - 示例2，不存放id，直接存放内容
  - This is likely to be a more expensive update, since you’re updating multiple Parts instead of a single Product. 
  - As such, it’s significantly more important to consider the read-to-write ratio when denormalizing in this way.

- Intermediate: Database denormalization with one-to-squillions relationships
  - This works in one of two ways: you can either put information about the “one” side (from the "hosts" document) into the “squillions” side (the log entries), or you can put summary information from the “squillions” side into the “one” side.
  - Just as with denormalization in the “One-to-Many” case, you’ll want to consider the ratio of reads to updates.

- Recap
  - You can use bi-directional referencing if it optimizes your schema, and if you are willing to pay the price of not having atomic updates.
  - If you are referencing, you can denormalize data either from the “one” side into the “N” side, or from the “N” side into the “one” side.
- When deciding on database denormalization, consider the following factors:
  - You cannot perform an atomic update on denormalized data.
  - Denormalization only makes sense when you have a high read-to-write ratio.

- Database denormalization rules of thumb
- Favor embedding unless there is a compelling reason not to.
- Needing to access an object on its own is a compelling reason not to embed it.
- Arrays should not grow without bound. 
  - If there are more than a couple of hundred documents on the “many” side, don’t embed them; 
  - if there are more than a few thousand documents on the “many” side, don’t use an array of ObjectID references. 
  - High-cardinality arrays are a compelling reason not to embed.
- Don’t be afraid of application-level joins: 
  - If you index correctly and use the projection specifier, then application-level joins are barely more expensive than server-side joins in a relational database.
- Consider the read-to-write ratio with denormalization. 
  - A field that will mostly be read and only seldom updated is a good candidate for denormalization. 
  - If you denormalize a field that is updated frequently then the extra work of finding and updating all the instances of redundant data is likely to overwhelm the savings that you get from denormalization.
- As always with MongoDB, how you model your data depends entirely on your particular application’s data access patterns. 
  - You want to structure your data to match the ways that your application queries and updates it.

- Your guide to the rainbow
  - For “one-to-few, ” you can use an array of embedded documents.
  - For “one-to-many, ” or on occasions when the “N” side must stand alone, you should use an array of references. You can also use a “parent-reference” on the “N” side if it optimizes your data access pattern.
  - For “one-to-squillions, ” you should use a “parent-reference” in the document storing the “N” side.
  - You’d do denormalizing only for fields that are frequently read, get read much more often than they get updated, and where you don’t require strong consistency, since updating a denormalized value is slower, more expensive, and is not atomic.

- Appendix I: What is database denormalization?
  - Data that is accessed together should be stored together. 
  - Denormalization is the process of duplicating fields or deriving new fields from existing ones. 
  - Denormalized databases can improve read performance and query performance in a variety of cases
  - While embedding documents or arrays without data duplication is preferred for grouping related data, denormalization can improve read performance when separate collections must be maintained.
  - Some users coming from the relational database who are more familiar with a normalized database model world treat the document as a row in a table or spread across multiple tables. 
  - it isn’t the more efficient way to store data or query large amounts of data, especially IoT data.
  - Denormalization enables you to increase performance of the database while having fewer joins compared with the normalized database model of a relational database.
  - Note that with a denormalized database, it's important to maintain consistent duplicate data . 
  - However, in most cases, the increase in data retrieval performance and query execution will outweigh the presence of redundant copies of data and the need to avoid data inconsistency.

- Appendix II: When does database denormalization make sense vs. database normalization?
- Denormalization makes sense when you have a high read-to-write ratio. 
  - With denormalization you can avoid costly joins, at the expense of having more complex and expensive updates. 
  - Therefore, you should practice denormalization on only those fields that are read most often and are seldom updated since data redundancy is less of an issue.
  - $lookup operations join data from two collections in the same database based on a specified field. 
  - $lookup operations can be useful when your data is structured similarly to a relational database 
  - If you frequently run $lookup operations, consider restructuring your schema through denormalization such that the your application can query a single collection to obtain all of the information it needs.
  - Use embedded documents and arrays to capture relationships between data in a single document structure. 
  - Use database denormalization to take advantage of MongoDB’s rich document model, which allows your application to retrieve and manipulate related data in a single query execution.
- Normalized data models describe relationships using references between documents. 
- In general, use normalized data models in the following scenarios:
  - When embedding would result in duplication of data but would not provide sufficient read performance advantages to outweigh the implications of data duplication.
  - To represent more complex many-to-many relationships.
  - To model large hierarchical data sets.
# blogs

# blogs-internals

## 🔍 [Full-Text Search: What Is It And How It Works | MongoDB](https://www.mongodb.com/basics/full-text-search)

- Full-text search refers to searching some text inside extensive text data stored electronically and returning results that contain some or all of the words from the query. 
- In contrast, traditional search would return exact matches.
- traditional string searches can be performed on smaller text fields. These methods are not as efficient as modern indexed searches but require fewer resources. 
- Full-text searches provide more rich options for advanced querying but can be more complex to set up.
- String searches are algorithms that search for consecutive characters in a larger text field.
  - Another technique often used for string searches is the use of regular expressions. Those expressions represent a search pattern and are supported by most modern programming languages.
  - Some algorithms exist to increase the speed of those searches if the text to be searched is more significant. The Rabin-Karp algorithm, which looks for matching substrings, is fast and easy to implement. The Knuth-Morris-Pratt algorithm looks for all instances of a matching character, increasing the speed for multiple matches in a string. Other advanced techniques can be used to perform fuzzy searches.
- In a SQL database, a search on a text field in a record is usually done using a `LIKE` operator.
  - In MongoDB, a similar search can be done using the $regex operator.

```JS
// SELECT * FROM menus WHERE item LIKE "%pasta%";

db.menus.find({ "item": { "$regex": /pasta/i } });
```

- Full-text search is meant to search large amounts of text. 
  - The key to this technique is indexing.
  - Indexing can be done in different ways, such as batch indexing or incremental indexing.
  - The index then acts as an extensive glossary for any matching documents. Various techniques can then be used to extract the data. 
  - Apache Lucene, the open sourced search library, uses an inversed index to find the matching items.
  - This technique is much faster than string searches for large amounts of data. However, these indexes require some disk space and can consume a lot of resources when created.

- The key to an efficient full-text search is index creation. 
  - Essentially, the index creation process goes through each text field of a dataset. 
  - For each word, it will start by removing any diacritics (marks placed above or below letters, such as é, à, and ç in French). 
  - Then, based on the used language, the algorithms will remove filler words and only keep the stem of the terms. 
  - This way, “to eat, ” “eating, ” and “ate” are all classified as the same “eat” keyword. 
  - It then changes the casing to use only either uppercase or lowercase. 
  - The exact indexing process is determined by the analyzer that is used.

- To implement a full-text search in a SQL database, you must create a full-text index on each column you want to be indexed. 
  - In MySQL, this would be done with the `FULLTEXT` keyword.
  - Then you will be able to query the database using `MATCH` and `AGAINST`.
- While this index will increase the search speed for your queries, it does not provide you with all the additional capabilities that you might expect. 
  - To use features such as fuzzy search, typo tolerance, or synonyms, you will need to add a core search engine such as Apache Lucene on top of your database.

```SQL

ALTER TABLE menus ADD FULLTEXT(item);

SELECT * FROM menus WHERE MATCH(item) AGAINST("pasta");
```

- No matter which database you are using, before implementing a full-text search solution, you will have to take these considerations into mind.
  - Necessary features. Adding a full-text index to your database will help you optimize text search. Still, you might need additional features such as auto-complete suggestions, synonym search, or custom scoring for relevant results.
  - Architectural complexity. Adding additional software to your architecture means separate systems to maintain and additional software complexity to query two different sources.
  - Costs. Whether a solution is built in-house or uses a third-party tool, additional charges are to be expected.

- To provide full-text search capabilities to your application, you will need an extra layer to take care of the indexing and provide you with the results.

- Conclusion
  - Full-text search is a complex topic. It requires a good amount of expertise to set up correctly. Adding additional features such as fuzzy search, highlights, or synonyms might also require a lot of extra work.

## 📝 [Inside New Query Engine of MongoDB_202309](https://laplab.me/posts/inside-new-query-engine-of-mongodb/)

- 
- 
- 

## 👥 [MongoDB’s new query engine | Hacker News](https://news.ycombinator.com/item?id=37583147)

- it looks like it was available from 5.1, also interesting is that you can't choose which engine to use, so I suppose it only works on subsets or queries that meet certain conditions.

- 🆚️ Serious question: Why use MongoDB when Postgres supports indexed dynamic json?
- MongoDB:
  - a) has a proven, supported, easy-to-use horizontal scaling solution. PostgreSQL doesn't.
  - b) is ridiculously faster than PostgreSQL at per-tuple document updates.
  - c) has clients which are tailored for operations and data structures around documents.
  - d) is easier to install, configure and manage.
- 👉🏻 PostgreSQL will be horizontally scaling if you can avoid joins and index range locks. But the thing is you don't want to, or why do you need SQL database then. I found MongoDB good for cases when you need a lot of upserts, your data model is looks like document and you don't need joins. Like you store events data for further processing or collect stats or counters with tags/indexes.

- one killer feature for me is ChangeStreams. It's miles ahead of what Postgres offers

- Does MongoDB still lose data?
  - No. Since 5.0 the default write concern is majority, if that's what you were referring to.
# more-blogs
