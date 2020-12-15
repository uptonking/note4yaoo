---
title: lib-pattern-rxjs-api
tags: [api, pattern, rxjs]
created: '2020-12-15T17:39:03.558Z'
modified: '2020-12-15T17:39:23.394Z'
---

# lib-pattern-rxjs-api

## Notification

- Represents a push-based event or value that an Observable can emit.
- This class is particularly useful for operators that manage notifications, like materialize, dematerialize, observeOn, and others. 
- Besides wrapping the actual delivered value, it also annotates it with metadata of, for instance, what type of push message it is (next, error, or complete).
