---
title: lib-collab-fluid-docs
tags: [docs, fluid-framework]
created: 2023-02-11T11:06:54.804Z
modified: 2023-02-11T11:07:05.558Z
---

# lib-collab-fluid-docs

# guide

- not-yet
  - 如何集成现有json
# [faq](https://fluidframework.com/docs/faq/)

## Can the Fluid Framework be used in a situation without access to the internet?

- In order to keep all clients in sync, they must be connected to a Fluid service.

- Clients do have to be connected to the Fluid service. 
  - Fluid can tolerate brief network outages and continue operating but eventually the promise of being able to merge local changes weakens. 
  - We are investigating ways to improve this using other merging techniques designed to reason over large deltas but no final solution is in place today.

- In principle there is nothing preventing an organization from hosting a Fluid service on an intranet. However, Microsoft has no plans to support that scenario directly.

## Does Fluid use operational transforms?

- Fluid does not use Operational Transforms (OTs), but we learned a tremendous amount from the literature on OT. 
- While OT uses operations that can be applied out of order by transforming operations to account for recent changes, Fluid relies on a Total Order Broadcast to guarantee that all operations are applied in a specific order.

## Does Fluid use CRDT?

- Fluid does not use Conflict-Free Replicated Data Types (CRDTs), but our model is more similar to CRDT than OT. 
- The Fluid Framework relies on update-based operations that are ordered using our Total Order Broadcast to prevent conflicts. 
- This allows us to have non-commutative operations because there is an explicit ordering.

## How does Fluid Framework deal with conflict resolution?

- Conflict resolution is built into the DDSes, and the strategies vary between DDSes. 
  - For example the `SharedMap` uses a last-write-wins approach, whereas `SharedString` attempts to apply all changes while preserving user intention. 
  - The strategies used by each DDS are detailed on their respective documentation pages.

- Can we create custom strategies to handle update collisions to the distributed data structure?
  - Yes. You can design your own DDSes with your own strategies for handling merge. You also have access to all operations and can write client code to reason over state in whatever way best suits your scenario.

## Can we have history of the changes?

- Yes. Fluid inherently keeps all changes and these are accessible through the framework. 
  - The only caveat is that for performance and storage efficiency, operations need to be summarized from time to time. 
  - This may cause a loss of granularity.

## What is a DDS?

- DDS is short for distributed data structure. DDSes are the foundation of the Fluid Framework.
- Any practical limits on the types of data and size of a DDS will be specific to the implementation of that DDS. 
  - DDSes can contain text, images, and other binary data and can effectively be any size. 
  - However, managing scale on the client requires thought, just as it does when working with local data.

## Where is the data stored?

- The specifics of data storage (both session data and persistent data) will depend on the implementation of the Fluid service. 
  - There is a great deal of flexibility here and developers of Fluid services may choose to offer options around where and how data is stored.

- There are two classes of data storage to discuss
- **Session storage** is managed by the Fluid service and is, essentially, a central record of all the operations (ops) performed on the DDSes. 
  - This record is used by the Fluid clients to produce identical local instances of the DDSes. 
  - Session storage also includes ops that summarize all past operations to improve performance for clients that join sessions later and for efficiencies when saving to persistent storage.

- **Persistent storage** is a record of ops (and summary ops) saved outside of the Fluid service. 
  - This could be a database, blob storage, or a file. 
  - Using persistent storage allows a Fluid solution to persist across sessions. 
  - For example, current Microsoft 365 Fluid experiences save ops in .fluid files in SharePoint and OneDrive. 
  - It is important to note that these files share many of the properties of a normal file such as permissions and a location in a file structure, but because these experiences rely on the Fluid service, downloading the files and working locally is not supported.

## How is data synchronized?

- Fluid service’s core responsibility is sequencing all the incoming Fluid operations and then broadcasting them to all clients. 
- Because the ops are ordered, and because each client is running the same code, the DDSes in each client eventually end up in an identical state.
- Fluid clients connect to the Fluid service using the WebSocket protocol. However, the Fluid runtime manages all of the connections so that Fluid client developers can focus on local experiences.

## Is the Fluid reference server implementation production-ready?

