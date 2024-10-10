---
title: lang-rust-community-concurrency
tags: [community, concurrency, rust]
created: 2023-08-28T04:42:10.075Z
modified: 2023-08-28T04:43:32.352Z
---

# lang-rust-community-concurrency

# guide

# discuss
- ## 

- ## 

- ## 

- ## 

- ## 

- ## [What's the Benefit/Allure of Async/Await vs. CSP/Green Threads (and Other Concurrency Models)? : r/rust _202312](https://www.reddit.com/r/rust/comments/18ede5k/whats_the_benefitallure_of_asyncawait_vs_cspgreen/)
  - I come from a go background where we brush off questions about Async as ludicrous. In this community though, with more power over the runtime and language primitives, people seriously entertain Async/Await/Future style, why?
  - It seems that rust removed native green threads as against it's philosophy
  - there are good CSP, yet people really like e.g. Tokio for Async/Await (although it also has greenthreads!) What am I missing?
  - The Async/Await style seems far more complicated than wait groups, muxes, message passing and so on - since with CSP you just need to set up a few blockers, while in Await you need to promote things. So surely there must be a benefit I'm not understanding?

- The very long and short of it is (at least my opinion): Green threads were not the right option for Rust. This is not to say that green threads don't work, or are bad. In fact, they can be very good. But they just weren't the right fit for Rust. The reasons essentially boil down to:
  - It's a feature, not a bug, that Rust has a very minimal runtime (as close to "no runtime" as possible). We want Rust to be a suitable language for embedded systems and other environments where a featureful runtime would be a dealbreaker. You can always add on a runtime on top if you want (Tokio is essentially a runtime), but it must be optional and can't be first-party.
  - It's a feature, not a bug, that await points in a code block are explicit and not implicit. The reason why is that await points have major implications for code validity of things like lifetimes, non-moveable types, and ! Send types that are not allowed to be transferred between threads (such as a mutex guard or other special native types). You're allowed to do certain things between await points, and not certain things across await points, and this is a consequence of the existing Rust language rules regardless. This would be very messy if "basically anywhere could be an await point, if the compiler or runtime decided it should be".
  - The async/futures model in Rust was one of the best contenders for meeting the requirement of "as zero-cost as possible", a pre-existing goal of Rust. Green threads (or at least almost all implementations) tend to have some overhead not visible in your code, which was considered contrary to the overall Rust approach.
  - Most green thread models don't play very nice with FFI, which would be a huge problem for Rust because good FFI with C is actually a major selling point of Rust.

- Green threads require a complicated runtime and Rust decided not to have one.

- Green threads implementations in libraries can't fully implement what makes green threads good, for example they can't use segmented stacks (that really requires language support and a runtime).
- Moreover they still suffer from some of async/await problems:
  - io operations still need to be reimplemented to yield to the scheduler rather than blocking on a syscall, or they won't be efficient; 
  - lot of unsafe code assumes you can't leak stackframes, which suspendable APIs however inherently can, hence why scoped tasks are unsound. This is not different with green threads, see for example this issue in generator, the library that may uses for green threads.

- To expand on this, this was actually one of the discussion points when Rust's async was being designed. The fact that this design required a very low amount of special compiler support to allow libraries to take care of the rest was considered a desirable feature. We wanted to allow delegating to library implementations as much as possible, rather than needing to implement a significant chunk inside Rust proper.

- 
- 
- 

- ## tokio IS "thread-per-core" - the controversy in the Rust community is about a tradeoff between work-stealing and share-nothing
- https://twitter.com/withoutboats/status/1710279468206485941
  - [Thread-per-core - Without boats, dreams dry up](https://without.boats/blog/thread-per-core/)
- I have never implemented work-stealing approach so cannot really comment on its effectiveness. My paper was investigating the impact of thread-per-core (with partitioning) on tail latency in comparison to traditional share-everything model. As you rightly point out in your post, you cannot draw any conclusions from my findings about partitioning vs. work stealing.
- I’ve always referred to thread-per-core with work-stealing as thread-per-core-until-things-get-tough. It’s a slippery slope from work-stealing to not pinning threads to CPUs but yeah usually the hot partition issue is the motivator for WS
