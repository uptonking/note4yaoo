---
title: lib-db-acebase-community
tags: [acebase, database, firebase]
created: 2024-01-07T12:45:00.425Z
modified: 2024-01-07T12:45:24.749Z
---

# lib-db-acebase-community

# guide

# dev

# examples

- https://github.com/coorise/swyger /202308/js
  - a boilerplate made for you to get started with Server and Client Side.
  - 依赖acebase
# discuss-stars
- ## 

- ## 🔀 [Use more than one CPU_202111](https://github.com/appy-one/acebase/issues/49)
- Using multiple CPUs is definitely possible using nodejs clustering or pm2, but you shouldn't have to if you add indexes. With an index (or multiple), you'll be able to get query results in milliseconds because it won't have to plow through all reords to check if they match your criteria.

- I've been working on the clustering functionality, it is now possible to create pm2 and cloud-based AceBaseServer clusters!
Check out the new AceBase IPC server repository, its documentation describes in detail how to setup a cluster of AceBase servers. All is obviously brand spanking new and might have issues, would really appreciate if you'd want to help testing!

- ## 📈 [How to speed up loading in 4GB CSV?_202202](https://github.com/appy-one/acebase/issues/65)
  - I have a 4GB CSV file where each line is points one string to a list of strings. I have about 3 million lines.

- Running AceBase in a single Node. JS process means only 1 CPU thread doing all the work. Although AceBase is able to run in clusters, it does not share already assigned workload with other processes. There is no internal load balancer, good to keep that in mind!
- If you have indexes on the data you are importing to, consider removing them until your import is done. An index slows down inserts. I assume this is not the case here, but I do want to mention it.
- If you have transaction logging enabled on your db, this will also slow down inserts and you might also want to disable that.
- 💡 I've recently worked on developing a streaming import for json data, but the current implementation is (too) slow. Improvements are coming, but will take some time. 
  - I might actually look at implementing a csv import before then, because of it simple "flat" format that makes it very easy to create batches. 
  - Note that transforming the import data (as in your code) will not be possible then, so batch updating will remain the preferred strategy in your case.

- I've made quite a few improvements that allow multiple index lookups and storing at the same time, I am seeing performance improvements in the 20x range already in my current tests. These changes do impact critical parts of the storage engine so I'll have to make 100% none of this can corrupt a database at any time, so I'll be doing extensive testing this week.

- you can't use multiple threads to speed up your import because each thread would acquire an exclusive write lock on the target collection - they'll effectively just be taking turns in importing batches.
# discuss
- ## 

- ## 

- ## 🌰 [Acebase looks great, just added support in MeshCentral_202208](https://github.com/appy-one/acebase/issues/137)
  - I needed a pure NodeJS database to use as a default for small instances where someone does not want to setup MongoDB, PostgreSQL, MariaDB, MySQL. 
  - AceBase looks like it works perfectly for what I need and I spent the day integrating it into MeshCentral

- ## [Anyone tried AceBase? : node_202202](https://www.reddit.com/r/node/comments/snsr3z/anyone_tried_acebase/)
- Acebase is a realtime filebased database. So far i have no bad experience at all been using it for a year now. There tons of stuffs that acebase can do vs other similar filebased db in npm such as indexing, realtime query and streaming.
- Downside of acebase is that you cant use OR operators for every filter chains are logically AND. 
- Im currently making a wrapped acebase-server an ala'h Parse-server where you can execute before/after hooks, link objects, field level ACL, live aggregates and live query of course. https://github.com/paradis-A/lendb-server

- when run acebase for the first time it provides username and password. if you disabled auth then you can use username: admin and leave the password empty. it will prompt error but you can actually navigate to browse the data. the auth is not sessioned so if you reload then you will have to reload again. 

- ## I'm the developer of AceBase which is essentially the Firebase realtime database for browser and Nodejs. _202103
- https://twitter.com/4ewout/status/1375012804864905216
  - I started building this because I wanted Firebase to work offline and Ionic's Storage API was too limited
