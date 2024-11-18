---
title: spec-format-protobuf-community
tags: [community, protobuf]
created: 2024-11-17T10:22:44.639Z
modified: 2024-11-17T10:22:56.761Z
---

# spec-format-protobuf-community

# guide

# discuss-stars
- ## 

- ## 

- ## 🆚️ I was crunching some numbers for JSON vs protobuf and the difference is staggering.
- https://x.com/arpit_bhayani/status/1857840494283468825
  - 2x improvement in data size
  - 2.5x improvement in serialization time
  - 4.5x improvement in deserialization time
  - no wonder protobuf has become a de-facto data format.

- But generally it is suggested to use protobuf only for inter-server communication not directly for clients. Is there any specific reason for it? Like why json is still preferred for browsers not protobuf if it is so advantageous
  - Because you spend a ton of time moving data/req/res over public internet (long distances) and the network latency overpowers the performance again of serialisation and deserialization.

- it's clear how significant network latency can be compared to JSON serialization/deserialization
  - Pinging https://google.com takes ~10 ms, about 1000 times more than the JSON serialisation/deserialisation time mentioned in @arpit_bhayani 's post

- Because browsers don't have native support for protobuf. Protobuf is recommended and designed to use for backend to backend

- If you think that’s fast, check out FastBinaryEncoding

- would be interesting to see benchmarks in comparision with simd json parser

- BJSON would perform much better but yeah not as good as protobuf.
# discuss-grpc
- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## 
