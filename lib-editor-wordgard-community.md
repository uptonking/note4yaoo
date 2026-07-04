---
title: lib-editor-wordgard-community
tags: [community, wordgard]
created: 2026-07-03T18:33:44.038Z
modified: 2026-07-03T18:33:54.312Z
---

# lib-editor-wordgard-community

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 

- ## [Wordgard: In-browser rich-text editor from the creator of ProseMirror | Hacker News _202607](https://news.ycombinator.com/item?id=48772573)
- I always wondered why there is no code/package overlap between CodeMirror and ProseMirror (or now Wordgard). Have you tried this? 
  - There's a significant amount of code in Wordgard that is copy-pasted from CodeMirror or ProseMirror, but modified enough that trying to share it would involve nightmarish amounts of type parameters and extra indirection. You could certainly build a generic editor framework and then build several editors on top of it, but you'd end up with Raku-level amounts of architecture acrobatics and extra complexity, much of which would leak out in the public library interface, and I don't think that is generally worth it. I do occasionally, when I realize a bug fix applies to one of my other projects as well, repeat it there. But that's okay.

- I'm part of the Zoho Writer team (Google docs alternative). And the new architecture is very similar to Zoho Writer i.e edits represented as a sequence of retains/keeps followed by action.
  - Also the decision to forego browser's selection and draw a custom layer.
  - All this makes reasoning about changes a lot more saner and intuitive. I've always wondered why prosemirror's transactions & steps couldn't be simplified further so I'm one vote up for the new design direction!

