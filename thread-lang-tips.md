---
title: thread-lang-tips
tags: [lang, thread]
created: 2021-04-30T11:09:55.766Z
modified: 2021-04-30T11:10:26.083Z
---

# thread-lang-tips

# guide

# discuss-stars
- ## 

- ## 

- ## 1 billion nested loop iterations
- https://x.com/BenjDicken/status/1861072804239847914
  - https://benjdd.com/languages
  - https://github.com/bddicken/languages
  - Java and Kotlin are quick! Possible explanation: Google is heavily invested in performance here.
  - Js is really fast as far as interpreted / jit languages go.
  - Python is quite slow without things like PyPy.
- Have you seen the 1 billion row challenge from @gunnarmorling ? https://morling.dev/blog/one-billion-row-challenge/ also compares different languages, see the Show and Tell list

- Implementing the code identically in different languages instead of using recommended patters skews the results, even while sticking to built-in functionality. Example: by using list comprehension in Python it'll run at the same speed as Ruby
# discuss-ruby
- ## 

- ## 

- ## 

- ## 

- ## 看最近 ruby on rails 更新，居然连 cache 和 queue 的 client 和 server 端都内置了，这就是我最最喜欢的做事方式啊
- https://x.com/xqliu/status/1832305066730049540
- 不好招人确实是个挺大的问题~ 不过对于小团队或者甚至个人创业者来说，我觉得这个问题应该还好，比大公司或者大团队的影响应该小得多，你觉得呢？
  - 不好招人的另一个点生态差，别人都git clone copy paste 跑起来上线验证完需求了，你还在读ruby的语法以及rails 内部 patch 了那些 ruby 语法。

- gitlab, openproject 等等我见到很多大型多人协作工具都是ruby on rails搭建的，确实很棒。 但用ruby on rails搭建的软件总有种老后端开发的感觉
  - 说到老，我们平台是 Jvm 的，国内企业客户大部分要求要用java，老开发用老后端，完美
# discuss-lisp/elixir
- ## 

- ## 

- ## 

- ## 🆚️ [What are the main benefits of Elixir compared to Clojure? _202003](https://elixirforum.com/t/what-are-the-main-benefits-of-elixir-compared-to-clojure/29959)
- The good thing about Elixir (and Erlang) lies in the concurrency - it’s all about creating parallel process and sending messages - and this (as Alan Kay has pointed out on numerous occasions) is the essence of OO programming. OO programming is all about objects. 

- Erlang and Elixir (and likely any BEAM language) give you:
  - 99% transparent parallelism and concurrency. I can’t stress enough how important this is and how I spent 15 years of my career trying to emulate this trait in at least 5 other languages (and failed like everyone else who tried the same).
  - Lag-less operation: spawn 50_000 tasks and the runtime will give them all a fair treatment for as much as the hardware allows.
  - Pre-emptive scheduling. No single task can slow down the others.
  - Ability to structure your software as a tree of tasks and supervisors, with the supervisors restarting tasks if they fail. The so-called fault tolerance. This is EXTREMELY underrated and people usually come looking for this in Erlang and Elixir after suffering in other ecosystems for a long time. I haven’t met a single new programmer who is able to appreciate how much of a productivity boost and a reducer of stress this feature is but oh well, what can you do.
  - Elixir-specific: macros. Basically code generators at compile time. Another vastly underrated productivity booster.
- While other 30-year old languages like OCaml are still struggling to even produce a working multithreaded runtime (hope it doesn’t take them another decade to make an actor runtime!), and others like Rust are just now laying the foundations of a solid asynchronous multicore runtime (and Go never being that impressive in that regard to begin with), Erlang has been enjoying a multicore pre-emptive runtime for 20+ years, long before mainstream multicore CPUs even existed.

- the JVM might be an advantage or a disadvantage depending on your circumstances.

- Clojure uses a LISP syntax which would be an advantage for folks coming from the LISP world. (Hat tip to rvirding and LFE)
  - Elixir uses a Ruby syntax which might benefit those coming from a Ruby background.

- Clojure is in my opinion a wonderful language (like many LISPs), that shares quite a few things with Elixir: both are functional without being pure, both are dynamically typed but support some tooling around enforcing types, both rely on immutable data structures, both have powerful meta programming in the form of macros written in the language itself, and both are compiled into an intermediate form, making them especially powerful for long-running programs, less so for scripting.
- Apart from the differences related to the JVM versus the ERTS, that others have mentioned, I would also mention some differences in the focus and practices of the community:
  - 🧮 Elixir and Erlang are designed from the ground up to allow for concurrency through the actor model (Erlang processes). While it is completely possible to write concurrent software with Clojure (for example with channels), concurrency in the Elixir and Erlang world is a core value that permeates the design of the language and its libraries.
  - The Clojure community tends to promote small composable tools over frameworks. While Elixir also places a lot of value in small composable modules, its community also provides high quality frameworks like Phoenix and Ecto. This is totally subjective, but I personally like Elixir on this aspect.
- At the end of the day, there is virtually nothing practical that one language can do and the other cannot, and they have many similarities, but they do have slightly different “core values”.

