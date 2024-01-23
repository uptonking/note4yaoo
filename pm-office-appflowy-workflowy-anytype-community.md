---
title: pm-office-appflowy-workflowy-anytype-community
tags: [anytype, appflowy, community, note-taking, workflowy]
created: 2024-01-23T02:52:57.229Z
modified: 2024-01-23T02:54:45.030Z
---

# pm-office-appflowy-workflowy-anytype-community

# guide

- require-login: workflowy, anytype
  - 无需登录: appflowy
# discuss-stars
- ## 

- ## 

- ## 
# discuss-appflowy
- pros
  - ?

- cons
  - ?

- features
  - ?

- ## 

- ## 

- ## 
# discuss-workflowy
- pros
  - ?

- cons
  - ?

- features
  - ?

- ## 

- ## 

- ## 
# discuss-anytype
- pros
  - ?

- cons
  - ?

- features
  - Open-Source, E2E encrypted, offline first, syncs to all your devices via IPFS so no centralized server, etc.

- ## 

- ## 

- ## [we'd love your feedback on Anytype - private, end-to-end encrypted and local first alternative to notion and obsidian : linux _202311](https://www.reddit.com/r/linux/comments/187kx7z/wed_love_your_feedback_on_anytype_private/)
- One of the big selling points of Obsidian to me is that everything is stored as text files. That makes it future proof, because even if I would stop using Obsidian, any app can read text documents.

- 🆚️ Why is it better than Logseq?
  - i think anytype is more visual, it has sets and databases/collections, customizable sidebar with widgets and other cool features + it has native mobile apps. 
  - the biggest upgrade will come with release of multi-player - we will add an ability to share spaces and collaborate with others by april 2024
- Sets and collections are less powerful than Logseq queries though.

- Why isn't everything stored in plaintext? 
  - to enable such features as data-bases and sets
- To allow this kind of sync
  - you can export to protobuf - an open data standard - it keeps all formatting and all details in place. you can also export to markdown, but relations are not exported. the beauty of anytype being local first is that if anytype no longer exists, you can still use the app on your devices and sync them without any problem, so you can use your data in this interface just because you already downloaded it
- it uses open source protocol Anysync to sync your data - it's a protocol that enables p2p local first collaboration over encrypted data. you can have anytype only on your desktop and your phone and sync them over your home network - there is no storage limit for that - you are basically limited only by your own storage space. If you want to have a back-up that can help with off-line/on-line problem you can use anytype backup or self-host your own backup. No the code of anytype is open for anyone to review. anysync, middleware (all networking and logic) are under MIT licence, clients are under source available licence at the moment
- anytype backups nodes are different vs. any cloud server, as the architecture is different. Cloud servers store not only your data, but your encryption keys and the logic is executed on the server. So for conflict resolution to happen the server needs to decrypt your data, make conflict resolution and then send it back to devices. Anytype backup nodes store only encrypted data, the keys are only controlled by users. Also, the logic is executed locally (local-first software), so the only place where data is decrypted is always a user device

- I would like to thank you for the clarity around the licensing, which is a mixed open source/non open source model. The clients and middle ware are not open source, and the fundamental network layer is. No one will get nasty surprises this way.
  - I would like to thank you for the clarity around the licensing, which is a mixed open source/non open source model. The clients and middle ware are not open source, and the fundamental network layer is. No one will get nasty surprises this way.
# discuss-more-note-taking
- ## 

- ## 

- ## 
