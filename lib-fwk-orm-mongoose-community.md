---
title: lib-fwk-orm-mongoose-community
tags: [community, mongoose]
created: 2023-02-05T18:47:50.614Z
modified: 2023-02-05T18:48:02.500Z
---

# lib-fwk-orm-mongoose-community

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## [Error when using AWS DocumentDB with 4.0.0 engine · Issue · Automattic/mongoose _202311](https://github.com/Automattic/mongoose/issues/14056)
- The only thing I can say is that the "More than one query match for field" error comes from DocumentDB, not Mongoose or the MongoDB Node driver. 
  - We don't work with DocumentDB at all and Mongoose doesn't support it, so unfortunately we can't help other than suggest that you use MongoDB Atlas. 
  - [Amazon DocumentDB compatibility with MongoDB - Amazon DocumentDB](https://docs.aws.amazon.com/documentdb/latest/developerguide/compatibility.html)

- [DocumentDB Compatibility? · Issue · Automattic/mongoose _202011](https://github.com/Automattic/mongoose/issues/9528)
  - We don't officially support DocumentDB. There have been a few issues reported: #7800, #4596 (comment), #4455. 
  - We fix DocumentDB issues if we can, but we do not currently test against DocumentDB, nor do we have plans to.
# discuss
- ## 

- ## 

- ## [Help me to choose between TypeORM or Mongoose for MongoDB_202202](https://www.reddit.com/r/Nestjs_framework/comments/swzr9y/help_me_to_choose_between_typeorm_or_mongoose_for/)
- Mongoose. In my experience TypeORM not have great support to MongoDB.
- I think one of the reasons to use ORMs is to make databse agnostic. But I dont think there are many cases of switching from NoSQL to RDBMS (or just any switch in general) after deployment (maybe migrate during dev).
- I would additionally suggest you to use mongoose over typegoose. Typegoose and the documentation was a pain, we had to switch to mongoose
- I've tried typeORM and mongoose, I think mongoose are good in doc. and simple for the beginner.
  - TypeORM the doc is not good. and will have a lot of tiny issues. It's not good to be a tool.

- ## [Mongoose browser implementation _202007](https://github.com/Automattic/mongoose/issues/9273)
- As long as you use Webpack and your webpack config has `target: 'web'` , then you should be able to use `const mongoose = require('mongoose')` in your browser code.