- No. Routerlicious on its own is not production-ready.
  - Using it would require more thought about storage, scale, security, and other typical considerations when building out a service on the internet. 
  - It is our expectation that most Fluid developers will be able to leverage existing Fluid services that will emerge as we approach version 1.0.

- 
- 
- 
- 
- 
- 
- 
- 

## 

## 

# docs
- FluidFramework /4.2kStar/MIT/202302/ts
  - https://github.com/microsoft/FluidFramework
  - https://fluidframework.com/
  - Library for building distributed, real-time collaborative web applications
  - cons
    - 依赖中心服务器转发op及定顺序
    - 不支持长时间的offline，但只要保存op就可合并

- examples-官方示例，共用服务器tinylicious(npm run start:debug)
  - textarea示例未渲染协作鼠标
  - prosemirror示例是单页面多实例
  - shared-text是自定义编辑器，光标靠方向键移动，可显示协作用户光标
  - canvas画布示例是单页面多实例
  - canvas-data-object-grid示例支持在新标签页编辑部分画布元素，多页面
  - view-fwk-sampler使用了react/vue/vanillajs 3个示例
  - table-view提供了类似excel的示例，基于自定义table-document作为model
  - tips
    - 安装依赖用pnpm i

## overview

- Fluid Framework is a collection of client libraries for distributing and synchronizing shared state. 
- Fluid Framework offers:
  - Client-centric application model with data persistence requiring no custom server code.
  - Distributed data structures with familiar programming patterns.
  - Very low latency.
- The developers at Microsoft have built collaboration into many applications, but many required application specific server-side logic to manage the collaborative experience. 
  - The Fluid Framework is the result of Microsoft’s investment in reducing the complexity of creating collaborative applications.
- To keep the server simple, each Fluid client is responsible for its own state. 
  - While previous systems keep a source of truth on the server, the Fluid service is responsible for taking in data operations, sequencing the operations, and returning the sequenced operations to the clients. 
  - Each client is able to use that sequence to independently and accurately produce the current state regardless of the order it receives operations.

- The following is a typical flow.
  1. Client code changes data locally.
  2. Client Fluid runtime sends that change to the Fluid service.
  3. Fluid service sequences that operation and broadcasts it to all clients.
  4. Client Fluid runtime incorporates that operation into local data and raises a “valueChanged” event.
  5. Client code handles that event (updates view, runs business logic).

- The core technology powering Fluid Framework is mature and stable. 

## [concepts](https://fluidframework.com/docs/build/overview/)

- Service
- Fluid clients require a centralized service that all connected clients use to send and receive operations. 
  - Fluid offers multiple service implementations that developers can use without any modifications.
- Each service-specific library adheres to a common API structure and has the primary goal of creating and retrieving container objects. The common structure enables you to switch from one service to another with minimal code changes. 
- There are two services currently available:
  - The Tinylicious service runs on your development computer and is used for development and testing.
  - Azure Fluid Relay runs in Azure and enables high-scale production scenarios.

- Container
- It consists of a collection of shared objects and supporting APIs to manage the lifecycle of the container and the objects within it. 
  - New containers must be created from a client, but are bound to the data stored on the supporting server. 
  - After a container has been created, it can be accessed by other clients.

- Shared objects
- A shared object is any object type that supports collaboration (simultaneous editing). 
- The fundamental type of shared object is called a Distributed Data Structure (DDS). 
  - A DDS holds shared data that the collaborators are working with.
- Fluid Framework supports a second type of shared object called Data Object.
  - A Data Object contains one or more DDSes that are organized to enable a particular collaborative use case. 
  - DDSes are low-level data structures, while Data Objects are composed of DDSes and other shared objects. 
  - Data Objects are used to organize DDSes into semantically meaningful groupings for your scenario, as well as providing an API surface to your app’s data.

## [Containers](https://fluidframework.com/docs/build/containers/)

- It allows a group of clients to access the same set of shared objects and co-author changes on those objects. 
  - It is also a permission boundary ensuring visibility and access only to permitted clients.

- When you load a container, the Fluid service will also return a service-specific services object. 
  - This object contains references to useful services you can use to build richer apps. 
  - An example of a container service is the Audience, which provides user information for clients that are connected to the container.

- A Fluid container can be attached or detached. 
  - An attached container is connected to a Fluid service and can be loaded by other clients. 

