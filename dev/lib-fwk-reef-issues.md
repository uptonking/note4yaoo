---
title: lib-fwk-reef-issues
tags: [issues, reef]
created: 2020-11-04T17:53:21.113Z
modified: 2020-12-08T13:25:59.562Z
---

# lib-fwk-reef-issues

# more-issues
- [Does Reef remove element event listeners?](https://github.com/cferdinandi/reef/issues/68)
  - When Reef removes elements from the DOM, does it make sure that all its event listeners are removed as well?
    - Just a small concern about memory leaks and was wondering what Reef is doing to help prevent them.
  - No, it does not, but browsers themselves do garbage collect event listeners attached to events that no longer exist.
  - I strongly recommend using event delegation


- [domParser performance](https://github.com/cferdinandi/reef/issues/32)

