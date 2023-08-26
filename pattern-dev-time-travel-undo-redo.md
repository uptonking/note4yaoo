---
title: pattern-dev-time-travel-undo-redo
tags: [pattern, time-travel, undo]
created: 2023-08-25T21:52:48.494Z
modified: 2023-08-26T02:51:41.206Z
---

# pattern-dev-time-travel-undo-redo

# guide
- branch和versioning的参考方案
  - 同类产品，如git
  - 编辑器，如vscode、ckeditor、ospreadsheet
  - 数据库，如dolt、mongodb-doc-ver
# examples

# blogs

- [Making Data Structures Persistent_1986](http://www.cs.cmu.edu/~sleator/papers/Persistence.htm)

## [History Data Structures](https://gist.github.com/CMCDragonkai/d266a3055735545447439f0fa662a0e1)

- For stateful applications, there are 5 different ways of managing the history of state:
  - No History - Living in the moment. - Examples: Any stateful application that doesn't discards all previous states upon mutation.
  - Ad Hoc Snapshotting - Allows restoration to manually saved snapshots. - Examples: Memento Pattern.
  - Singleton - Only remembers the previous snapshot, where undoing the undo is just another undo. - Examples: Xerox PARC Bravo.
  - 1 Stack - Allows linear undo. - Examples: AtariWriter.
  - 2 Stack - Allows linear undo and redo. - Examples: Browser History, Microsoft Word, Adobe Photoshop.
  - Append-Only Log - Allows moving forward with reversed patches/deltas (a.k.a. compensating transactions). - Examples: Git-Revert, Datomic, Blockchain, Event Sourcing.
  - Tree - The Multiverse Approach. - Examples: Git, Vim, Emacs with UndoTree, Delorean.
- There's variations and hybrid approaches that have to deal with special cases involving multi-user history, which is relevant to operational transformation applications such as Google Docs.

- there are 2 different ways of encoding states. 
  - The snapshot method and the delta method. 
- The snapshot method is where every "state" is a complete and independent snapshot of what the state was. 
- Whereas the delta method (a.k.a. delta encoding) is the (ideally minimal) difference between the past and present. 
- The snapshot method uses more storage space, while the delta method requires more computation to merge the differences.
- the time to construct the snapshots takes much longer then when using the delta method.
  - This is because you may need to transitively apply all the deltas from origin.
- There's also a theory formalising how deltas works called "Patch Theory", which is used by the Darcs and Pijul version control system.

## [Introduction to a data structure that let's us time travel](https://arpitbhayani.me/blogs/persistent-data-structures-introduction/)

- Ordinary data structures are ephemeral implying that any update made to it destroys the old version and all we are left with is the updated latest one. 
  - Persistent Data Structures change this notion and allow us to hold multiple versions of a data structure at any given instant of time. 
  - This enables us to go back in “time” and access any version that we want.

- Persistent Data Structures preserve previous versions of themselves allowing us to revisit and audit any historical version. 

- Depending on the operations allowed on the previous versions, persistence is classified into three categories
- **Partially Persisten**t Data Structures allows access to all the historical versions but allows modification to only the newest one. 
  - This typically makes historical versions of the data structure immutable (read-only).
- **Fully Persistent** Data Structures allows access and modification to all the historical versions. 
  - It does not restrict any modifications whatsoever. 
  - This means we can typically revisit any historical version and modify it and thus fork out a new branch.
- **Confluently Persistent** Data Structures allow modifications to historical versions while also allowing them to be merged with existing ones to create a new version from the previous two.

- Implementing Partial Persistence
- Copy on Write Semantics
- Copy on Write Semantics
- Copy on Write Semantics
- Path-Copying Method

- Since persistent data structures thrive on high memory usage, they require some garbage collection system to prevent memory leaks. 
  - Algorithms like Reference Counting or Mark and Sweep serves the purpose pretty well.

## [Persisting the version history of a complex data structure](https://medium.com/@mmdGhanbari/persisting-a-persistent-data-structure-3f4cfd46036)

- In this article, we learned about persistent data structures and the different methods available to copy a complex one, as well as how to persist them in a relational database.
  - you may also want to check the Event Sourcing pattern, which suggests persisting the change itself instead of the changed data.
# more
- [Data model for storing revision history in FoundationDB · couchdb](https://github.com/apache/couchdb/issues/1957)

- [Immutable Data Structures - DEV Community](https://dev.to/martinhaeusler/immutable-data-structures-2m70)
