---
title: lib-collab-ot
tags: [collaboration, lib, ot]
created: 2021-10-14T10:55:05.828Z
modified: 2022-04-05T10:09:36.436Z
---

# lib-collab-ot

# guide

# dev

## [OT wiki](https://en.wikipedia.org/wiki/Operational_transformation)

- Various transformation properties for ensuring OT system correctness have been identified. 
  - These properties can be maintained by either the transformation control algorithm or by the transformation functions.
  - Different OT system designs have different division of responsibilities among these components. 
  - The specifications of these properties and preconditions of requiring them are given below.

- Convergence properties
  - CP1/TP1: For every pair of concurrent operations {\displaystyle op_{1}}op_{1} and {\displaystyle op_{2}}op_{2} defined on the same state, the transformation function T satisfies CP1/TP1 property if and only if
  - CP2/TP2: For every three concurrent operations {\displaystyle op_{1}, op_{2}}op_{1}, op_{2} and {\displaystyle op_{3}}op_{3} defined on the same document state, the transformation function T satisfies CP2/TP2 property if and only if

- Inverse properties
