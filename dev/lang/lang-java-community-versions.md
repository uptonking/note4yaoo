---
title: lang-java-community-versions
tags: [community, java]
created: 2023-08-28T04:36:12.285Z
modified: 2023-08-28T04:36:35.505Z
---

# lang-java-community-versions

# guide

# discuss
- ## 

- ## 

- ## 

- ## 

- ## Why not moving even to Java 17?
- https://twitter.com/gunnarmorling/status/1522484429477842944
- That'd mean leaving many users behind. Everyone using Debezium's embedded engine would have to move to 17 too, and a share of users isn't there yet. That said, we do use Java 17 for our own tests.
- Good point... up until a couple of years ago I thought https://github.com/sirixdb/sirix is more of an academic project. Currently I'm always switching to the newest Java-version as I wanted to use the new foreign memory API for a simple mmap backed storage alternative.
  - However, to get some users I finally have to stick to a Java-version, as it's also one of the benefits, that you can simply embed SirixDB in your Java/Kotlin/Closure...-applications and to release real versions. Up until now I also simply release SNAPSHOTs all the time
- Yeah, it depends on how you position and distribute SirixDB (need to check it out btw. if it's a separate server application which you ship as a container image or jlink-ed runtime image, 17 is fine. If it's meant to be a library folks pull into their apps, I'd stick to 11.
  - Basically it's both. The core can be simply used via APIs or an HTTP-server to access SirixDB remotely and that's also how the docker container can be used. I've thought about adding a Kafka backend to write the resources in a distributed queue instead of an append-only file.
  - The whole index is a huge persistent trie of tries (first level revisions are indexed, Second level is the document index plus secondary indexes). The data is versioned in the leaf pages through a sliding snapshot algorithm (no write peaks due to intermittent full page snapshots)
