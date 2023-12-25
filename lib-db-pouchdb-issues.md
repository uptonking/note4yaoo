---
title: lib-db-pouchdb-issues
tags: [issues, pouchdb]
created: 2023-12-25T18:53:42.754Z
modified: 2023-12-25T18:53:52.847Z
---

# lib-db-pouchdb-issues

# guide

# not-yet
- [Find keeps query objects in heap memory_202311](https://github.com/pouchdb/pouchdb/issues/8833)

- [indexeddb: move attachments out of DOC_STORE?_202310](https://github.com/pouchdb/pouchdb/issues/8811)
  - pouchdb-adapter-indexeddb's current implementation currently follows the naïve path.
  - Moving attachments e.g. to a separate `IDBObjectStore` would have performance implications, and would require a migration.
  - If making this change, care should be taken to re-use IndexedDB transactions where possible.
# issues

# more
