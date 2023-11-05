---
title: lib-db-pouchdb-docs
tags: [docs, pouchdb]
created: 2023-10-10T21:37:10.415Z
modified: 2023-10-10T21:37:19.382Z
---

# lib-db-pouchdb-docs

# guide

# docs

## [Updating and deleting documents](https://pouchdb.com/guides/updating-deleting.html)

- PouchDB and CouchDB's document revision structure is very similar to Git's. 
  - In fact, each document's revision history is stored as a tree (exactly like Git), which allows you to handle conflicts when any two databases get out of sync.

## [Conflicts](https://pouchdb.com/guides/conflicts.html)

- PouchDB exactly implements CouchDB's replication algorithm, so conflict resolution works the same in both. 
  - For the purposes of this article, "CouchDB" and "PouchDB" may be used interchangeably.

- CouchDB and PouchDB differ from many other sync solutions, because they bring the issue of conflicts front-and-center. 
  - With PouchDB, conflict resolution is entirely under your control.

- In CouchDB, conflicts can occur in two places: immediately, when you try to commit a new revision, or later, when two peers have committed changes to the same document. 
  - Let's call these immediate conflicts and eventual conflicts.

- you can present both versions to the user, or resolve the conflict automatically using your preferred conflict resolution strategy: last write wins, first write wins, RCS, etc.
- Another conflict resolution strategy is to design your database so that conflicts are impossible. 
  - In practice, this means that you never update or remove existing documents – you only create new documents.
  - This strategy has been called the "every doc is a delta" strategy. 
  - There is also a PouchDB plugin that implements this strategy: delta-pouch.
# docs-couchdb

## [The CouchBase Database File Format_201805](https://github.com/couchbase/couchstore/wiki/Format)

- [The CouchBase Database File Format_201211](https://github.com/couchbaselabs/couchstore/wiki/Format)

- This is the current database file format used by Couchbase Server 2.0. 
  - It's similar, but not identical, to the format used by Apache CouchDB 1.2. 
  - It is implemented in a Couchbase 2.0 fork of CouchDB (in Erlang), and also by CouchStore in C.

- The most important thing to understand about a CouchDB file is that it is append-only. 
  - The only way the file is modified is to append new data at the end; bytes written are never overwritten. 
  - As a consequence, the critical file "header" data actually lives at the tail end of the file, since it has to be re-appended every time the file is changed.

- advantages
  - The data format is extremely robust, since the software can recover simply by scanning back from the end of the file to the last valid header.
  - Writers don't disturb readers at all, allowing concurrent access without read locks.
  - By default, earlier versions of a record remain in the file, making it easy to implement a version history and multi-version concurrency control (as exposed in the CouchDB API.)

- disadvantages
  - the file grows without bound as it's modified. To work around this, the file is periodically compacted by writing the live data to a new file, then replacing the old file with the new one. This can be done in the background without locking out either readers or writers.

- B-Tree Format
  - The B-trees used in CouchDB files are a bit different than in a typical implementation, because the file is append-only. 
    - A tree node is never updated in place; instead, a new copy of the updated node is written at the end of the file. 
    - Of course this means that the node's parent also has to be updated to point at the updated node, so the effect is that 👉🏻 every modification has to rewrite all the nodes from the affected leaf up to the root. 
    - In practice this isn't too expensive, especially if multiple writes are batched together into one update.
  - CouchDB's B-trees also have to forgo(弃绝；放弃) the sibling-node chaining that's typically used to speed up sequential access. 
    - The reason is that updating a node would invalidate the pointers to it in its siblings, forcing those nodes to be updated as well, resulting in a huge cascade of updates. 
    - Instead, the iteration algorithm remembers the path back to the root and periodically backtracks to find the next sibling node.
- Nodes On Disk
  - All B-tree nodes are compressed using the Snappy algorithm.

- Indexes
- A CouchDB database file contains three B-trees:
  - The by-ID index, which maps document IDs to values.
  - The by-sequence index, which maps sequence numbers (database change numbers, which increase monotonically with every change) to document IDs and values.
  - The local-documents index, which is conceptually the same as the by-ID index except that the documents in it do not appear in the by-sequence index, and by CouchDB convention the document IDs all begin with the ASCII sequence `_local/`.
- A CouchDB mapreduce view file contains two B-trees:
  - The by-ID index, which maps document IDs to values. This is also called the back-index.
  - The mapreduce-view index, which maps the the keys emitted by the view to its emitted values.

- The By-ID Index
  - This B-tree is an index of documents by their IDs. 
  - The keys are simply the document IDs, ordered lexicographically by raw bytes (as by the memcmp function.)
- The By-Sequence Index
  - The keys in this B-tree are 48-bit numbers representing the sequence number of a change to the database. 
  - This number is strictly increasing.
- The Local Documents Index
  - The reduce value in interior nodes of this B-tree is unused (empty).
- The Mapreduce-View Index
  - The keys in this B-tree consist of the emitted key and the document ID. 
  - For node pointer it is the emitted key and document ID of the rightmost child node.

- Numbers And Alignment
  - Numbers are in big-endian byte order (most significant byte first).
  - All values are tightly packed; there is no padding or multi-byte alignment.
  - Some values occupy partial bytes and have lengths that are not a multiple of 8 bits. These are stored in most-significant to least-significant bit order. 

- File Blocks
  - For purposes of locating the current file header (q.v.), the file is organized into 4096-byte blocks. 
  - The first byte of every block is reserved and identifies whether it's a data block (zero) or a header block (nonzero). 
  - Therefore only 4095 of the bytes are available for storing data.
  - Above the block level, these prefix bytes are invisible and simply skipped. So a data value that spans a block boundary will be written out with a zero byte inserted at the boundary, and this byte will be removed when reading the value.

- Data Chunks
  - The data in the file (above the block level) is grouped into variable-length chunks. 
  - All chunks are prefixed with their length as a 32-bit big endian integer, followed by the CRC32 checksum of the data. 

- File Header
  - A file header always appears on a 4096-byte block boundary, and the first byte of the block is nonzero to signal that it contains a header. 
  - A file will contain many headers as it grows, since a new updated one is appended whenever data is saved; 
  - So the algorithm to find the header when opening the file is to seek to the last block boundary, read one byte, and keep skipping back 4096 bytes until the byte read is nonzero.
# more
