---
title: lang-rust-dev-log
tags: [dev-log, rust]
created: 2025-04-10T02:57:18.262Z
modified: 2025-04-21T07:29:39.259Z
---

# lang-rust-dev-log

# guide

# discuss-stars
- ## 

- ## 

- ## 
# discuss-usage/tips
- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## 

- ## [Regex parse error at tracing-subscriber-0.3.16\src\filter\env\directive.rs:140:10 · Issue #2565 · tokio-rs/tracing _202304](https://github.com/tokio-rs/tracing/issues/2565)
- Seems like manually enable the `unicode-case` feature in `regex` inside the application `Cargo.toml` would work.

```toml
regex = { version = "1", features = ["unicode-case"] }
```
