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
# [WebFinger - Mastodon documentation](https://docs.joinmastodon.org/spec/webfinger/)
- WebFinger as described in RFC 7033 is a spec that defines a method for resolving links to a resource, given only a URI on a particular server. 
  - This allows anyone to look up where a resource is located without having to know its exact location beforehand; for example, by email or phone number. 
  - This lookup is directed at the endpoint `/.well-known/webfinger`, and a `resource` query parameter is passed along with the lookup. 
  - The resource URI used with Mastodon is the `acct:` URI as described in RFC 7565, with the username of a profile that is hosted on a particular domain.
- Because Mastodon heavily relies on mentions for addressing other profiles, WebFinger is required for fully interoperating with Mastodon. 
  - Mastodon’s internal logic depends almost completely on `acct:` URIs or `username@domain` representations. 
  - Searching for any objects or profiles from an ActivityPub implementation without WebFinger will fail because the author cannot be converted to a user in the local database.
