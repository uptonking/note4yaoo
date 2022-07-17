---
title: thread-data-tool
tags: [data, thread, tool]
created: 2021-08-09T07:24:32.473Z
modified: 2021-08-09T07:24:45.113Z
---

# thread-data-tool

# discuss

- ## 

- ## 

- ## 

- ## I love delta, a CLI tool that makes git diffs pretty and useful.
- https://twitter.com/cpojer/status/1520538000882487296
  - https://dandavison.github.io/delta/introduction.html

- ## Had a devious(不直接的，迂回的；欺诈的) thought: that SQLite.js trick where you host the DB file statically on GitHub pages? 
- https://twitter.com/simonw/status/1428843031134834689
  - You could totally handle writes to the DB if you wrote to a CSV file using the GitHub API and then ran an Action to rebuild and redeploy the database file
- How do you authorize to the github api? Unless they let you do crazily granular permissions, publishing an API key sounds like a Very Bad Idea
  - You could get people to OAuth themselves against GitHub and then use  the API to submit issues against the repo, then have the actions trigger against new issues
  - Or you could use a trick like this one to create encrypted API tokens that only have permission to call very specific API endpoints
- Played around with that exact idea. Did analytics since I could set up a snowplow collector on another CDN & run a job to process the log files. 
  - https://analytics.serv.rs/
- You could, the main problem is writes from multiple clients; only one client could ever write to it
  - fwiw you’re free to hack on a new backend to absurd-sql. All the machinery is there for any kind of async backend
- As @AbdulrhmnGhanem mentioned in a comment, I've done a very similar solution using Azure Functions and PyGitHub (which is a wrapper to GitHub REST API).
  - Database migrations are also triggered with a GitHub action, API authentication is handled with Auth0.
- @NoorEldeenSalah has done something similar; an Azure function handles writes, behind Auth0, and migrations are handled in a GitHub action.
  - https://github.com/ElGarash/meetings

- ## I have to batch-convert CSV to XLS (or XLSX).
- https://twitter.com/rauschma/status/1421850627060158469
- https://github.com/Aternus/csv-to-xlsx
  - Convert CSV files to XLSX (Excel 2007+ XML Format) files.
  - Written in JavaScript. Available for Node.js CLI and API.
  - Binaries are available for: Windows/Linux/MacOS
- The `xlsx` module actually ships with a bin script:
  - $ npx xlsx --xlsx in.csv # writes XLSX -> in.csv.xlsx
  - $ npx xlsx --xls in.csv # writes XLS -> in.csv.xls
  - $ npx xlsx in.csv -o out.xlsx # writes to out.xlsx
- https://github.com/erikmartinjordan/jsonmatic
  - https://tiempone.com/
  - transform a CSV into a JSON and vice versa.
