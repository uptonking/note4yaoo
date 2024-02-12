---
title: lib-collab-powersync-blog
tags: [blog, collaboration, powersync]
created: 2024-02-12T03:23:21.954Z
modified: 2024-02-12T03:23:39.026Z
---

# lib-collab-powersync-blog

# guide

# blogs

## 🆚️ [ElectricSQL vs PowerSync _202311](https://www.powersync.com/blog/electricsql-vs-powersync)

- On the surface, ElectricSQL and PowerSync have similar goals and enable similar outcomes for developers: Both are designed to be a drop-in sync layer for existing application stacks — offering bi-directional syncing of data between standard Postgres and client-side SQLite databases. 
- Both ElectricSQL and PowerSync provide:
  - Instant reactivity for your apps (by allowing your app front-end to work with a local SQLite database, with live queries)
  - Offline operation of apps (read and write to a local database, and then data syncs in the background automatically when connectivity is available — both systems use some kind of upload queue on the client-side)
  - Real-time multi-user collaboration (by keeping data in sync between users and devices in real-time)
  - Both use JWTs for authentication. 
  - Both use Postgres logical replication/the WAL to monitor the database for changes to be streamed to clients. 
  - Both provide causal consistency guarantees.

- Here’s a brief overview of the fundamental differences in architecture. 
- ElectricSQL architecture
  - Dynamic partial replication not yet available (controlling what data syncs to which users). Specifically, DDLX and Shapes functionality are not yet available.
  - Writes are made directly to your Postgres database via the Electric sync service (bypassing your backend application), using CRDTs to merge changes deterministically.
  - This means that custom business logic cannot be applied to writing changes to your database on the server-side.
  - Makes extensive modifications to your Postgres database (schema additions, additional storage, triggers and subscribing to a logical replication stream from the Electric sync service).
  - Sync controls are defined partly on the server-side (access control / permissions) and partly on the client-side (Shapes, controlling what data is synced).

- PowerSync architecture
  - Dynamic partial replication is available and production-ready. See PowerSync Sync Rules.
  - Writes are sent through your own application backend, allowing you to customize how they're handled: You can apply your own business logic, fine-grained authorization, validations and server-side integrations, you can resolve conflicts using the techniques/algorithms of your choosing, and you can reject changes from clients if needed.
  - Your backend is authoritative: After processing the write on your backend, the state will correctly and consistently replicate to clients.
  - This does mean that some additional work is required to implement writes. Writes and conflict resolution are not automatic like with ElectricSQL.
  - Does not make modifications to your Postgres database. Operation history is stored in the PowerSync Service.
  - Sync controls are defined on the server-side (Sync Rules) and can make use of dynamic parameters from the client.

- ElectricSQL writes directly to your Postgres database, using CRDTs to merge changes deterministically
- With ElectricSQL there is no custom server/backend mediating the interfacing with Postgres, and ElectricSQL uses Postgres as the exclusive “control plane” for the system. 
- As a result of the ElectricSQL architecture, server-side workflows cannot be triggered by your backend application. 
  - Therefore, ElectricSQL recommends triggering server-side workflows using event sourcing based off of database change events. 
  - This means adding an additional system/component to your stack for database event sourcing, and integrating your backend framework with that system.
- ElectricSQL applies predefined behavior to merging changes and resolving conflicts using CRDTs.
  - ElectricSQL does plan on eventually allowing the developer to select between different CRDTs/conflict-resolution policies, but this will still result in limited flexibility. 

- PowerSync’s authoritative backend architecture
- With PowerSync, writes are sent through your own application backend, allowing you to customize how they’re handled
- At PowerSync, we believe CRDTs have great strengths: For example, they are an excellent solution for collaborative document/text editing. 
  - Although ElectricSQL’s internal merge logic uses CRDTs, ElectricSQL does not provide a built-in solution for document/text collaboration using CRDTs. 
  - It would be a similar effort to implement document/text collaboration with either PowerSync or ElectricSQL. 
  - For example, you could use Yjs and store its CRDT data structure in Postgres using blob columns, with each row in the Postgres table representing a user edit/update (or each row representing a whole document).
- Another factor that developers should take into consideration is the degree to which they require any changes to the Postgres database.
- ElectricSQL makes various changes to your Postgres database:
  - Adds additional “shadow tables” to your schema, which store CRDT data which are used to merge changes. 
  - Adds triggers, for example to perform merge logic.
  - Subscribes to a logical replication stream from the ElectricSQL sync service — this is how changes are written into your database
  - It is also worth noting that Electric currently requires SUPERUSER privileges/permissions to your Postgres database. 
- PowerSync does not modify your Postgres:
  - Requires no modifications to your Postgres database except for enabling logical replication
  - Requires read-only permissions to your database (only the SELECT and replication privileges) 
- ElectricSQL’s architecture makes it tightly-coupled to your Postgres schema and configuration
- PowerSync is loosely coupled to Postgres, creating a layer of flexibility between your Postgres schema and configuration and the client-side SQLite schema.
# more
