---
title: lib-saas-overleaf-docs
tags: [docs, overleaf]
created: 2024-10-19T09:27:21.258Z
modified: 2024-10-19T09:28:05.374Z
---

# lib-saas-overleaf-docs

# guide

# overview

# docs

## env-requirements

- A minimum base requirement of 2 cores and 3GB memory is required for basic operations with around 5 concurrent users.
  - As a rule of thumb, to provide a high and consistent level of service, 1 CPU core and 1GB of memory should be added to the minimal install for every 5-10 concurrent users.

- 👎🏻 We advise against using NFS/Amazon EFS/Amazon EBS for project/history storage in larger setups and explicitly do not support it for horizontal scaling. 
  - The behaviour of these file systems is not providing the necessary performance and reliability that Server Pro needs when running at a high scale. 
  - When the file system cannot keep up with the load, the application stalls from too many blocking IO operations. 
  - These stalls can lead to overrun redis-based locks, which in turn can result in corrupted project data. 
- 👍🏻 We advise on using S3 compatible object storage instead. 
  - Slow S3 performance in turn only affects the upload/download of files, which only leads to an elevated number of open connections to your S3 provider and in turn does not affect the behaviour of the rest of the application.
  - Additionally, Server Pro can specify reasonable timeouts on S3 requests, which is not possible for file system/IO operations at the application level.
- For reference, GitLab is following a similar stance of not supporting NFS/Amazon EFS with their self-managed offering.

- LaTeX is a single threaded program, meaning it can only utilize one CPU core at a time. 
  - The CPU is also the main limitation when compiling a document. 
  - Therefore the faster the single core performance of your CPU, the faster you will be able to compile a document.
  -  More cores will only help if you are trying to compile more documents than you have free CPU cores.

## [Sandboxed Compiles](https://github.com/overleaf/overleaf/wiki/Server-Pro:-sandboxed-compiles)

- Server Pro comes with the option to run compiles in a secured sandbox environment for enterprise security. 
  - It does this by running every project in its own secured docker environment.
- 
- 
- 
- 
- 
- 
- 
- 
- 

# more
