---
title: pattern-local-first-blog-db
tags: [blog, database, local-first, offlineable]
created: 2023-12-10T01:44:41.350Z
modified: 2023-12-10T01:45:11.286Z
---

# pattern-local-first-blog-db

# guide

# blogs

## [Choosing the right frontend database for a single page application - DEV Community_201910](https://dev.to/johannesjo/choosing-the-right-frontend-database-for-a-single-page-application-3i0)

- WatermelonDB put me off because of its strong focus on React and it not working well with typescript atm. It shares one of the "problems" with LokiJS: The data in stored in IndexedDB is just a big string. This might not be a real problem, but it feels wrong to go about persistence like that. I didn't come much further than playing around a little with LokiJS, because I felt that it might be basically WatermelonDB with less issues, but also less of the stuff I need and I was still hoping for something better.
- RxDB looked pretty promising and I assume that it really shines when you are using a server. But the bad performance was just not an option for an app that aims at desktop app like performance.
- Using native IndexedDB should work fine for the most part. The main disadvantage is that I would have to write a lot of code and I don't want to re-invent the wheel (just quite yet).

- I've completely rewritten LokiJS's IDB adapter to store things in little chunks
# more
