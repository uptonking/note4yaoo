---
title: lib-collab-crdt-blog-stars
tags: [blog, crdt]
created: 2023-03-11T15:37:35.868Z
modified: 2023-03-11T15:37:59.134Z
---

# lib-collab-crdt-blog-stars

# guide

# blogs

## [A comprehensive study of Convergent and Commutative CRDT_201101](https://www.researchgate.net/publication/50949847_A_comprehensive_study_of_Convergent_and_Commutative_Replicated_Data_Types)

- Sets constitute one of the most basic data structures. 
  - Containers, Maps, and Graphs are all based on Sets.
- We consider mutating operations add (takes its union with an element) and remove (performs a set-minus). 
  - Unfortunately, these operations do not commute. 
  - 👉🏻 Therefore, a Set cannot both be a CRDT and conform to the sequential specification of a set.
- Thus, a CRDT can only approximate the sequential set. 
- The CALM Theorem states that anything that is logically monotonic (read: append-only) can be made into a CRDT. Non-monotonic things may ‘retract’(收回；否认) previous statements.

- Two-Phase Set (2P-Set)
  - It combines a G-Set for adding with another for removing; the latter is colloquially known as the tombstone set. 
  - To avoid anomalies, removing an element is allowed only if the source observes that the element is in the set.
