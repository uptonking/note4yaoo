---
title: lib-db-app-community-event-mq-queue
tags: [community, database, kafka, mq, queue]
created: 2023-12-09T12:32:17.786Z
modified: 2023-12-09T12:32:50.692Z
---

# lib-db-app-community-event-mq-queue

# guide

# discuss-stars
- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## Seeing several #Postgres-based queue implementations lately, 
- https://twitter.com/gunnarmorling/status/1733245970341646742
  - one thing I've been wondering: could vacuuming become an issue here, with lots of potentially short-lived records in high volume/through-put scenarios?
- Bloat needs to be managed. Autovacuum can be tuned aggressively to deal with it, but it is not free. We wrote about that
- Right. This is how PGQ https://github.com/pgq/pgq works for decades already (developed in Skype long ago). Nobody has achieved better results yet I think, and all new tools should look at this experience. BTW, CloudSQL is equipped with PGQ as I learned recently.
- Of course, a Postgres-based queue has its limits compared to message brokers, but with reasonable care, it can go far 