- One thing i've struggled with with Prosemirror (via TipTap) is that I very often need to interact with JSON representation of the document programmatically to extract data from it, this means I need (okay, strongly prefer) a statically-typed representation of it.
Prosemirror doesn't really have any mechanism to do this, so i've ended up doing one of these two things:
1. Define the schema twice, once using Prosemirror and once using something like Zod. Then having a battery of equivalence tests to assert that the schemas match. 
2. Build a meta schema definition layer that can output a Prosemirror schema, but conforms to the standard schema spec (https://standardschema.dev/), this approach is more viable if not using something like Tiptap.
I haven't tried using Wordgard yet, so I can't tell if it does anything to address this, but just calling it out as a pain point i'd love to see solved.

- While these use contenteditable, it's not accurate to say they're just contenteditable plus some UI and interop.
  - None of these modern editors (Wordgard, ProseMirror, Lexical, Slate) use contenteditable for the document model. Rather, they have their own internal document model and use contenteditable as a kind of input layer where the editor monitors what the browser does, then translates that into actual edits.
  - Early editors like FCKEditor and TinyMCE were only wrappers around contenteditable. They used the DOM as the real document model, then intercepted certain keypresses and events and "fixed" the behavior when it wasn't correct (e.g. double enter inside a bullet list should switch to paragraph mode). The result was rife with bugs and inconsistencies, and didn't allow for a proper split between the model and the view (e.g. to represent columns, video embeds, and so on).

- I haven't entirely decided what utilities I'm going to include in the core library, but mentions are definitely on the list for potential inclusion.

- I don't like WYSIWYG on the web. You do a long and tedious formatting of a forum post, then close the tab and it's all gone. I prefer to use a local text editor then Ctrl+V into web form. Which I can with markdown
  - I've seen this solved in some platforms with localstorage, so that it automatically saves your "draft" as you type and seamlessly restores it if you re-open the page. 
- Any sites that have forms or editors that don't save your progress with localstorage need to leave the web and not come back.

- Why this over Lexical by Meta?
  - The person who got inspired by prosemirror and built lexical is no more at meta. Go to the repository and you'll find it's already in maintenance mode. Its promise of cross platform extensible editor is unrealised yet. I'd pick prosemirror any day over Lexical.
- I don't know if you ever used Draft.js that FB put out some time ago, but it was a horribly buggy monstrosity that was a heavy lift to move away from. 

- I think the issue is not the "solving", rather that people have different opinions and they want different things, and there isn't common agreement what is needed or how. Most editors work just fine for the basic needs. But well, that is my opinion.

- ## 🚀 [Wordgard Release 0.1 _202607](https://marijnhaverbeke.nl/blog/wordgard-0.1.html)
- Wordgard is a new iteration of a ProseMirror-style rich text editor system, integrating the things I've learned since stabilizing ProseMirror, nine years ago. 
- Wordgard is (once again) a JavaScript library that uses the browser DOM to display its editor interface.
- The architecture also takes a lot of inspiration from the version 6 redesign of the CodeMirror text editor.

- ProseMirror isn't going anywhere—it will continue to be maintained. But there are parts of its design that make me wince every time I have to work with them, because at this point I know that I should have done them differently.
  - Instead of trying to change ProseMirror to incorporate these new insights, I have chosen to create a completely new system with a new name. 
- You'll find a lot of ideas from ProseMirror in Wordgard, but the programming interface is built from scratch, without concern for compatibility.

- Stop Doing Steps
- ProseMirror change representation was designed by a person who was very much occupied with the problem of preserving semantic meaning for changes even if the changes were transformed, but who also didn't have a lot of experience with change formats. Steps break down changes into atomic parts that each do a single clear thing. A given editor update might involve any number of them, each defined to act on the document produced by the one before it. They serve their purpose, but they are seriously awkward to work with.
- Wordgard uses a much simpler but arguably more powerful system based on my experience with CodeMirror's change representation, which derives from the old “delta” format from ShareJS. In CodeMirror, a change is a sequence of sections, each of which either preserves a part of the old document, or replaces it with a piece of new content. So in a document of length 10, inserting an L at 4 is represented [keep 4] [replace 0 with "L"] [keep 6], and deleting the first two characters would be [replace 2 with ""] [keep 8].
- Wordgard extends this with modification sections, which preserve the structure of a section, but add or remove marks to it (which are things like emphasis, link style, or image alt text). Making the word from 3 to 6 bold would be represented as [keep 3] [update 3 +bold] [keep 4].
- unlike CodeMirror's plain text, rich text content isn't just a flat string. Because Wordgard uses a token-counting indexing system for document positions (the same system ProseMirror uses) the change format can address the document as a flat sequence of tokens (node open and close tokens, and leaf tokens), into which it splices new sequences of tokens.
  - These types of changes can easily be combined, so that a single transaction always has a single change associated with it, which is easy to inspect and reason about. They also support a limited form of operational transformation, making it possible to merge a bunch of changes that are all described in terms of the start document. That gives us an ergonomic way of describing transactions with multiple changes and makes it possible to implement collaborative editing and an undo history that supports undoing some changes but not others.
- the document is not really a flat sequence of tokens. Those tokens only make sense if they combine to form a well-formed tree. If you delete a node closing token, for example, the tokens aren't balanced anymore, and you'll have created a change that cannot be applied. 
  - This issue also comes up in the handling of operational transformations. If you reinterpret a step so that it can be applied after another step, that transformation must also preserve the property of not making the document invalid. 
  - What Wordgard's change model does is, when transforming changes, to derive a fix-up change that corrects the result of the combined steps in such a way that it produces the same fix for A-over-B that it produces for B-over-A (by being careful about what inputs the fix-generation code gets). 

- Schema Composition
- Because ProseMirror document schemas specify relations between nodes in a rather direct way, setting them up generally needs to be done by hand. Node and mark types live only within a given schema—you can share their definition object, or part of it, but there's no usable node identity between schemas.
- Wordgard takes a different approach, making it so that node and mark types are their own independent thing, which may be part of different document schemas. This makes those objects usable as typed, autocompletion-supporting handles that stand in for node or mark types, and makes it easier to compose schemas by just throwing together the elements you need.
- The definition of the node or mark specifies its default content or target types, but a schema that wants to use the element differently can change those.
- ProseMirror is plagued by the issue of schemas being so generic that it was hard to provide reusable functionality—code was either specific to a schema, or it just didn't know what any of the schema elements meant. This works much better in Wordgard.
- Another schema composition problem in ProseMirror was the way node attributes are defined. Things like text alignment or alt text were defined directly in the target node, as a node attribute, strongly tying them to that node type. This made it a chore to add something like alignment or text direction to your schema, because you'd have to add that attribute to every textblock node.
- The node types themselves don't even to know what marks are targeting them.

- Content Constraints
- The ability to specify the allowed content for a given parent node using a regular expression is ProseMirror's signature feature. 
- Wordgard no longer supports this. A node's content description can only constrain what type of children it supports, not their order.
- The biggest reason is that it is just too hard to write generic document-manipulation code for ProseMirror. If your code isn't written for a specific schema, it can assume almost nothing about what transformations are valid, and needs to check every single thing it does against the content constraints. 
- I've become convinced that hard-locking your document shape with these kinds of constraints will often be detrimental to the user experience. Documents are edited through a series of small editing actions that add up to the intended shape. If your editor won't allow users to make intermediate steps that leave the document in an odd shape, that will often frustrate them.
- Wordgard is going with a more relaxed system to encourage a less rigid approach to document shape. For cases where you really do need to specify invariants beyond what the schema rules offer, it provides an abstraction called a “correction” which is a programmatic way to fix up document shapes that you don't want to allow. They also work for things that even ProseMirror's constraints couldn't express, such as making sure tables are rectangular.

- Extension System
- The CodeMirror system, based on facets, makes extensions a much more fine-grained thing, and allows every extension value to set its own precedence category. Facets are typed extension points, and can be defined by any code, not just the library itself. So editor extensions can define their own extension points, which is useful surprisingly often.
- Wordgard pretty much copies CodeMirror's system here, including its state update and reconfiguration mechanisms.
- A configuration, in this system, is not an array of plugins, but a tree of extensions, each of which can do anything from defining an event handler to configuring the editor's attributes to adding a new piece of editor state. A given feature implementation typically consist of a group of extensions that work together to produce the desired behavior.

- Dependence on the Browser
- A lot of the issues people run into with ProseMirror are related to the way it delegates selection behavior to the browser's native implementation. This approach isn't unreasonable. Doing cursor motion properly, in bidirectional text and content styled in potentially weird ways, is hard. The idea was to let the browser do it, see what it did, and update our own model of the selection to follow that.
- Unfortunately, browsers did not do as good a job as hoped. They'll refuse to move the cursor past some kinds of content, sometimes won't draw the cursor at all, other times draw it in the wrong place, and glitch out mouse selection drag gestures if you look at them funny. 
- So Wordgard bites the bullet and does almost all pointer and keyboard-based selection itself. This involved implementing bidirectional text handling (which is useful to have for other purposes as well), forming some kind of model of the way the content is laid out, and drawing the cursor ourselves.
- The one area where this is unfortunately not possible is touch selection. You can do an okay job reimplementing that, but doing so seems to irrevocably break the native context menu, which tends to be pretty hard to do without on phone and tablet systems. So touch selection is native. Fortunately, it tends to have less strange misbehavior than keyboard selection.
- Browsers have come quite a way in consistent support for editing events (notably beforeinput) in the past 9 years. Wordgard can do without the trick that ProseMirror is built on, where it monitors the document DOM for changes and parses changed content to construct an actual document change. Wordgard just handles beforeinput events for everything except composition text input. That avoids the need for a whole class of messy workarounds.

- Wordgard is a bit further along than my previous projects were at the time they were announced—its core interface supports almost everything I want it to support, and I've written a bunch of extensions to confirm that my design is practical. 
- Even though this isn't the first editor I've built, I'm sure further insights will require me to rethink parts of the public interface. I'm releasing this first version as 0.1 and will stay on 0.x versions for a while (likely at least a year) to gather feedback, fix bugs, and help me clear up the rough corners of the system.

- No language models were used in the creation of this software. I design and build my systems by hand.
- I'm doing an experiment where I don't take pull requests for Wordgard. I've realized that I find those the worst part of maintenance work. Reviewing a big change and negotiating all the adjustments needed to make it fit my expectations is generally more work than implementing the change myself. 
# discuss-internals
- ## 

- ## 

- ## 

- ## 

- ## 
# discuss-tips
- ## 

- ## 

- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## 

- ## 

- ## 