## [Data modeling](https://fluidframework.com/docs/build/data-modeling/)

- Your application can declaratively define a set of shared objects that are immediately and always available to all clients; 
  - or, for more complex scenarios, your application can create shared objects at runtime only when a user takes a particular path through the application.

- The most straightforward way to use Fluid is by defining initial objects that are created when the Fluid container is created, and exist for the lifetime of the container.
  - Initial objects are always connected

- A shared object can be created by the container at runtime. 
  - Dynamic objects are both created and loaded dynamically. 
  - When your code creates an object dynamically, it must store a reference to the object within another shared object so that your code can later retrieve it.
  - Dynamically created objects are local only (in-memory) and cannot be shared with other clients unless a reference to each of them is stored in a connected shared object.
- Dynamic objects are more difficult to work with than initial objects, but are especially valuable in two scenarios:
  - When the app has a very large data set. Because dynamic objects are loaded into memory on demand, using them can reduce boot time of your application by delaying when the objects are loaded.
  - When the data needed by the app will vary depending on choices made by the user. Dynamic objects are also not strictly defined in the container schema. This enables your app to create containers with flexible, user-generated schemas.
- An example where this is useful is building a collaborative storyboarding application.
  - By using a dynamic shared object for each board, your code can load the boards on demand as the user accesses them, instead of having to load them all in memory at once.

## [Architecture](https://fluidframework.com/docs/concepts/architecture/)

- The Fluid architecture consists of a client and service. 
  - The client contains the Fluid loader and the Fluid container. 
  - The Fluid loader connects to the Fluid service and loads a Fluid container.
- The Fluid loader contains a document service factory, code loader, scopes, and a URL resolver. 
- The Fluid runtime is encapsulated within a container, which is built using Shared objects and distributed data structures.
- A Fluid container includes state and app logic. 
  - It’s a serverless app model with data persistence. 
  - It has at least one shared object, which encapsulates app logic. 
  - Shared objects can have state, which is managed by distributed data structures (DDSes).
- DDSes are used to distribute state to clients. 
  - Instead of centralizing merge logic in the server, the server passes changes (aka operations or ops) to clients and the clients perform the merge.

- The service also stores old operations, accessible to clients through a DeltaStorageService object, and stores summaries of the shared objects. 
  - It’s worth discussing summaries at length, but for now, consider that merging 1, 000, 000 changes could take some time, so we summarize the state of the objects and store it on the service for faster loading.

## [Total order broadcast & eventual consistency](https://fluidframework.com/docs/concepts/tob/)

- Operations describe changes to a data structure. 
  - By chaining a series of operations together we can represent changes to a data structure over time (history). 
  - When clients receive operations, they apply those operations to their local data.
- However, just sending operations is not enough – we need to be sure that each client applies the operations in the right order.
- Fluid is, at its core, a data model for distributed state.
- Fluid guarantees eventual consistency via total order broadcast. 
- That is, when a DDS is changed locally by a client, that change – that is, the operation – is first sent to the Fluid service, which does three things:
  - Assigns a monotonically increasing sequence number to the operation; this is the “total order” part of total order broadcast.
  - Broadcasts the operation to all other connected clients; this is the “broadcast” part of total order broadcast.
  - Stores the operation’s data (see data persistence).
- This means that each client receives every operation relayed from the server with enough information to apply them in the correct order. 

- Operations
- Fluid is also efficient when communicating with the server. 
  - When you change a data structure, Fluid doesn’t send the whole data structure to the server. 
  - Rather, it sends operations. 
- The Fluid service is responsible for storing ops and their accompanying data. 
  - It’s important that the server stores the ops themselves, because in order for a new client to sync their local state to the state of all the other clients, the new client needs to retrieve ops from the server to apply locally. 
  - When a new client connects, the server will send it all necessary ops (more precisely, the client will request the ops from the server) to bring it to a consistent state with all other clients. 
  - This is managed by the Fluid runtime.

- Summary operations
- As the number of operations increases, replaying all ops when loading a Fluid data structure is inefficient. 
  - Fluid provides a specialized operation, called a Summary operation, to address this. 
  - a Summary operation is one that summarizes all previous operations. 
  - Thus, a Summary op represents the state of Fluid data structures at a particular sequence number.
