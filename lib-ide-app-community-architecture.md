---
title: lib-ide-app-community-architecture
tags: [architecture, community, ide]
created: 2024-12-03T13:20:09.295Z
modified: 2024-12-03T13:20:30.085Z
---

# lib-ide-app-community-architecture

# guide

- 代码文件与数据库紧密结合的方案示例，可参考git
- 代码与数据库结合来更新应用的方案，可参考aquameta/couchapp/reka
# discuss-stars
- ## 

- ## 

- ## ⚖️ [Build Server Protocol](https://build-server-protocol.github.io/)
  - Protocol for IDEs and build tools to communicate about compile, run, test, debug and more.
  - The Build Server Protocol (BSP) provides endpoints for IDEs and build tools to communicate about directory layouts, external dependencies, compile, test and more.
  - The build server can notify the client about compile progress and report compile errors.
- BSP is complementary to LSP
  - While LSP allows editor clients to abstract over different programming languages, BSP allows IDE clients to abstract over different build tools.
- Example of running, testing and debugging a Scala program in VS Code via BSP and the Debug Adapter Protocol.

# discuss-ide-database 🛢️
- ## 

- ## 

- ## 

- ## 🔡 [Codebase as Database: Turning the IDE Inside Out with Datalog (2020) | Hacker News _202210](https://news.ycombinator.com/item?id=33076092)
- The biggest challenge with incrementality in the IDE (I'm not even talking about incremental parsing or whatever) is you're subject to the whims(突发奇想，异想天开；心血来潮) of a given language's build system and how it behaves on multi-million LoC codebases. With sufficient human suffering thrown at the problem, you can approximate decent incrementality, but it ain't easy.
- why isn't the compiler incremental?
  - It doesn’t need to be / it is, depending on perspective. The C# compiler, for example, has what’s called a “semantic speculative model” wherein it will use various heuristics to know when you need to re-typecheck things or not (e.g., editing just the body of a method without changing a type signature kicks off much less work than if you also change the return type). But it’s also just really fucking fast and will use as many threads as you want it to, so it can also be kinda moot too. Very rarely is the compiler actually a bottleneck in the C# case, but could be in others.

- Source-code can be stored in a database of course. But I think this is about having source-code express the data. In a sense SQL does that already with its data-definition language subset. Or maybe I misunderstood?

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

- One of my ideas is "lazy invariant maintenance". It should be possible to layer the tip of execution (what should go on next) with lazy incremental materialized invariants. Let the computer decide what is the most efficient approach to solving the computational problem. 
  - In other words everything is a query and queries are layered on top of eachother in arbitrary directions. 
  - I think storage or source of truth should be decided by the software. It might be more efficient to arrange data a certain way to sustain multiple types of queries.

- ## 🤔🔡 [Turning the IDE Inside Out with Datalog | Hacker News _202007](https://news.ycombinator.com/item?id=23869592)
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

- 💡 This is how Rust Analyzers intellisense works, it uses a query engine called Salsa that stores the symbols in a database and the linting and completion/semantics are entirely query-driven
  - Good video describing it's use for working with Rust's AST:
  - [Salsa In More Depth (2019.01) - YouTube](https://www.youtube.com/watch?v=i_IhACacPRY&t=1348s)

- Sorry to disappoint but for people doing programming language semantics there’s nothing new here. The hard part is always to go from the made-up language to a set of multiple full-blown languages.

- ## [The Database Inside Your Codebase | Hacker News _202102](https://news.ycombinator.com/item?id=26160186)
- Check out Aquameta, a web dev stack built entirely in PostgreSQL (self-plug):
  - There's a ton down this rabbit hole. One of the great anomalies(异常的事物；不合规则) of our industry is that we've used the database to bring coherence(合乎逻辑的; 协调) to countless "user domains", but never applied the same principles to our own stack. The benefits of doing so compound exponentially.
- So basically Oracle Apex, oracle html db before that, and end of the 90s we were generating this from Oracle Designer 2000: low-code tools to generate web applications from the database...

- I've been playing with some ideas for creating a SQLite database of classes, functions and suchlike found in Python code, so I can analyze my codebases with SQL queries.
  - I've had some good initial results with https://github.com/davidhalter/jedi - which is the Python introspection library that powers various editor autocomplete implementations. I have a prototype which uses that to create a SQL database of functions, classes and places that they are used.
  - I've also been playing with https://github.com/github/semantic - it can parse Python, JavaScript and other languages and offers a --json-symbols option which dumps out a JSON object showing the symbols (functions, variables etc) found in the code.

- It's really a shame the database is not at the base of what we're doing. We're inventing and re-inventing tons of file formats and ways to persist data without using the database, we have to eternally worry about race conditions in the file system and stuff, and all the while most of our concerns would be well served by an RDBMS.

- ## [Aquameta: Web development platform built in PostgreSQL | Hacker News _201910](https://news.ycombinator.com/item?id=21281042)
- I think this is an awesome idea. I really like the Smalltalk approach of not using files and instead representing the structure of a program purely in memory. I also love the idea of drawing inspiration from spreadsheets and databases instead of representing programs purely in lines of code.
  - Any long-lived executable sits in memory (notwithstanding paging, which the database server is also subject to), and such an executable is free to maintain any files it accesses in memory as well.
- I think what was being referred to is the technique of defining a program, not as source code files which are then compiled/run in an interpreter, but as an in-memory VM environment (think REPLs). The memory-based environment can then be saved to a file, similar to making a core dump.
  - This changes the structure of programs from a file/disk based structure, to the potentially richer structure of the programming environment (e.g. graphs of objects). Although it comes with disadvantages like losing the tool inter-operability of files.
- I have a hard time seeing advantages of ditching files. I like this concept, but you can have it both ways (come up with a graphical notation that you can then manipulate with graph like tools), but at the end of the day you need a source of truth, and the file metaphor (a named region of code) is hard to beat (impossible to beat?). Even databases store things as files.
- File systems are just one approach to storage. 
  - Databases can use file systems, block devices, or object-based storage (such as distributed storage systems, e.g. Ceph, Amazon S3). 
  - Traditional file systems are, by themselves, inadequate for many use case, as they don't provide things like versioning. 
  - The strength of the file system, is that much tooling already exists for it.

- I guess this isn't that dissimilar from Git, except that when you snapshot your environment, you get everything (code, IDE settings, issue tracking, and persistent data) all in the same dump.
  - if we had a way to version code that combines source, data, and issues, I'm super interested. It just needs to pipe into existing tools rather than recreating existing tools.

- Oracle have already done this, it's called Application Express[0]. I used it for my last job. In practice it was pretty good for fast prototyping and iterating on database-backed apps. It took the schema as the source of truth and would add useful interface features based on it (eg, dropdown lists derived from foreign keys, converting some check constraints to javascript validation code etc).
  - But on the downside it was essentially untestable and version control meant dumping a massive file of autogenerated PL/SQL and checking it into git. For anything more complicated than basic CRUD and reporting you'd wind up cracking the hood to directly use PL/SQL and then skin it with APEX. The tradeoff being that you lost some of the roundtrip niceties.

- Databases have been basically awful at being approachable from the command-line.
  - Let's say I have some HTML in some field in the db and want to make a change to it from the terminal. How do I do this?
  - Aquameta has a filesystem integration layer that lets you browse the database from the command line, grep database content, edit the content of a field using your preferred text editor
  - Generally just trying to ease these pain points has been a big goal of the project... still a lot to do.

- The problem with not putting business logic in an RDBMS is that you risk ending up with an application which evolves towards... implementing features already provided by the RDBMS.

- For a good overview of what power and speed you can have by "putting a web development platform entirely inside an RDBMS", check out this video called "Twitter-like App in 20 minutes with Oracle APEX"

- Is this comparable to Oracle Apex, which is a web development tool written entirely in oracle PL/SQL?
  - Used Apex when it first came out (as HTMLDB). I’ve never found anything that compared to its speed in rolling out web based forms for internal use

- reminds me of couchdb apps where you'd use document attachments to store html/public files and serve them directly from couch.

- This is actually really similar to on-premise SharePoint development; list data, content types, workflow definitions, front-end HTML, CSS, JS code are just stored in the back end database.

- Data driven applications are cool, I think I'd use Datomic over Postgres but it didn't exist 20 years ago
# discuss-ast
- ## 

- ## 

- ## [Codemod – A library to assist with large-scale codebase refactoring | Hacker News _201708](https://news.ycombinator.com/item?id=15083882)
- This code was open sourced in 2008, with a few improvements here and there until 2010.
  - Codemod is great, but there are better tools out there (pfff by facebook, IntelliJ plugins, etc). It's too bad the readme doesn't do a great job explaining that.
- https://github.com/facebookarchive/pfff /LGPL/201702/ocaml/archived
  - pfff is a set of tools and APIs to perform static analysis, code visualizations, code navigations, or style-preserving source-to-source transformations such as refactorings on source code. 

- I also like Clang Tools for C++ AST and programmatic refactoring. Much better than regex replace. What exactly is the benefit of Codemod? Too me it seems like a glorified regex replacer, nothing more.
- What I really want: a language agnostic abstract syntax tree parser, matcher and transformer.

- Facebook also maintains a JS codemod tool that React uses: https://github.com/facebook/jscodeshift

- I find the idea of https://github.com/facebook/jscodeshift to be really useful.
  - For example, I wrote a small script to change var to let or const when possible. It uses the AST to check scoping rules and to check if a variable is ever reassigned.
  - Writing scripts like this is way more effective than doing it by hand.

- Or just use a language that supports large scale refactoring, say Java, C#, perhaps even C++ if you are careful. I generally don't like dynamic languages for large projects exactly because of this. You can't safely and quickly do large scale refactorings, a point that will come back and haunt you sooner or later. No matter how good you are or how much care you take, the code will rot significantly more than in Java/C# because you just can't quickly refactor stuff across the entire codebase, so you won't.

- I'd also recommend checking out https://github.com/Yelp/undebt (/201707/python/archived) which is a bit more robust it seems in the search aspect, since it's grammar-based instead of regex-based.

- 
- 
- 
- 
- 

- ## [Where is the CRDT for syntax trees | Hacker News _202112](https://news.ycombinator.com/item?id=29433896)
  - 核心是json的crdt操作
- We are almost there, for lists and structs there are CDRT's but a move operation across the data structure is missing. Martin Kleppman (from automerge) talks about this in his talk "CRDTs: the hard parts"
  - I also think a range move or range delete is missing from many of these algorithms. Peritext

- We just got CRDTs for generic textual documents
  - code has generic textual components -- like comments -- plus tree-like elements -- so it's arguably more complex. 
  - Furthermore, one expects automatically merging conflicting content to often have to be resolved because even a merge + a sophisticated node-based merging strategy will fail to capture effectful intents. 
  - However, i am excited to see tooling where, for example competing merges get run through a trichotomy (A only, B only, A + B) to see which branch satisfies the most number of tests... And then suggests the resolution accordingly.
- In terms of generic textual documents, do you have a link? The only thing that comes to mind is Pijul: https://pijul.org/ I also found peritext

- Sounds nice in theory. But how is syntax based version control ever supposed to work when we have so many languages that literally parse differently depending on dependencies that aren't even in the codebase? Let alone ones that easily take hours to compile even when they are in the codebase? Sounds impossible in practice unless we restrict ourselves to sufficiently context free languages.

- Sounds similar to what Semantic Merge does. Of course it would also have to handle syntax errors. For that it could fall back to the current crop of text CRDTs.

- ## ✏️ [Treefrog: A code editor that uses both AST and text editing commands | Hacker News _202201](https://news.ycombinator.com/item?id=29787861)
- I started experimenting with AST editing ideas after getting frustrated with my editor's lack of understanding of the structure and meaning of code, ie. the editing primitives all dealt with text and simple changes to the code often required repetitive manual text edits that had nothing to do with the meaning of the change. 
  - I went through a couple of prototypes and landed on the idea of augmenting a standard editing interface with a new mode that works on a simplified representation of the structure, which basically follows indentation levels - blocks of code like functions, loops, etc, can be moved and manipulated as units, and there are specific editing commands for the different elements.
  - The main idea is to design all of the editing and navigation commands around the thought processes (instead of designing around a data structure, which I think is where traditional editors have gone wrong), so that it feels natural and intuitive to use - like something that's been designed for what editing code actually involves, as opposed to a text editor that's had lots of code intelligence stuff added on top of it.

- There has been a movement to try something like this under the buzzword "projectional editing". The idea was to edit a representation of the code and not the code itself. People and companies experimented with it but didn't get much adoption. Not sure why. Perhaps you need to allow the developers to reach invalid states, because the editors I tried just refused entries which would result in a syntax violation. This is harder to implement though. 
  - Yeah, that's one of the main issues with ASTs and why I think they make the same mistake as text editors ultimately - designing around a particular data structure just constrains you into weird UX scenarios that don't have anything to do with the actual problem of making something that lets you write code.
- Friend of mine said he worked with a system like that. Problem with it was it couldn't save code that didn't compile. That's a defect. Am reminded of someones comment that they would like a compiler that just stubs out code that doesn't compile. For a system to be workable you need to be able to handle that.

- I think of refactorings as being a level of abstraction above text and AST editing - kind of like macros for AST edits.

- The features I've always dreamed about from an AST aware editor was shell-like functionality where operations to rename, move, copy, create, etc were akin to file manipulations done on the command line. At one point I was thinking about the possibility of FUSE-ifying(https://en.wikipedia.org/wiki/Filesystem_in_Userspace) some code so that a normal shell could be used. Any chance of shell-like functionality from treefrog?

- ## [Flattening ASTs and other compiler data structures | Hacker News _202307](https://news.ycombinator.com/item?id=36559346)
- Blender (the 3D modelling software) is a fascinating case of this. 
  - To make loading and saving files fast and lossless, it uses identical on-disk and in-memory representations. 
  - In other words, everything is in an arena(活动场地), and saving and loading is just a memcpy of the entire arena. 
  - Considering the massive potential complexity of a Blender project and the myriad issues you could have with serialisation and deserialisation, this seems like a great design to me.
  - The trade-off of course is that your data structure design is kinda sticky, insofar as you need to be able to open files for older versions.

- The missing piece is a way to evolve those data structures over time, in a similar way to database migrations. Only when loading data from an older version of the app those operations would need to be issued, and then the app could save the updated version in disk immediately to avoid incurring that cost again.
  - An example implementation of this concept is [this project](https://www.inkandswitch.com/cambria/) that was created in the context or CRDTs. If it is not directly applicable, at least it should be a good inspiration

- You ever hear of .doc files? Yeah. There is a reason XML was seen as the future back in the 90s. 
  - Custom databases often get extended into custom filesystems. And these systems on top of systems get obscure features (like embedding excel sheets inside of Word) and... Thing get hairy.

- Wasn't that also the way Word used to dump structs onto disc in the "doc" days? I think I read that way also a major problem in writing converters, you baobab needed to decode Word's internal data structures which were of course undocumented.
  - It's very common in old software and video games. Pre-97 office did that though with more formalisation than most (the binary format is now called Binary Interchange File Format, or BIFF, and is relatively generic, at the time MS almost certainly had utility libraries for working with BIFF).
  - This was a common source of portability issues for game saves (as well as blowing your saves on updates), as they'd commonly just blit internal data structure, with no formalised interface.

- I remember Spolsky saying Excel .xls worked like this, but I guess this should apply to .doc files as well. This is usually orders of magnitude faster than serializing to/deserializing from a different storage format.
  - I don't think so. Serializing is IO-bound, if your format is "simple" (e.g. CBOR) you can't measure the difference.

- I believe Microsoft Word originally did this, and it was a major pain as the file format evolved.

- It also means you can't share files between little endians and big endians.
  - It isn't a real problem. Blender supports only little-endian targets and the code byte swaps data files as needed. I guess someone could port it to AIX, z/OS, or Linux/zSeries, but that's unlikely at best.

- Storing changes and the originals blew up badly for Microsoft Word in the late 1990's due to privacy concerns.

- I love flattened ASTs. One of my favorite uses of them is for inline markup in pulldown-cmark (see [1] for a brief description).
  - Here's a sketch of the problem being solved. The raw input is broken into a sequence of nodes, and something like * is turned into a "MaybeEmphasis" node, as it has the potential to turn into emphasis, or remain text if no match for it is found.

- This reminds me of a GDC talk where rust was praised because it forces you to either go mad because of the borrow checker or structure code using an entity component system. I find it funny that the value of the borrow checker in all these real world scenarios with complicated lifetimes is to find a way to avoid it entirely by putting stuff in arrays and reference them by their index.
  - Using an entity component system felt like writing very fancy spaghetti code in my limited experience with the Bevy game engine in Rust. No longer having direct references between objects means the type system isn't nearly as useful and I found it very hard to reason about the code. I can believe it becomes useful in very large systems but it was just a hinderance in the small program I was writing.

- This is also how Prolog terms are represented on the heap in the Warren Abstract Machine (WAM). 

- I used such a succinct(简洁的；简要的) AST structure to implement a JavaScript parser and interpreter for a severely memory constrained environment (embedded): V7 (https://github.com/cesanta/v7)
  - We later switched to a ast->bytecode compilation step but for a while the implicit AST was directly traversed during interpretation.

- I did something similarly for my Yaml to Sql compiler at https://yaml2sql.netlify.app.

- Same ideas are used in Nim's incremental compilation (wip) https://github.com/nim-lang/Nim/tree/devel/compiler/ic Also there are two JSON implementations with a flat architecture https://github.com/Araq/packedjson and https://github.com/planetis-m/packedjson2 (this one I wrote) But I agree it's a pain to write it like that.

- There was some work on having flattened JS as bytecode. It never got much adoption but I believe it would have made the web a lot more efficient.
# discuss-lint
- ## 

- ## 

- ## 

- ## Semgrep is a security scanner trusted by the biggest enterprises in the world. Now runs on every deploy for vibe coders on Replit. _202505
- https://x.com/amasad/status/1923071981299065189

# discuss-ide
- ## 

- ## 

- ## 

- ## 

- ## [Drowning in code: The ever-growing problem of ever-growing codebases | Hacker News _202402](https://news.ycombinator.com/item?id=39356574)
- Basically, "divide and conquer." Big things are composed of small things.

- I once used OpenGrok, a web based sourcecode repository viewer to tell myself I would try reading and understanding a large code base.

- 
- 
