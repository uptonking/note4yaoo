---
title: lib-db-app-blog-stars
tags: [blog, database]
created: 2023-09-16T17:49:18.664Z
modified: 2023-09-16T17:49:28.532Z
---

# lib-db-app-blog-stars

# guide

# blogs

## 💡 [The Strength of the Record · XTDB Docs](https://docs.xtdb.com/concepts/strength-of-the-record/)

- There is some surface area to a database that allows us to store, query, and listen. This is our user interface. It is also our storage metaphor.
- 👉🏻 Storage metaphors come in three broad structural categories: rows in tables, documents in trees, triples in graphs. 
  - These structures, in turn, are bound to a three-dimensional field. 
  - Our X-axis is schema, from hard to soft, our Y-axis is depth, from flat to nested, and our Z-axis is shape repetition, from regular to unique. 
- Rows in a relational database table will subscribe to a hard schema, a flat depth, and a common shape. 
- Document stores will subscribe to a softer schema, a nested depth, and (potentially) unique shapes. 
- Triples do not dictate schema by their nature but they have negligible(不重要的；很小的) depth and negligible variety. The uncomplicated nature of triples is reminiscent(引起联想的, 提示的) of LISP’s absence of syntax. That makes them attractive…​ but esoteric(只有内行才懂的；难懂的).

- Tables: the hometown favourite
- A table is an intuitive concept, even to children. But we all know, just as my teacher understood, that text in an arbitrary table is effectively meaningless, text in a spreadsheet table is meaningful but unconstrained, and text in a database is constrained by datatype. 

- Documents: structs, trees, and nests
- An object isn’t a simple or intuitive concept; an object is type-matching dynamic dispatch implemented over a collection of closures which in turn share a second collection of lexically-bound variables which themselves are — you guessed it — more objects.
- Document DBs, on the other hand, were not such a bad idea. They were just poorly implemented. Standard query languages? Nope. Schemaless? Nope. Relationships? Not really. Append-only, immutable data? That gets pretty expensive when you denormalize all your records into a deeply-nested rat’s nest.
- MongoDB lacked basic joins until version 3.2 but this was an honest mistake. MongoDB engineers believed their customers could survive on schemaless, denormalized data with no relationships. We now know this isn’t true. All databases have schema. All databases have relationships. Our schema and relationships may be implicit but they are truths we must face.
- Neo4j, on the other hand, is a document database that actually works. Neo4j is a property graph and property graphs do not pretend relational data doesn’t exist — or that it exists but somehow isn’t important. Unfortunately, Neo4j has its own homebrew query language, Cypher, with its own baggage. Although an open standard since 2017, Cypher queries are difficult to compose because the language lacks a foundation in logic
- Rather than hide behind a deeply-nested document model or inglorious query languages, we can put our faith in decades of research. 

- Triples: oh, the trouble with triples
- I was excited about the possibility of Clojure-style simplicity in database form: The triple-store.
- Roughly, there are two categories of triples: **RDF triples**, which attempt to encode relationship semantics, and **EAV triples**, which only encode the relationship
  - A semantic triple might look something like `[Bob belongs_to CommunistParty]` where an EAV triple is more likely to take the shape `[Bob :party CommunistParty]`.
- Rather than debate the semantics of semantic triples, we’ll treat them as loosely equivalent for this story. Caveat lector.
- My team was immediately attracted to triples. The declarative logic of Datalog, with its Prolog origins, felt like the perfect way to ask questions of a database. Having never worked with triple-stores before, there was a purity to EAV triples none of us had ever imagined possible during our career with relational databases. An immutable store of pure facts? Count us in!
- Back in 2014 our triple-store of choice had a hard schema, not unlike the schema definitions in most relational databases. However, it went so much deeper than that. 
- In retrospect, it feels as though there must be an underlying reason RDF has never enjoyed general database success. Despite more than two decades of research and implementation, RDF remains the storage metaphor of museum artefacts and government statistics.
  - The elevation of purity above all else is a certainly one problem with triples. 
  - Their true deficiency, however, is hidden in plain sight: **triples by their very nature only describe relationships**. 
  - Despite their name, relational databases consign(移交；交付) the very notion of a "relationship" to the realm of the derivative. 
  - Triples have the opposite problem. Triples treat nouns as second-class citizens.

- Enter The Record
- relational databases fail the dictionary definition. Most lack a meaningful, first-class representation of time with which to view the past. The flip side of that coin is the absence of immutability.
- Triples fail our mental model instead. The client record card is natural. Specifying each individual fact about your client is not. If we want to see that natural record, triples force synecdoche on us.
- It is possible to find a middle path between hard, flat rows in tables and infinitely malleable(容易改变的，易受影响的) triples. Surprisingly, documents are that middle path.

- Records: doing documents right
- "Flat is better than nested" is a guideline, not a rule.
- To ensure nothing crazy will ever happen, our storage metaphor of "documents" must play by the rules. The dictionary says our database must store immutable facts on a timeline. Computer Science says our database must speak a standard query language. Our experience and intuition says our database should provide us lightweight references between our documents and discourage deep nesting.
- These are not abstruse or mystical ideas, but they do demand a reappraisal of the database. We can’t just tack immutability onto MongoDB or temporality onto Postgres. We must rebuild the foundation. We must record a graph of immutable facts on a timeline tolerant of growth and query them by time-aware logic. That’s a mouthful, so let’s just call it a Record. This is the new metaphor.  
# more