- 📌 #1 Elixir is not a Lisp, Clojure is one
  - The parenthesis and s-expressions are actually a big part of this question, as well as the dynamism of the language compiler and the REPL driven development it brings. Those things go hand in hand, and are integral to what makes Lisp interesting.
  - In Lisps, the code is the unambiguous tree of evaluation, it is what actually gets transformed and computed, you’ve removed a layer between you and the machine. It’s the closest syntax to pure untyped lambda calculus you’ll find.
- 📌 #2 Elixir runs on the Beam VM, Clojure runs on the JVM
  - The BEAM is designed from the ground up to run distributed systems, that means that you cannot have two piece of code run concurrently or in parallel in ways where they share data. It also means that it doesn’t rely on the OS threads for concurrency and parallelization, implementing its own scheduler for concurrent code execution.
  - Elixir takes advantage of all this in turn of running on the Beam VM.
  - The downsides of this comes at the expense of performance for non-distributed applications, single thread performance of single machine multi-threaded code. There’s always going to be overhead in exchanging data instead of sharing it straight form memory.
  - Another downside, but that could change in the future, is just the investment put behind each VMs, the JVM has been funded a lot more, it has thus had a lot more optimization go into it and many companies offer long term support and all that for every version of it imaginable.
- 📌 #3 Elixir is weird, Clojure is weirder
  - Elixir is weird, it has different ways for doing things than your typical OO imperative language. You have pattern marching, modules, actors, enumerations, streams, and all other such things, there’s a lot to learn. 
  - But in Clojure, there’s even more weird stuff to learn, metadata, transducers, multimethods, drastically different ways of doing concurrency like executor services, futures, locks, stm, agents, csp, reducers, and just in general you’ll be faced with weirder things to learn.
- 📌 #4 Elixir is much closer to Erlang than Clojure is to Java
- #5 Elixir has big frameworks that have made all the hard decisions for you and don’t demand you to understand a lot to get going and build apps, while Clojure expects you to know everything
- #6 Elixir is only Elixir, Clojure is now a whole generation of dialects
  - I’m not too sure why there are so many Clojure dialects compared to Elixir, I think one reason is that Lisp heritage, it makes implementing Clojure a lot easier
  - But it could also be because Clojure has more of a self-identity in its own semantics, that Elixir would find harder to re-implement itself without all that the Beam provides. 
  - Another reason might just be Elixir is newer, or that less people need an alternative to the Beam compared to the JVM 
- #7 Elixir startup is slow, Clojure is slower but…
  - Clojure start time are even slower. Yet since GraalVM can compile Clojure code to native binaries 
- #8 I am obviously biased towards Clojure

- The technical differences are variously significant (JVM vs BEAM) or trivial (syntax), but culture & context also matters.
  - Clojure emphasises self-assembly of solution styles from orthogonal and self-chosen libraries; 
  - Elixir ergonomics and community-wide architectural styles.
  - So for a beginner (to the language/platform, not to development) Clojure’s expectation is that your scaffolding comes from your immediate team. 
  - Elixir provides that scaffolding in its standard libraries & tooling.

- (As of late 2022, OCaml is finally multithreaded.)

- ## 🆚️ [What are the main benefits of Elixir compared to Clojure? | Hacker News _202003](https://news.ycombinator.com/item?id=22658515)
- The main benefits of Clojure
  - Desktop apps
  - Server-side apps
  - Mobile apps
  - Unity games
  - Live coding music performance
  - AI apps
  - C libraries
  - Native apps

- I can use libraries with low friction from the following ecosystems:
  - JavaScript
  - Java
  - . NET
  - Python

- Runtimes include but limited to:
  - JavaScript
  - JVM
  - CLR
  - Erlang
  - SubstrateVM

- Clojure specific advantages:
  - Datomic
  - Crux
  - Datascript
  - Datahike

- Most "functional" languages bottom out into some highly mutable SQL thing and it's gross
  - Then there are the cultural things, so as you grew as a programmer you probably went imperative, OO to FP, well with Clojure you go another step: imperative, OO, FP, Data-driven

- Seems like the main takeaways from this are that concurrency on BEAM is amazing and the JVM can't match that. So it feels like it boils down to whether you like Ruby syntax versus Lisp syntax. 

- Elixir is not Ruby, it just has a somewhat Ruby-like syntax. The similarities end there. Elixir does not have the performance issues that Ruby has (although it may have different ones!)

- ## is Elixir simply syntactic sugar for AST?
- https://twitter.com/elixirfun/status/1780838300346958156
- That’s why I’m using it for sorb! It’s like a language front-end I can just apply to another use case.
- It’s quite often compared to a lisp and I’d say that’s pretty accurate. The power and expressivity with a more human readable syntax.

- ## Static typing is super critical for large projects
- https://news.ycombinator.com/item?id=38052864
- YMMV very large project have been written in Erlang/Elixir without static typing and they've been wildly successfull
  - i.e WhatsApp (based on Ejabberd), Ericsson network switches, RabbitMQ, CouchDB and a lot more
  - [Which companies are using Erlang, and why?](https://www.erlang-solutions.com/blog/which-companies-are-using-erlang-and-why-mytopdogstatus/)