- Summary ops, like all Fluid operations, are created by the client. 
  - The Fluid runtime will automatically create summaries at opportune(恰当的) moments. 
  - The Summary op is created by a single client selected from the connected clients.
- The Summary op is unique in that it is ignored by connected clients. 
  - The Summary op is primarily a message to the Fluid server that it needs to store a new summary. 
  - If the operation is valid, then the server will commit the summary to storage and broadcast an event to the connected clients acknowledging that the summary was stored. 
  - In normal operation the clients will ignore both the summary op itself and the acknowledgement, since connected clients already receive all ops and are thus already consistent.
- Summary ops summarize the state of distributed data structures, so Data Objects (which are a collection of distributed data structures) don’t need to do anything to participate in summarization; it happens automatically, and all Data Objects’ data structures will be summarized.

## [Handles](https://fluidframework.com/docs/concepts/handles/)

- A Fluid handle is an object that holds a reference to a collaborative object, such as a DataObject or a distributed data structure (DDS).
- The primary use case for handles in the Fluid Framework is for storing a DDS or DataObject into another DDS. 

- Shared objects, such as Data Objects or DDSes, cannot be stored directly in another DDS. 
- There are two primary reasons for this:
  - Content stored in a DDS needs to be serializable. Complex objects and classes should never be directly stored in a DDS.
  - Frequently the same shared object (not merely a copy) has to be available in different DDSes. The only way to make this possible is to store references (which is what a handle is) to the collaborative objects in the DDSes.

- Handles encapsulate where the underlying object instance exists within the Fluid runtime and how to retrieve it. This reduces the complexity from the caller by abstracting away the need to know how to make a request to the Fluid runtime to retrieve the object.

- Handles enable the underlying Fluid runtime to build a dependency hierarchy. 
  - This will enable us to add garbage collection to the runtime in a future version.

## [Summarizer](https://fluidframework.com/docs/concepts/summarizer/)

- Summaries are client-generated snapshots of the state of the document at a given sequence number. 
  - A summary is a consolidation of the operation (op) log into one JSON blob.
- Why have summaries?
  - Summaries allow new clients to quickly catch up to recent state.
  - Without a summary, the client would have to apply every operation in the op log, even if those operations no longer affected the current state (e.g. op 1 inserts ‘h’ and op 2 deletes ‘h’). For very large op logs, this would be very expensive.
  - Instead, when a client joins a collaborative document, they can instead download a summary of the document state, and simply process new operations from that point foreward.

- Summary lifecycle
- The runtime generates summary tree
  - The timing of the summaries is determined by a few heuristics discussed below
- The runtime uploads summary tree to the Fluid Service storage (Historian), which returns a handle to the data.
- The runtime submits a “summarize” op to the server containing that uploaded summary handle.
- The ordering service on server stamps and broadcasts the “summarize” op.
- Another service on server responds to “summarize” op
- The runtime watches for “summaryAck”/“summaryNack” ops, using them as input to its heuristics determining when to generate summaries

- Summaries take the form of a tree consisting of blobs. 
  - Each layer in the tree is parallel to a part of the runtime model. 
  - The root node corresponds to the Container, and it contains the protocol information as well as any partially processed chunk op data.
- when uploading a summary, handles can be used in place of trees or blobs. 
  - Handles are pointers to nodes within the previous tree. 
- The handle itself is just a full path to the node it is referencing

## [Introducing distributed data structures](https://fluidframework.com/docs/build/dds/)

- The Fluid Framework provides developers with two types of shared objects: distributed data structures (DDSes) and Data Objects. 
- Data Objects are composed of DDSes and other shared objects.
  - Data Objects are used to organize DDSes into semantically meaningful groupings for your scenario, as well as providing an API surface to your app’s data. 
- However, many Fluid applications will use only DDSes.
- DDSes automatically ensure that each client has access to the same state. 
  - They’re called distributed data structures because they are similar to data structures used commonly when programming, like strings, maps/dictionaries, and sequences/lists. 
  - The APIs provided by DDSes are designed to be familiar to programmers who’ve used these types of data structures before. 
- When using a DDS, you can largely treat it as a local object. Your code can add data to it, remove data, update it, etc. However, a DDS is not just a local object. A DDS can also be changed by other users that are editing.
- When a DDS is changed by any client, it raises an event locally. Your code can listen to these events so that the app knows when data is changed and can react appropriately.

