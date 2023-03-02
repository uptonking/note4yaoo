---
title: lib-editor-slate-community-storage
tags: [community, slate-editor, storage]
created: 2023-03-02T14:24:00.087Z
modified: 2023-03-02T14:24:52.061Z
---

# lib-editor-slate-community-storage

# guide

# discuss
- ## 

- ## 

- ## [JSON format for storing](https://github.com/ianstormtaylor/slate/issues/1959)
  - In previous APIs I made, I noticed that arrays parsed faster than objects.
  - Here, sub-arrays are used to encode objects
- The current JSON format is definitely not the smallest it can be. But I think there are often other concerns for storage, having to do with read vs. write volumes, ease of maintenance, etc.
  - For example if you need to run migrations on your documents, having to pull them out of the database to deserialize them first is a big barrier. Or if you need to be able to query inside JSON documents (in Mongo/Postgres/etc.) then maintaining the naming scheme for the JSON is also very helpful.
  - For this reason, I think it's best to keep the JSON format as un-opinionated as possible. It maintains great readability, is easy to render into HTML/React/etc. for the view layer, and it maps directly to the immutable structure used while working with Slate. These are big benefits, and make sense for core.

- All that said, that doesn't mean you can't write your own minified serializer. I'm sure others would find it useful too. But I just don't think it makes sense as something to maintain alongside the core library, it's better as a third-party library.
