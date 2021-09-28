---
title: thread-lang-js-worker-concurrent
tags: [concurrent, js, thread, web-worker]
created: '2021-09-28T04:43:49.453Z'
modified: '2021-09-28T06:00:34.338Z'
---

# thread-lang-js-worker-concurrent

# discuss

- ## 

- ## 

- ## 

- ## Synchronous communication for DOM operations between main and worker thread has been a fun challenge. 
- https://twitter.com/adamdbradley/status/1442490416062943234
  - But the real dragons lay in marshaling data, and creating functions on one window context, to be accessed by another.
- I have always wondered how node did this with IPC then I saw somebody else pass functions between isolated contexts. completely mind-blowing stuff.
- https://github.com/laverdet/isolated-vm
  - a library for nodejs which gives you access to v8's Isolate interface. 
  - This allows you to create JavaScript environments which are completely isolated from each other. 
  - This can be a powerful tool to run code in a fresh JavaScript environment completely free of extraneous capabilities provided by the nodejs runtime.
