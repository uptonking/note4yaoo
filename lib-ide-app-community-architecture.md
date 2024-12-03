---
title: lib-ide-app-community-architecture
tags: [architecture, community, ide]
created: 2024-12-03T13:20:09.295Z
modified: 2024-12-03T13:20:30.085Z
---

# lib-ide-app-community-architecture

# guide

# discuss-stars
- ## 

- ## 

- ## 
# discuss-ide-database 🛢️
- ## 

- ## 

- ## 🔡 [Codebase as Database: Turning the IDE Inside Out with Datalog (2020) | Hacker News _202210](https://news.ycombinator.com/item?id=33076092)
- The biggest challenge with incrementality in the IDE (I'm not even talking about incremental parsing or whatever) is you're subject to the whims(突发奇想，异想天开；心血来潮) of a given language's build system and how it behaves on multi-million LoC codebases. With sufficient human suffering thrown at the problem, you can approximate decent incrementality, but it ain't easy.
- why isn't the compiler incremental?
  - It doesn’t need to be / it is, depending on perspective. The C# compiler, for example, has what’s called a “semantic speculative model” wherein it will use various heuristics to know when you need to re-typecheck things or not (e.g., editing just the body of a method without changing a type signature kicks off much less work than if you also change the return type). But it’s also just really fucking fast and will use as many threads as you want it to, so it can also be kinda moot too. Very rarely is the compiler actually a bottleneck in the C# case, but could be in others.

- This is a well composed idea. This reminds me slightly of (Rich's?) Codeq https://github.com/Datomic/codeq although codeq is only outlining code/scm relationships and not syntax trees etc. I think I was always hoping codeq would add something like this (for doing what you are doing to validate forms) but the input mechanism probably needed more hammock time

- 💡 It's not a new approach but actually a very old one. 
  - The author mentions Intellij but fails to note the history of Eclipse which, via IBM's Visual Age, you can actually trace back all the way to Smalltalk, which arguably had one of the first modern IDEs three decades ago.
  - Smalltalk programs were stored in a database. There were no .sm source files on disk anywhere. It had a refactoring browser, which was a tool that allowed you to restructure the code. This came straight out of the first research papers on refactoring. It came with a class hierarchy browser as well. It was pretty amazing for the time. Smalltalk was very clever about exposing its internals to developers. Refactoring, introspection, reflection etc. were all things that it supported out of the box. And meta programming, which is something that came out of the Lisp community, was also supported of course.
  - Visual Age was basically built around IBM's tooling for Java, which included an incremental compiler they built. A lot of the people involved with that had a Smalltalk background (it actually also was a Smalltalk IDE). It stored code in a database. Later, they created Eclipse which dropped the database but kept a lot of the compiler internals that allowed it to be way faster at refactoring and working with Java code than Intellij ever was
  - Eclipse would be able to compile and be ready to run your code in between key presses. We're talking milliseconds here. In Intellij it's never less than 4-5 seconds and usually a lot more. Even on an M1. I have one. It helps. Faster is better. But it's still slow. It's just architected wrong to be that fast. It would need to internalize the compiler for it to be that fast and it just never did that. It relies on external build tools running via forked processes. It mitigates with a lot of (flaky) caching. That's why it has a top level menu option labeled "Invalidate Caches". Because cache coherence is a hard problem and they have plenty of bugs related to that.
  - So, it's an old idea and a very good idea. The ultimate version of this idea would be intentional programming (https://en.wikipedia.org/wiki/Intentional_programming) where the core idea is that programming is manipulating abstract syntax trees and that text is a mere serialization of that syntax tree. With intentional programming, you use tools (including editors) that do things with that syntax tree. Sadly, Simonyi, the person who came up with this never really got any traction with the company he founded out of Microsoft for this.
  - 💡 However, modern compiler design is finally starting to acknowledge that there is value in being IDE friendly. A compiler necessarily has to do a lot of the same things an IDE does but with very different requirements. Simply running a compiler from and IDE is slow and leads to a lot of repeated work. A much better approach is a compiler that exposes its internals to the IDE directly and runs incrementally. Like IBM did with Java in the late nineties. The Rust community has also been working on this lately and it's a topic that you see discussed in the context of other compilers. And with VS Code gaining popularity, a lot of languages are now supported through language servers that expose (some) basic refactoring functionality and other things. Mostly this is limited by the underlying tools; i.e. compilers and interpreters. It's nowhere near what Intellij does but it's better than nothing. And it's creating some stimulus for compiler makers to do better.
  - Jetbrains took their sweet time figuring that out (given they make IDEs and a major language) but their upcoming version of the Kotlin compiler frontend takes some steps in that direction as well. Java is slow in intellij. Kotlin is slower. Because the compiler is doing a lot of work and it can easily take something like half a minute to compile our code base; 

- In traditional Smalltalks, all the method objects have a shared object representing the file that method source is stored in (either .sources or .changes, with room for more) and an offset in the method to point to the text. On compilation, all it does is write the new method with metadata to the end of the .changes file, then set the text indexes. There is a mechanism to crunch out all the unused source text and generate a new merged .sources file. If you are all working on the same base version, .sources files can be shared since they are usually read only.

- Source-code can be stored in a database of course. But I think this is about having source-code express the data. In a sense SQL does that already with its data-definition language subset. Or maybe I misunderstood?

- ## 🤔🔡 [Turning the IDE Inside Out with Datalog | Hacker News _202207](https://news.ycombinator.com/item?id=23869592)
- This is really nice. Key points:
  - Parse the program like an IDE would, but expose the data in an open queryable database format (both line and unlike a language server).
  - Use Datalog for storing the facts and inferring new facts about data.

- Jetbrain IDEs (e.g. IntelliJ) have structural search which is basically a query language for code

- In the Rust ecosystem, I believe the next-generation IDE support is already beginning to incorporate some ideas like this, although I believe it uses Prolog rather than Datalog (I'd be interested to learn more about how they differ). The logic library is called Chalk ( https://github.com/rust-lang/chalk ), and it's designed to be a full trait resolution engine for Rust (trait resolution being a necessary step to e.g. autocomplete methods on types); rust-analyzer has been using it for quite a while now, and it's slowly being incorporated into rustc itself. Not as impressive as basing the entire IDE on queries, of course!
  - The Rust project is also using the differential-datalog library mentioned in the OP to underlie their third-generation borrow checker: https://github.com/rust-lang/polonius
- Datalog is the positive, function-free fragment of Prolog, i.e., what Prolog offers over Datalog is negation and “value invention” through function terms. One consequence of that is that deciding whether a Prolog program entails a fact is undecidable (i.e., Prolog is Turing-complete), deciding whether a Datalog program entails a fact is can be done in polynomial time with respect to the size of the database.

- For prior work on IDE as database check "Energize/Cadillac & Lucid's Demise", https://www.dreamsongs.com/Cadillac.html

- Agreed on the Prolog/Datalog approach of expressing a query as a collection of facts. CodeQL does the same. From one datastore nerd to another, I actually think this is a relatively unexplored area of querying knowledge graphs (code being a very complex, dense knowledge graph.)

- There’s a lot of research on this area. The fact that Semmle was acquired by Github/Microsoft is a testament to the maturity of the field.

- This is a similar idea to that of SemanticDB, which is used in the Scala community
  - It is a queryable database of semantic information about the program which is generated by the compiler (compiler plugin, to be precise). Once generated, other tools which need semantic information, like linters or language servers, can consume it without having to worry about how to actually generate it.

- Kythe by Google is also a similar thing: https://kythe.io/

- I would have expected a mention of Roslyn which powers Visual Studio (Not code). Sort of similar to the IntelliJ approach but it is also what drives the C# compiler, it maintains the code model (actually 2 of them, syntactic and semantic) which makes it pretty powerful. It is multi language (VB, C# and I think F# now too?) but it’s perhaps not as universal as the Language Server Approach

- Reminds me a little of "Intentional Programming" or Structured Editors.

- This idea of turning a program into a database and using prolog/dalalog on it is not new. The most successful example is Semmle (bought by Github), which has been doing it for years now, with a SQL-like syntax for requests (named ". QL").

- This is how Rust Analyzers intellisense works, it uses a query engine called Salsa that stores the symbols in a database and the linting and completion/semantics are entirely query-driven
  - Good video describing it's use for working with Rust's AST:
  - [Salsa In More Depth (2019.01) - YouTube](https://www.youtube.com/watch?v=i_IhACacPRY&t=1348s)

- Sorry to disappoint but for people doing programming language semantics there’s nothing new here. The hard part is always to go from the made-up language to a set of multiple full-blown languages.
# discuss-ide
- ## 

- ## 

- ## 
