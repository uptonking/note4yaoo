---
title: lib-collab-logux-dev
tags: [collaboration, logux]
created: 2023-05-14T04:29:05.202Z
modified: 2023-05-14T04:30:34.915Z
---

# lib-collab-logux-dev

# guide

- features
  - collaborative using crdt
  - realtime/reactive using webSocket client/server framework
  - optimistic ui
  - offline-first with actions and merge-conflicts
  - no vender lock-in, works with any db
  - cross-tab communication in browser
  - compatibility between different client versions
  - 架构灵活，支持多框架，react/vue/django
  - Logux uses the peer-to-peer model. 

- cons
  - 案例少
# dev
- tips
  - version-history的效果可直接参考redux-devtools
  - logux client/server
  - nanostores提供persistent/router/query-fetch/logux-sync
# roadmap
- 如何持久化actions

- [WYSIWYG editor](https://github.com/logux/logux/issues/12)
# [Why I created Logux_202003](https://slides.com/ai/why-logux/)
- https://slides.com/ai/logux2#/94
  - logux is not a crdt, not a db
  - it's a framework to implement both

- autoprefixer is stable
  - time for a new adventure

- Simple AJAX works only on localhost
  - A lot of code even for simple edge cases, like loading/error/data

- Let’s forget about AJAX and dream about the perfect state sync for SPA
  - We have stores in our apps
- With extra code to sync state with server
- Feature 1: sync state without extra code
- Feature 2: sync state between tabs by default
- Feature 3: built-in authorization
  - Feature 3a: built-in client version
- Feature 4: Optimistic UI
  - Feature 4a: global UI for network errors
  - Feature 4b: Offline
- Feature 5: Collaborative First Apps
  - Feature 5a: Real-Time Updates
  - Feature 5b: The same changes order

- My own solution for client-server sync
- Proxy server for Web Sockets
- Logux Proxy re-send changes to clients
- Changes have time mark to keep order
# examples
- https://github.com/logux/examples
  - 仅支持单用户多窗口同步

- https://github.com/zumkorn/logux-simple-app
  - front+back

- https://github.com/meafmira/crdt-codeshare
  - App uses CRDT for collaborative editing and implement it through logux web framework.
# docs
- Logux synchronizes action log between peer-to-peer nodes.

- Each node has action log (list of operations). 
  - When you want to change the application state, you add an action to the log. 
  - An action is a JSON object that describes what happened. 
  - Every action must have a `type` property.
- Action log is append-only. You can only add actions, but can’t change or delete them. However, you can compress log by cleaning old actions, 

- Each `action` in the log has own `meta` with id/time/added/reasons

- Logux Client and Logux Server add `meta.subprotocol` with version of application-level protocol.

- Differences between action and meta:
  - Actions are immutable. But you can change meta (except meta.id, meta.added, and meta.time).
  - Logux synchronizes actions, but only meta.id, meta.time, and meta.subprotocol will be synchronized by default. Each Logux implementation decides what meta keys it will synchronize.

- You can use any method to connect Logux nodes. Logux uses WebSocket only as default way. 

- During the synchronization Logux guarantee:
  - Each action will be synchronized only once.
  - Actions will have the same order on each node.
- Logux is based on the Optimistic UI idea. 
  - When a node creates action, it applies it immediately to own application state. 
  - In the background, Logux will synchronize this new action with other nodes.

- If the node is offline right now, new actions will wait for a connection in the node’s log. 
  - Offline is a standard mode for Logux application.

- Logux client keeps only one WebSocket connection even if the user opens an application in multiple browser’s tabs. 
  - Logux clients in different elect one leader to keep the connection. 
  - If the user closes the leader tab, other tabs will re-elect a leader.

- in Logux subscriptions is a way to request data from the server.
- Clients or server should create an action to change data.

- We created Logux to have better UX in non-stable networks of the real world.
- Sending data to the server is a basic feature of any web application. 
  - Unfortunately, in production we have a lot of abstractions for AJAX: action creator, Promises, loader flags, HTTP parameters and body.
- In Logux we try to simplify the system. You have actions. 
  - You use these actions to change UI. 
  - And you use the same actions to communicate with servers. 
  - Back-end code works with the same action. 
  - And server response is actions as well.

- Logux keeps actions in memory. 
  - During the edit conflict, Logux will revert changes, get new actions from another client, and apply all changes in the right order. 
  - If action can’t be applied, Logux will automatically revert it and show a warning to the user.

- Optimistic UI us a pattern to accept changes in UI immediately without loader and waiting server response

- Logux uses WebSocket subscriptions instead of HTTP requests. 
  - Your application subscribes to some channel. 
  - The server sends the current state to the client during the subscription. 
  - If the server will receive action changing this data (with the same channel in meta.channels), the server will resend this new action to all subscribed clients.

## concepts

- Logux uses the peer-to-peer model. 
  - There is no big difference between client and server. 
  - This is why we call both client and server “nodes”.
- Logux Core provides BaseNode class, which will synchronize actions between two nodes. 
  - ClientNode and ServerNode classes extend this class with small behaviour changes.
- If a user opens a website with Logux in multiple browser tabs, tabs will elect one leader, and only this leader will keep the connection. If the user closes the leader tab, tabs will re-elect a new leader.

- Logux actions are very similar to Redux actions. 
  - JSON objects describe what was changed in the application state. 
- Actions are immutable. You can’t change action. 
  - If you want to change the data or revert changes, you need to add a new action.
  - All values should be serializable to JSON. 

- Adding actions to the log is the only way to change application state in Logux. The log is append-only. 
  - You can add action, but can’t change added action or change the state by removing actions from the log.

- Logux has a few built-in actions with logux/ prefix.
  - logux/undo
  - logux/subscribe

- 💡 By default, Logux will forget all unsaved actions if the user will close the browser before getting the Internet. 
  - You can change the log store to `IndexedStore` or you can show a warning to prevent closing browser

- The state describes all data of your application. 
  - On the client-side state describe UI state, data load from the server, user’s local changes. 
  - On the server-side state is what you have in the database.

- Logux Redux uses event sourcing pattern on client-side. 
  - Actions describe the current state. 
  - State object is just an cache.

- By default, Logux keeps last 1000 action (you can change it) and cache state every 50 actions to make time-travel faster.
- Logux Redux generates big JS object as application state. 

- By default, the server state is opposite to client state. 
  - Because server-side cache could be very big, the database is the single source of truth. 
  - You can use any database with Logux.
- Logux Server removes action after processing and always look to a database for the latest value. 
  - As a result, you can’t undo actions on the server.
  - However, you can change this behavior and have event sourcing on the server too.
- Every time when client subscribes to some data, server go to database and send initial value

- Logux Client wrapper such as Logux Redux and Logux Vuex keeps old actions and old state values.
  - Be default, they keep last 1000 actions. You can change it or implemented more complex logic. 
  - Logux wrapper saves state every 50 actions. 

- Logux Redux and Logux Vuex uses time travel to keep the same order of actions on all machines. 
  - It uses `ID` and `time` from `meta` to detect order and time travel to insert action in the right moment of history. 
  - Time travel is a technique when Logux Redux reverts recent actions, apply new action, and then re-apply recent actions.
- As a result, if the developer used atomic actions, conflict actions will override each other (“the last write wins” model). 
  - In complicated cases, you can define merge logic in reducers.
- By default, Server doesn’t use time travel, because the average state can’t be stored in the memory. 
  - You need manually compare action’s time and latest change time to implement “last write wins.” 
  - Similarly, you can implement any other conflict resolution logic.

- Offline support is easy in Logux. 
  - Logux will keep unsaved actions in the log and synchronize them later.

- Logux Redux uses event sourcing to deal with server error
  - In any moment server can send logux/undo action and client will revert changes of this action. 
  - Logux Redux will load the closest state snapshot and then re-apply all actions without reverted action.

- subscriptions and channels are the main way to get data from the server. 
  - It asks the server to send current data state and re-send all actions with these data changes.
- Channel is just a string like exchange-rate or users/14.
- The client remembers all the subscriptions. If the client loses connection, it will re-subscribe to channels again.

- users may use old client for weeks because they do not reload the page. especially for mobile
  - As a result, the **server needs to be able to speak with different versions of clients**. 
  - Logux has subprotocol versions to do it.
- Subprotocol is your application-level protocol:
  - What actions can be generated on the client and the server.
  - The schema of action’s objects.
  - The reaction on this actions.
- If the server doesn’t support the client’s subprotocol, it will refuse the connection and client will show “Please reload page” warning to the user.
- On the server you can have different logic for different clients by checking subprotocol version

## Logux Protocol

- Logux is a client-server communication protocol. 
  - It synchronizes actions between clients and server logs.
- You can use any encoding and any low-level protocol: JSON encoding over WebSocket, XML over AJAX and HTTP “keep-alive”.
- This protocol is based on simple JS types: boolean, number, string, array and key-value object.

- Communication is based on messages. 
  - Every message is a array with string in the beginning and any types next

- Logux uses Back-end Protocol to make a proxy between WebSocket and HTTP. 
  - Logux Server sends the user’s authentication requests, subscriptions, and actions to an HTTP server and receives new actions by HTTP to send them to Logux clients.
# more
- [Cool frontend arts of local-first: storage, sync, conflicts](https://evilmartians.com/chronicles/cool-front-end-arts-of-local-first-storage-sync-and-conflicts)

- [Collaborative real-time security: Logux for Akeero](https://evilmartians.com/chronicles/collaborative-real-time-security-logux-for-akeero)