- In a distributed system like Fluid, it is critical to understand how changes from multiple clients are merged. 
  - Understanding the merge logic enables you to “preserve user intent” when users are collaborating on data.
- In Fluid, the merge behavior is defined by the DDS. 
- 👉🏻 The simplest merge strategy, employed by key-value distributed data structures like SharedMap, is last writer wins (LWW). 
  - With this merge strategy, when multiple clients write different values to the same key, the value that was written last will overwrite the others.

- Fluid DDSes exhibit different performance characteristics based on how they interact with the Fluid service. 
  - The DDSes generally fall into two broad categories: optimistic and consensus-based.

- Optimistic DDSes apply Fluid operations locally before they are sequenced by the Fluid service. 
  - The local changes are said to be applied optimistically in that they are applied before receiving confirmation from the Fluid service, hence the name optimistic DDSes.
  - Many of the most commonly used DDSes are optimistic, including `SharedMap`,         `SharedSequence`, and `SharedString`.

- Consensus-based DDSes are different from optimistic DDSes because they wait for confirmation from the Fluid service before applying operations – even local operations. 
  - These data structures offer additional behavior guarantees and can be used when you need atomicity or synchronous behavior.
- An example of a consensus-based DDS in Fluid Framework is the `TaskManager`.
- To understand why consensus-based DDSes are useful, consider implementing a stack DDS.
- A consensus-based DDS does not optimistically apply local ops. 
  - Instead, these DDSes wait for the server to apply a sequence number to the operation before applying it locally. 
  - With this approach, when two clients pop, neither makes any local changes until they get back a sequenced op from the server. 
  - Once they do, they apply the ops in order, which results in consistent behavior across all remote clients.

- Distributed data structures can store primitive values like numbers and strings, and JSON serializable objects. 
- For objects that are not JSON-serializable, like DDSes, Fluid provides a mechanism called handles, which are serializable.
- When storing a DDS within another DDS, your code must store its handle, not the DDS itself.

- Because distributed data structures can be stored within each other, you can combine DDSes to create collaborative data models
- The following two questions can help determine the best data structures to use for a collaborative data model.
  - What is the granularity of collaboration that my scenario needs?
  - How does the merge behavior of a distributed data structure affect this?
- You likely have more than one shape in your data model, so you could create a SharedMap object to store all the shapes, then store the SharedMaps representing each shape within that parent SharedMap object.

## [User presence and audience](https://fluidframework.com/docs/build/audience/)

- The audience is the collection of users connected to a container. 
- When creating a container, your app is also provided a container services object which holds the audience. 
  - This audience is backed by that same container. 
- Typically a user will only have one connection, but scenarios such as loading the container in multiple web contexts or on multiple computers will also result in as many connections. 
  - An audience member will always have at least one connection. 
- Connections can be short-lived and are not reused. 
  - A client that disconnects from the container and immediately reconnects will receive an entirely new connection. 
  - The audience will reflect through its member leaving and member joining events.

- While the audience is the foundation for user presence features, the list of connected users does not provide a compelling experience on its own. 
- Building compelling presence features will involve working with additional user data. 

- SHARED PERSISTED DATA
  - Most presence scenarios will involve data that only a single user or client knows and needs to communicate to other audience members. 
  - Some of those scenarios will require the app to save data for each user for future sessions. 
  - For example, consider a scenario where you want to display how long each user has spent in your application.
  - An active user’s time should increment while connected, pause when they disconnect, and resume once they reconnect. This means that the time each user has spent must be persisted so it can survive disconnections.

- SHARED TRANSIENT DATA
  - Many presence scenarios involve data that are short-lived and do not need to be persisted. 
  - For example, consider a scenario where you want to display what each user has selected in the UI.
  - Each user will need to tell other users their own information – where they clicked – but the past data are irrelevant.
- You can address this scenario using DDSes in the same way as with the persisted data scenario. 
- However, using DDSes results in storage of data that are neither useful long term nor in contention among multiple users or clients. 
  - Signals are designed for sending transient data and would be more appropriate in this situation. 
  - Each user can broadcast a signal containing their selection data to all connected users, and those users can store the data locally. 
  - Newly connected users can request other connected users to send their selection data using another signal. 
  - When a user disconnects, the local data are discarded.

