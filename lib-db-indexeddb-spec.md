---
title: lib-db-indexeddb-spec
tags: [database, indexeddb, spec, web]
created: 2022-11-18T17:01:26.836Z
modified: 2022-11-18T17:01:54.103Z
---

# lib-db-indexeddb-spec


# guide


# [Indexeddb API 3.0 Spec](https://www.w3.org/TR/IndexedDB/)

## key
- in-line key: A key that is stored as part of the stored value.

- An object store optionally has a key path. 
  - 👉🏻 If the object store has a key path, it is said to use in-line keys. 
  - Otherwise it is said to use out-of-line keys.
- An object store optionally has a key generator.
  - A key generator is used to generate keys for records inserted into an object store if not otherwise specified.
- Every object store that uses key generators uses a separate generator. That is, interacting with one object store never affects the key generator of any other object store.

## keypath 决定key自身的值

- The key is the value inside the keypath. 

- A key path is a string or list of strings that defines how to extract a key from a value. 

- { foo: { bar: "bla" } }
  - If you want to query the bar property the keypath will be "foo.bar"
