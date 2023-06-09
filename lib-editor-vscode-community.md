---
title: lib-editor-vscode-community
tags: [community, editor, ide, vscode]
created: 2023-01-21T18:49:01.333Z
modified: 2023-01-21T18:53:04.519Z
---

# lib-editor-vscode-community

# guide

# discuss
- ## 

- ## 

- ## 

- ## Most sandboxes in CodeSandbox are stored in a Postgres database.
- https://twitter.com/CompuIves/status/1667148424389566465
  - 40M+ sandboxes and 400M+ files stored in Postgres, and we still have performant load times.
  - When going with Postgres, I thought "this is the first thing we'll have to replace". Still didn't happen after 6 years
- Generally, the three technologies that exceeded my expectations in scale and performance:
  - Postgres
  - Elixir
  - Rust
- Now we're seeing that the database is growing very big (leading to long & big backups), so we started archiving sandboxes to GCP to save space. We're considering moving our DB from k8s to a managed instance. But still, Postgres has exceeded all my expectations.
- Curious, which components are written in Rust vs Elixir? Did you find that Elixir was better suited for some tasks than Rust?
  - Yah, Elixir is doing everything with the API (including websocket message handling).
  - Rust is doing computationally expensive things, or things that require a lot of string manipulation.
  - For example, we use Elixir to handle WS OT messages, but we use Rust then to apply the OT operations on the string. We first did this with Elixir, but (partly because of my implementation) it started to eat a lot of memory as every mutation created a new string.
  - Elixir + Rust interop is fantastic, so it's nice if you can pull out Rust for these kind of things while maintaining the concurrency/robustness of Elixir for the server.
- Erlang/Elixir under load is just amazing. Incredibly resilient. One of the many reasons I became a fanboy of CouchDB. Still love Postgres but there is something beautiful about storing everything in a giant B-tree

- 🤔 How is the Postgres DB structured.  Is it single node or shareded across multiple nodes?  And do you store files in Postgres as blobs?
  - Single DB (with a R/O replica). Files are stored as text, binary files are uploaded to GCP and we store a link in the db.
- Wow, just single DB for such huge workload!  Must be a huge machine.
  - It's not huge! 4 cores and 24GiB RAM (actually I believe 16GiB would be fine too). Plus we also store sandbox pageviews (hourly, daily, weekly, monthly)/users/teams etc...
- Incredible!  I am using a little bigger machine for a much lesser scale application.  Likely I am doing something wrong.
