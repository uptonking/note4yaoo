---
title: lib-collab-crdt-community-tiny-merge
tags: [collaboration, community, crdt, tiny-merge]
created: 2023-08-01T08:58:09.146Z
modified: 2023-08-01T08:59:45.360Z
---

# lib-collab-crdt-community-tiny-merge

# guide

 

- resources
# discuss
- ## 

- ## 

- ## 

- ## How to compress causal graphs to tiny sizes.
- https://twitter.com/JungleSilicon/status/1740062478560903395
- These tricks were used by @josephgentle in diamond types.

- ## 🧐 let's talk about CRDTs. It's been a while.
- https://twitter.com/JungleSilicon/status/1729316660849627634
- A simple model of time is a linear sequence, kind of like those number lines from math class. Each change increments by one.
- it gives you a history of changes, which means you can rewind time. You can also query how things change *over time*.
- 🤔 what if you go back in time and then make a change? 
- Well, one way to handle this is just like the undo / redo stack. You can override any changes in the divergent timeline and force it into a linear sequence.
- Another solution might be a less destructive path where you do a diff between 1 and the new change and apply that diff to the end. This way, every state that has occurred is preserved. This is cool, but we lose something too. We now no longer know that 4 came from 1.
- Another way to represent this is to create a branch off 1. Now there are two timelines with the time 2. This has lost something too! You now don't know that the new 2 came *after* 3.
  - Alright, so let's change the way we label these nodes, now, instead of them being labelled with their sequence in time, they're labelled with the order in which the change occurred. You can tally the sequence in time by adding the number of elements from the beginning.
- 🤔 what if I want to merge that timeline back into the original one? 
- Well, we can always do a diff between the two and then apply those changes to the end of 3.
  - This is great, but we lose the causal relationship between the other timeline.
- Another way to represent this is that a new node has been added to the original timeline that *points* to 4. Now we know where the change originally came from *and* we have the correct state.
- 🤔 but how do I collaborate with others? 
- Let's go back to basics.
  - Imagine time as two linear sequences, one for each person. 
  - The problem here is that neither timeline has any knowledge of the other persons changes.
- One way to solve this is to allow changes to be parented off each others changes rather than just our own! These leads to needing changes to be able to have more than one parent.
- Ok so the numbers you saw before, they're called global sequence numbers, you get the latest sequence number you've seen and add 1 to it. There's also local sequence numbers, they're the ones in green and blue. They are the number of changes an agent has made since the start.
- There's also sequence numbers for fields or files, how many times has the position field been changed? What about the size field? These can be useful for rewinding time for a single field or file.

- ## 💡 How to build social reacts using CRDTs
- https://twitter.com/JungleSilicon/status/1676195595990732800
  - Each react-emoji has an index
  - Store each agents react in an object. The key is the agent id, the value is an index into the reacts
  - Agents that haven't reacted don't need to store a value
  - But we need to know which per agent is the latest. We compare the current react for that agent with the new change. Whichever value is highest wins.
- This pattern is an optimised version specifically for reacts, but you can **generalise it by using lamport clocks per agent** associated with a value and allowing multiple types of reducers to act on the same data. e.g. median, mean, sum, etc.