- UNSHARED DATA
  - In some cases, the user data could be generated locally or fetched from an external service. 
  - For example, consider a scenario where you want to display the connected users with a profile picture and a color border
  - If your app retrieves a user’s profile picture from a user metadata service and assigns each user a color based on a hash of their user ID, then the app will have the desired data on other users without needing to communicate with them.

## [Types of distributed data structures](https://fluidframework.com/docs/data-structures/overview/)

- A distributed data structure behaves like a local data structure. 
  - Your code can add data, remove data, update existing data, etc. However, a DDS is not a local object. 
- A DDS can also be changed by other clients that expose the same parent container of the DDS.
- Meaning of 'simultaneously'
  - Two or more clients are said to make a change simultaneously if they each make a change before they have received the others’ changes from the server.
- Choosing the correct data structure for your scenario can improve the performance and code structure of your application.
- DDSes vary from each other by three characteristics:
  - Basic data structure: For example, key-value pair, a sequence, or a queue.
  - Client autonomy(自治) vs. Consensus(共识): An optimistic DDS enables any client to unilaterally(单方地) change a value and the new value is relayed to all other clients, while a consensus-based DDS will only allow a change if it is accepted by other clients via a consensus process.
  - Merge policy: The policy that determines how conflicting changes from clients are resolved.

- Key-value data structures are the most common choice for many scenarios.
  - User preference data.
  - Current state of a survey.
  - The configuration of a view.

- Sequence scenarios
  - Tabular data
  - Timelines
  - Lists
- Store only immutable data as an item in a sequence. 
  - The only way to change the value of an item is to first remove it from the sequence and then insert a new value at the position where the old value was. 
  - But because other clients can insert and remove, there’s no reliable way of getting the new value into the the desired position.

- SharedString – a data structure for handling collaborative text.

- Consensus data structures have one or both of these characteristics:
  - Only one client can perform a particular action on a particular data item, such as pull an item off of a queue.
  - An action, such as changing a value, can occur only when all clients consent to it.
- These DDSes are not optimistic. Before a change to a consensus data structure is confirmed, the connected clients must acknowledge the change.
- TaskManager – Tracks queues of clients that want to exclusively run a task.
- Typical scenarios require the connected clients to “agree” on some course of action.
  - Import data from an external source. (Multiple clients doing this could lead to duplicate data.)
  - Upgrade a data schema. (All clients agree to simultaneously make the change.)

## [Tutorial: DiceRoller application](https://fluidframework.com/docs/start/tutorial/)

- Tinylicious is the Fluid Framework’s local testing server, and a client is responsible for creating and loading containers.
- The app creates Fluid containers using a schema that defines a set of initial objects that will be available in the container

- Create a Fluid container
- 👉🏻 Fluid data is stored within containers, and these containers need to be created before other users can load them. 
  - Since creation and loading of containers both happen in the browser, a Fluid application needs to be capable of handling both paths.
- The `attach` call publishes the container to the Tinylicious service and returns the `id` of the container, which the app can use to load this container on other clients (or this client in a future session). 
  - Once attached, any further changes to the shared objects, made by the rendered app, will be communicated to all collaborators.
- When loading a container, the container already contains data, and is already attached

- Write the dice view
- The Fluid Framework is agnostic about view frameworks and it works well with React, Vue, Angular and web components.

- Connect the view to Fluid data
- assigns a handler to the click event of the “Roll” button. 
- Instead of updating the local state directly, the button updates the number stored in the value key of the passed in diceMap. 
- 👉🏻 Because the diceMap is a Fluid `SharedMap`, changes will be distributed to all clients. 
- Any changes to the diceMap will cause a `valueChanged` event to be emitted, and an event handler can trigger an update of the view.
- This pattern is common in Fluid because it enables the view to behave the same way for both local and remote changes.

- To keep the data up to date as it changes an event handler must be set on the diceMap to call updateDice each time that the valueChanged event is sent. 
- Note that the valueChanged event fires whenever the diceMap value changes on any client; that is, when the “Roll” button is clicked on any client.
  - 本地点击触发的更新或是远程发来的更新，都会触发执行update方法更新view
# more