- ## I think there is quite a bit of potential in the CRDT space for pruning(修剪; 精简) using distributed reference counters. 
- https://twitter.com/JungleSilicon/status/1688782836533522432
  - (Keeping track of how many references there are to CRDTs that you're currently connected to).
- I see there are two main areas for pruning:
  - Is this a new operation that I have not seen before.
  - Can I clear some data or will one of my peers need to reference it via UID?  Reference counters could help with the latter.

- ## Applying a series of ranges (emphasis, strong, underline) to a series of characters
- https://twitter.com/JungleSilicon/status/1673728494260588547
  - Overlapping ranges is really the *hard case*.

- Yeah, I’ve been reading the peritext paper quite a lot lately. The algorithm needs to be slightly different for tiny merge, but the core ideas are the same.
  - The main difference is Tiny Merges use of paths rather than UIDs.

- ## If you use a sync engine that can sync arbitrary data...
- https://twitter.com/JungleSilicon/status/1678910691640754176
  - One of the *huge* benefits of data-driven libraries / notations is that creating a multiplayer version of that library is as simple as hooking it up to the store.
- When I hear "Syncing arbitrary data" I think "multi-value registers" (the CRDT term). If you need to match all structures how else do you do it?
  - You can use multi-value registers, last-writer-wins registers, lamport clocks or something OT based, it really depends on your use-case.

- It depends on your use-case, OT is generally less network agnostic. OT can be mixed with CRDTs (e.g. Diamond Types does something like this) for performance optimisations.

- ## I’ve found a simple way to explain the list CRDT I wrote.
- https://twitter.com/JungleSilicon/status/1685797755351179265
  - Each run by a single agent of consecutive inserts is grouped together.
  - Each insert is a node with a uid, parent uid and an offset.
  - All it’s doing is ‘stitching together local timelines’ where the runs start.
- What makes this interesting is that it separates sequence numbers(ie. array index) from their insert locations.
  - Sequence numbers are then only used for overriding values at the same position.
- Due to the built in run-length encoding, you reduce the dependency that each character has on the other characters and it’s easier to prune elements.
  - It also makes it possible to easily store their position as a path which entirely removes the dependency on other elements.

- Here’s an example of some inserts in the middle of someones run.
  - As you can see there is no need to create a fake element as there is already an element to parent off to the right.
- This CRDT does not have interleaving issues and it seems to fix the same issue that the fugue paper outlines too.

- This is interesting. While I see how this could be useful for text editors, can this be somehow extended for richtext? or is that out of scope?
  - So this is something i’ve been exploring recently and i’m not 100% sure yet, but it seems like some edge cases may not be ideal due to a loss of sequence information. We will see!

- ## There is raw data, then there are views into how you access & group it.
- https://twitter.com/JungleSilicon/status/1686244874725834752
- With Tiny Merge, I'm exploring how to lean into this so that:
  - references
  - hierarchy
  - ordering
  - names
- Are all properties of these views that look at the underlying data that can be mixed and matched.

- ## What I like about block types is that they are similar to file types.
- https://twitter.com/JungleSilicon/status/1686278078467911680
  - Through standardisation of block types you can create interoperable, high-level components that entirely side-step the data migration issue.
  - Looking through this lens - applications become more like interpreters that support specific block-types.
- I do believe that an extensible block based standard is more likely to be the future!

- ## I think it's possible to build a state-based BFT resistant CRDT.
- https://twitter.com/JungleSilicon/status/1637482087136788480
  - The general idea is for versions to be a combination of a sequence number and the value.
  - 👉🏻 Then if sequences hit the max possible value, you wrap them back around to zero and set a new parent uid.
  - When wrapping it around you must specify what you are overriding.
  - https://github.com/siliconjungle/Tiny-Merge-BFT

- Byzantine Fault Tolerant.
  - This solution is kind of *interesting*, its *mostly* eventually consistent, except for when agents have different "parents" (that should only change by bad actors).
  - Different parents is treated as a merge event before exchanging information.

- https://twitter.com/JungleSilicon/status/1637425083806539776
  - An interesting conclusion to trying to limit how many sequence numbers an agent can increase in a distributed system.
  - TLDR: You can only verify changes that you've seen.
  - Alternatively centralised systems & blockchains (which are kind of like centralised / decentralised systems) can also stop this.
  - If you have a full history you can undo changes that weren't supposed to occur. If you don't each agent needs to sign other agents changes before passing them along and then you can have a maximum of MAX_CHANGES * NUM_AGENTS.

- ## if anyone has novel solutions to this problem: sequence number can reach the max interger
- https://twitter.com/JungleSilicon/status/1636364948187250703
  - Another approach is to just restrict the amount a sequence number can grow by, but that feels imperfect.

- Do you mean in the context of an HLC? There’s only so much collaborative work you can do in a microsecond!
  - It's true, but it's more of an intellectual problem than anything for me.

- I faced a similar but not identical problem recently. Sharing my solution as an inspiration, I know it is not directly applicable. I needed a way to determine which items in a cache have not been used the longest.
  - It is an embedded and constrained system, so I needed something simple. I decided to label each item with MAX_INT initially, decrementing all labels by one on each cache access, the exception being the label of the actual element being accessed, which is reset to MAX_INT
  - When I hit 0, I just don't decrement anymore, so I lose the time ordering for the very very old items, but for those items the time ordering matters the least anyway. So, the trick was to accept a lossy scheme that loses the least valuable part of the information.
- is your idea like lru cache? just throw the very very old items away
  - Yes, but with the twist that I can let the age saturate and it's OK and that the code is simpler if I keep track of (MAX_INT - age) instead of age.

- ## I've begun building out a server tick rate for message sending in Tiny Merge._202211
- https://twitter.com/JungleSilicon/status/1597770904716865538
  - 轮询：Starting out with 30 messages per connection per second.
  - I'm thinking I'll eventually move to something like a minimum send rate and a maximum depending on activity.

- we should talk more, I'd argue for pull-based with some good use cases there.
- I think it depends on the kind of application you're building. 
  - For real-time applications like a game a tick-rate would be more ideal. 
  - For something like a notion or linear something pull-based could be more ideal.
- ooh yeah, I think about modern multiplayer techniques there and I agree with that.
  - rollback-based multiplayer I think is what I'm thinking of there.

- ## If anyone has been curious about how to build a CRDT but thought the idea was too daunting. tiny-merge-legacy_202205
- https://twitter.com/JungleSilicon/status/1526123548753858560
  - I've created one with as much of the complexity stripped out as I could whilst keeping it useful.
  - I call it Tiny CRDT.
  - Refactored it by separating the ram from the crdt & added a sequencer.

- https://github.com/siliconjungle/tiny-merge-ts
  - A Tiny CRDT library.
  - I converted the trimmed-down version of Tiny Merge to Typescript and swapped the objects out for maps.
  - https://github.com/siliconjungle/tiny-merge-ts/tree/feature-rich

- https://github.com/siliconjungle/tiny-merge-legacy
  - A tiny CRDT implementation in Javascript.

- ## The main trade offs between history and state based CRDT's is this:
- https://twitter.com/JungleSilicon/status/1559749305467957248
- History:
  - More capabilities (rewinding time, more complex merging logic).
  - Requires more storage.
  - Can have smaller network messages.
  - Is more complicated.
- State:
  - Simpler.
  - Less capabilities.
  - Less storage required.
  - Larger message sizes (especially on connect).

- ## It's becoming really clear that CRDT's become much more powerful and easy to reason about when you break them down into their tiniest pieces.
- https://twitter.com/JungleSilicon/status/1525515082876063750
  - Below I've separated where values are defined from the keys that reference them. This separation allows you to easily modify the data and change which keys point to which data in memory.
- https://github.com/siliconjungle/reference-crdt
  - An implementation of CRDT object references.

- ## I made a simple list CRDT that only supports push and replace operations. (No inserts before the end)._202204
- https://twitter.com/JungleSilicon/status/1511523633294094337
  - It requires no history and is extremely light-weight. Useful for things like message histories or posts.
