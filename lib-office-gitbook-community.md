---
title: lib-office-gitbook-community
tags: [community, ebook, gitbook]
created: 2023-09-19T06:34:17.919Z
modified: 2023-09-19T06:35:28.278Z
---

# lib-office-gitbook-community

# guide

# discuss-stars
- ## 

- ## Why #OpenDoc failed, and then failed 3 more times?_202105
- https://twitter.com/warianoguerra/status/1391757734236889088
  - [Why OpenDoc failed, and then failed 3 more times?_202105](https://instadeq.com/blog/posts/why-opendoc-failed-and-then-failed-3-more-times/)
- Summary of reasons found around the web and comparing them with other implementations of the same concept: 
  * ActiveX
  * KParts
  * Bonobo

- ## [Google Docs will now use canvas based rendering | Hacker News](https://news.ycombinator.com/item?id=27129858&p=2)
- "Displaying documents" and "displaying editable documents" are two completely different beasts. The web browser has never dealt well with displaying editable documents, the closest standard that exists is contentEditable and pretty much everyone agrees that it sucks and is not fit for complex use cases.
- It's about producing PDF vs producing HTML. 
  - Google Docs produces printable documents not hypertext. 
  - Print was never a priority of HTML. And I guess it shouldn't be either. 
  - Just look at the complexities of DocBook, LaTeX or Open Office XML.

- ## [Laying Out a Print Book with CSS | Hacker News_202303](https://news.ycombinator.com/item?id=35242299)
- 
- 
- 
- 

# discuss-alternatives-gitbook
- ## 

- ## 有没有什么像gitbook一样的文档托管平台，gitbook就是不太好看，而且编辑文档慢，页面打开速度慢，想换一下
- https://x.com/tvytlx/status/1799099262875427148
- 喜欢 md 可以考虑 vitepress
  - SaaS 服务最好是，它这个不用写代码也不用自己部署
- 推荐 nuxt content 模板 + https://nuxt.studio 

- ## [ReStructuredText vs. Markdown for documentation | Hacker News_201606](https://news.ycombinator.com/item?id=11922485)
- I prefer Markdown. It's readable and easy to start writing by non-technical folk.

- For me, Asciidoc hits the sweet spot as it seems to have much of the simplicity of Markdown, and with the AsciiDoctor/DocBook toolchain it has the publishing power of RestructuredText.
  - Asciidoc was created to simplify DocBook, so Asciidoc has the same expressive power with no downsides (as far as I know).

- Let authors use the fucking tools they know and prefer.
- Organise common text through translation tools. Pandoc is fucking amazing.

- ## [Compare AsciiDoc and Markdown | Hacker News_202107](https://news.ycombinator.com/item?id=27744509)
- I use asciidoc because it provides callouts, sidebars, captions, figures, cross references, LaTeX (via hard-to-use plugins), themes, fonts, etc. when converting to pdf or epub, etc.

- I reckon reStructuredText is the best syntactic and semantic foundation of all the ones I’ve seen, but there are a few things it could do with changing. Most significantly, reStructuredText is designed for being written in a sane text editor, where indenting stuff is easy; but this doesn’t work well for use in a plain `<textarea>` as web applications of it will commonly go for, where any indentation must be applied manually by the writer. So I’d say it’d be good to get a new syntax construct for fenced, rather than indented, directives.
  - As it stands, reStructuredText is based around having visually-pretty source: monospacedly-aligned tables, indentation for hierarchy, that sort of thing. (Headings feel like the only major thing that doesn’t use very significant whitespace.) I almost always like this, but there are definitely some situations when it’d be nice not to work that way.
- rST doesn't support nesting markup (bold and italic? nope. code styling in a link? nope.). It's decent for writing software docs, but not good at all (in my opinion) for writing blog posts or other prose.
  - Yeah, nesting inline markup is definitely something I’d want to add. Note that code styling in a link is actually possible, just convoluted

- 
- 
- 
- 
- 
- 

- ## [I wish Asciidoc was more popular | Hacker News_202302](https://news.ycombinator.com/item?id=34680558)
- AsciiDoc was written primarily as a way to write DocBook without having to use XML. 
  - AsciiDoctor has an alternative goal of writing HTML without having to use HTML. 
  - The subtle differences between these goals leads to a lot of "gotchas" if you try to serve both of them at the same time.

- One of the most powerful features of Asciidoc is the attributes and blocks system. 
  - Asciidoc documents are structured in blocks, which are arbitrary length collections of lines. 
  - Lines can be text, attributes, directives, or formatting instructions.
- One of the most powerful features of Markdown is that it's just text, and you don't need to learn some deep programmer lore in order to use it. 
  - Those extra features do come at a cost, such as being to tied to a single Ruby implementation and not having been ported to countless other languages because a Markdown parser is so much easier to write. 
  - And Crafting Interpreters was written in Markdown, you wouldn't think it because it's so beautifully formatted. 
  - Markdown is enough, simplicity wins.

- Very briefly on admonitions(警告): there is nothing stopping you from adding them to markdown yourself
  - This is both the power and "problem" with Markdown. 
  - The "promise" (I'd say) of Asciidoc in general versus Markdown is that it aims to truly be a standard.
  - Markdown itself comes (not even implicitly, but explicitly!) with the philosophy that there is no "true" standard. It's very flexible, very customizable, and does not aim for interop between implementations, for tooling, and so on.
  - Asciidoc tries to focus on being a Standard with a capital "S" so that the entire ecosystem around it can interop properly without implementation specific quirks/incompatibilities.
  - Both are good tools but with completely different philosophies. I learned all of this because I wanted to make a fast markdown parser in WASM directly. And at the same time I wanted to have a common way to put together a book to be published. What I learned quickly when trying to come at Markdown from a technical perspective is that there are dozens or more Markdown flavors and the idea of "Markdown" as a "general thing" isn't accurate, there's not even really a "core" shared between the variants/flavors. Which is in stark contrast to Asciidoc.
  - edit: A small aside, I also learned that a few publishers that focus on tech writing specifically use Asciidoc for their "publishing" workflows. So in that realm Asciidoc is practically useful to know.

- With Asciidoctor, we produce decent-looking PDF documentation as well as HTML.
- Your PDF options in Asciidoc boil out to this:
  - Asciidoctor-pdf:: this is the Ruby prawn-based thing, it's the current official path, but SVG and images can choke it. Complex customization means extensions, and that has its own overhead.
  - FOPUB aka docbook-xsl:: this is built in to the AsciidocFX dedicated editor, and uses the DocBook-XSL pipeline. Yeah, I know, it's XSL, but since DocBook has such a long tail there's a huge amount of customization that's possible, along with some docbook-only features like better indices, list of figures, etc. It's also very capable of chewing through thousand page books if it's in its own environment. But again, XSL.
  - asciidoctor-web-pdf:: this is the semi-experimental web based PDF tool, based on Paged.js, that uses the CMM Paged Media Module Level 3 (CMM PMM L3). I think this is built in to Antora now. This has the best promise, in my opinion
  - After these you have DBLATEX, which uses DocBook->LaTeX as its typesetting, and you have the Haskell thing, and the wiki-2-PDF converter that's default in Visual Studio Code Asciidoctor extension. 

- We adopted Asciidoc at work (migrated from Word and Markdown), and it has been a stellar tool for editing and reviewing our technical documentation, as it fits well into our code review process. We also use Mermaid and PlantUML for our diagrams, which the asciidoctor extension has handled well.

- It’s an endless balancing act between easy to write (code-like) and easy to read (text-like).
  - Features like table is the ultimate conundrum - if you want beautiful text based tables like in reStructuredText it becomes very difficult to write and edit unless you use a specialized editor, while Asciidoc’s table syntax is very code-like and is completely unreadable as a tabular table (almost like a simplified HTML markup).
  - Markdown strikes a middle ground where it tries to be readable while being as easy to write by hand as possible. However in practice most people don’t bother to keep the columns aligned by hand so it still becomes quite unreadable, and you still need specialized editor to do align columns automatically if you want to retain readability.

- 
- 
- 
- 
- 
- 
- 
- 

- ## [Asciidoctor | Hacker News_202010](https://news.ycombinator.com/item?id=24849348)

- AsciiDoc was implemented in Python. AIUI, the project got neglected or abandoned, so someone re-implemented it in Ruby to create AsciiDoctor -- same markup, different rendering engine.

- IMO AsciiDoc's advantage over Markdown, RST, LaTeX and others is its adoption of DocBook XML as an industrial-strength backing format. 
  - The combination of a pragmatic markup language and a proven, stable, and relatively media-independent translation target is unique and extremely useful.

- The **advantage** of ADoc is that its model maps onto that of DocBook, so it's possible to render ADoc into DocBook and then use it with established DocBook toolchains.
  - I mostly work in DocBook, but I don't like it much. I personally find raw XML horribly wordy and it took me a long time -- at least months -- to learn to read it or write it fairly easily and fluidly.
  - ADoc you can learn in an afternoon and the source remains perfectly naked-eye readable.
- The arguable **weakness** is that because DocBook is a tightly-specified format, you can formally validate a DocBook document. You know it will work and render to something, even if what comes out isn't quite what you wanted.

- I love adoc, but I really dislike the build tools (maybe because I don't work with Ruby). My feeling is that part of the reason adoc is missing or a real PITA to configure for thrid-party software (e.g.: pandoc or hugo) is largely due to this. 
  - Furthermore, I don't love the way math typesetting looks when you export to PDF (although, I guess I should just use XeTeX/LaTeX at that point).

- I've now written a book using asciidoc and I am not a fan. It's full of oddities and minilanguages and special cases. For the main body of the work it was no quicker or easier than Markdown. For anything complex I wound up spending hours poring over the docs, stackoverflow, ancient forum posts, github issues trying to learn the magic incantations.
  - I would have greatly preferred LaTeX or DocBook, but the offered alternatives were Word or Google Docs.

- ## [MdBook – A command line tool to create books with Markdown | Hacker News_202306](https://news.ycombinator.com/item?id=36528984)
- The usage of Highlight.js + MathJax on the front-end is horribly wasteful. 
  - Why? It demands all clients parse & render the syntax/LaTeX which is not only taxing on CPUs and batteries, but this action is idempotent meaning every user agent on every page visit is going to do the same wasteful parsing to get the same result. 
  - There is no good reason that syntax highlighting shouldn’t be done at build time, nor should it require JavaScript.
- Maybe it’s because MathJax loading slow would delay rendering, and using a CDN-hosted MathJax increases the chance the content is cached? That’s usually why people use CDNs. It’s more important for MathJax than, say, interactive scripts, since it can cause rendering. I don’t think MathJax loads any additional files (I don’t remember seeing any additional network requests).

- MDX is not coupled to React. You can also use it with Preact, Vue, Emotion, Theme UI, etc. Both the classic and automatic JSX runtimes are supported.
  - A sibling comment already mentions a Svelte implementation [1]. So I fail to see how this doesn't open a pandora's box of yet more flavors, this time coupled to frontend frameworks. First in .mdx and then incompatible with .md

- JSX is evidence that new generation of programmers are not taught engineering. There are very valid reasons why we went for encapsulation and **separation of concerns**. JSX throws the baby with the bath water and goes back to PHP5 sites with markup and code interspersed. 
  - Even authors of JSX cannot make it work reliably in their flagship product. MDX couples JSX with markdown.
  - I cannot see how this yields maintainable source. 
  - Sure, spaghetti code is nice for quick, one off scripts, but if you'd volunteer for helpdesk shift to be yelled at rather than fix a bug in 5k SLOC collection of Windows Batch scripts, then maybe you should reconsider mdx.

- Markdown is a really poor storage format. There is quasi-official standard (CommonMark), but since it's feature-poor, people mostly use something else, like GitHub Markdown. Individual apps often extend Markdown in various incompatible ways.
  - There are better alternatives (e.g. AsciiDoc, but it's specialized towards documentation), but they don't have anything close to the momentum of Markdown.

- Markdown is a late comer to the game, so the better question is - why should books be in Markdown? 
  - Markdown's biggest (or the only?) advantage compared to binary/XML based formats is sort-of readability in plain text, but that's just not that important for the majority of publishers and readers.

- The point becomes moot(有讨论余地的; 悬而未决的) when your book contains images/illustrations and you (like a normal reader) want to view them within the content. You will use some Markdown formatter/viewer which is again based on browser.
  - Markdown is just insufficient for any non-trivial document. 
  - There isn't any standard way to set image size for example. 
  - There's no standard way to create even rudimentary(基本的, 初步的) tables.

- Something like reStructuredText (.rst) is a similar alternative, but I think that if you're irritated by the limits of Markdown then rST isn't going to be any better. If you really want good formatting options, then LaTeX is the best I can think of at the moment.

- ## 🚀 [mdBook – A utility to create modern online books from Markdown files | Hacker News_202004](https://news.ycombinator.com/item?id=22854272)
- One of the things I love about it is that the toolchain for building and using it is just the Rust standard toolchain, which means no crazy dependency hell to manage. 
  - By comparison I’ve found Jekyll to be a long-term annoyance to keep up-to-date, I’m probably using it wrong. I know.

- I recently switched from Markdown to AsciiDoc.
  - it's more structured, much more fully featured, just two big implementations (AsciiDoc and AsciiDoctor) which are largely compatible. There's only one way to mark the language of a code block, only one way to make lists, only one way to make footnotes, etc. Also it actually has first-class support for things like footnotes and admonitions etc
  - It is a syntactic sugar layer on the **DocBook** XML format which is apparently used to make actual books. But **AsciiDoctor compiles it to everything from DocBook XML to HTML to Markdown to ePub to PDF**.
  - Another thing I like is that AsciiDoctor actually comes with a good default stylesheet. AsciiDoctor has a good default theme as well as a number of other themes available, and by default will embed the CSS into the HTML so you just have one file to distribute. It even shows anchor links to the headings when you hover over them.

- ## [Madoko – Write full-blown academic articles in Markdown | Hacker News_201509](https://news.ycombinator.com/item?id=10165395)

- https://github.com/koka-lang/madoko /js/inactive
  - a fast markdown processor for high quality academic and technical articles written in Koka

- Scholarlymarkdown is nice and I like the way you can add captions and references to equations and images
  - https://github.com/timtylin/scholdoc /haskell/pandoc/inactive
  - http://scholarlymarkdown.com/

- ## [GitBook: A modern publishing toolchain | Hacker News_201503](https://news.ycombinator.com/item?id=9209041)
- My best bits:
  - Most of the product is open-source, which means I can tinker with their publishing platform.
  - Version control
  - Markdown support
  - Mailing lists for readers (so you can send email updates)
  - Support for donations and selling (I'm not using it, though)
  - A traffic email sent every week
  - Builds are pretty fast
  - They even offer an educational discount on the pro plans if you ask nicely.
- A few issues I've faced:
  - The traffic stats are not realistic. It counts page loads, which are down by a factor of 2-3 as per my google analytics
  - Landing page customization. They do have a few options, but I'd like more options

- 
- 

# discuss-format
- ## 

- ## A dilemma posed by Humane Interface: might OpenDoc/OLE style compound documents ironically exacerbate the problems with apps?
- https://twitter.com/geoffreylitt/status/1470759473371226114
  - As with apps, each component  defines its own world. But unlike apps, you don’t even know when you’re switching worlds! “Modality with a vengeance”

- ## 🪶📄⚖️ [What if OpenDocument used SQLite? (2014) | Hacker News_202309](https://news.ycombinator.com/item?id=37553574)

- OpenDocument - Initial release: 1 May 2005; 18 years ago
  - SQLite - Initial release: 17 August 2000; 23 years ago
  - OpenDocument traces it's ancestry to OpenOffice XML format, which traces it's ancestry to StarOffice, which was xmlized around the time Sun bought it in 1999
  - Not to be confused with Office Open XML (OOXML), Microsoft's "standard".

- ⚖️ Is SQLite’s disk format an open, versioned standard? Or is it just “however SQLite saves data to disk”?
  - [Database File Format](https://www.sqlite.org/fileformat2.html)
  - Note that there have been no breaking changes since the file format was designed in 2004. 

- The **problem with SQLite** is that it's not a standardized file format. 
  - It's well-documented and pretty well understood for sure, but there's no ISO standard defining how to interpret an SQLite file in excruciating detail. 
  - Same goes for competing implementations, Zip and XML have a much smaller API surface than SQLite, whose API, apart from a bunch of C functions, is the SQL language itself. 
  - Writing an XML parser is not a trivial task, but it's still simpler than writing an SQL parser, query optimizer, compiler, bytecode VM, full-text search engine, and whatever else Sqlite offers, without any data corruption in the process. 
  - If Open Office used SQLite, its programmers would inevitably start using its more esoteric features and writing queries that a less-capable engine wouldn't be able to optimize too well.

- ## 💡 [XML is almost always misused | Hacker News](https://news.ycombinator.com/item?id=21391322)
- I mean, in theory, you could do this in JSON or some other data structure. But you would go insane and be shooting yourself in the head before long.
- See https://developers.google.com/docs/api/samples/output-json for what Google Docs does - basically **separating markup from the text by using indices**.
  - which is probably the only way to properly deal with markup and especially commented sections that can span over paragraph start/ends - neither JSON or XML seems to have a proper answer for such annotations and I wonder if there's any standard format that can that, especially if humans still want to reasonable be able to view or edit it
- **OOXML and its binary equivalents more or less solve this by completely separating paragraph and character formatting, both separately indexing the spans of text they annotate**
- That is what essentially every WYSIWYG text processor does. And also the reason why getting sane HTML out of text processor is somewhat non-trivial, as the **separately indexed spans can very well overlap, contradict each other or contain completely unnecessary formatting information**.

- I've been getting along fine using JSON for pretty much everything. 
  - That being said XML has some very sophisticated features like rigorous schema definition, a query language, a formal include syntax, comments (that's a big one), it's a lot easier to do multi-line content and in fact you can mix normal text and structured data. The include syntax doesn't get enough love. It's crazy that JSON doesn't support it.

- ## [The cost of ODF and OOXML | Hacker News](https://news.ycombinator.com/item?id=4032429)
- TeX doesn't allow separation between markup and presentation very well. 
  - Something like DocBook with a presentation engine like XSLT might be better, if it wasn't for the verbosity of the XML source.

- ## [AsciiDoc Language Submitted to Eclipse Foundation | Hacker News_202007](https://news.ycombinator.com/item?id=23711607)
- Most publishers tend to work with more industrial formats like Docbook or DITA, plus there are nice WYSIWYG editors for them.
  - Asciidoc is meant to be semantically and syntactically equivalent (and thus, losslessly round-tripable) to DocBook.
- The origins of AsciiDoc is informative. AsciiDoc is a lightweight successor to the XML DocBook format used originally to write O'Reilly computer books/manuals. Both DocBook and ePub XML add semantic elements required to describe book structure.

- ## [Sile: A Modern Rewrite of TeX | Hacker News_202211](https://news.ycombinator.com/item?id=33449323)
- TeX is one of those bits of software that's so complex to replace, it'll take another few decades (and likely a few false starts) before we can get there.
  - The fundamentals of TeX's typesetting are amazing, but everything else is just bolted on. You'd probably want to rebuild it with its own, custom language, perhaps inspired more by modern XML/markdown rather than the old TeX language.
  - The biggest problem that we're going to have moving past TeX is that it's something of a standard for math representation in text. MathML never _really_ took off. Re-training millions of people skilled in typesetting math is going to be _tough_
- TeX itself is not really complex. The implementation is fine. The hard part is the ecosystem.

- ## [Write plain text files | Hacker News_202203](https://news.ycombinator.com/item?id=30521545)

- [Write plain text files_202203](https://sive.rs/plaintext)
- I write almost everything important in my life: thoughts, plans, notes, diaries, correspondence, code, articles, and entire books.
  - I refer to them often. I search them, update them, and learn from them. 
  - I convert them into HTML to make websites, or LaTeX to make books.
- why I only use plain text files. 
  - They are the most reliable, flexible, and long-lasting option.
- PORTABLE
- free/UN-COMMERCIAL
- OFFLINE
- NO DEPENDENCIES
- EASIEST TO CONVERT
- NEED HIERARCHY?
- NEED VISUALS OR GRAPHICS?
- CONCLUSION
  - Reliable, flexible, portable, independent, and long-lasting.
  - I especially enjoy the tranquility of their offline, non-commercial nature. They’re quiet. They’re focused. (As I aim to be.)

- Another advantage to plain text files: source control. You can check your writing into git and get a history of all your edits.
  - It’s something programmers take for granted, but it would be amazing if this got more widely adopted outside of tech.
  - “Git for everything“ would be a multi-billion dollar startup easily.
- In addition to plaintext documents, I have found that a simple JSON diff is also a very effective way to demonstrate changes between 2 complex biz objects. 
  - Non-developers can cope with this as long as the differences are visually obvious (red=removed, green=new, etc) and the object graph is reasonably flat. 
  - Everything can be trivially serialized to a JSON document, so this scales super well in my experience. 
  - We use a port of Google's DiffMatchPatch to generate human-friendly HTML reports of object diffs in our latest administration tools.

- 👉🏻 **docx and epub are `zip` files, you can rename them `.docx/.epub` with a `.zip` at the end and open to see what is inside**. 
  - It might not be as simple to zip them back, at least for epub is very important to zip the files in a certain order but I forgot the details, but is easy to do from command line.
- Or use Vim; it has built in support for zip files, so you can just type something like vim my_file.docx and it will open the files in netrw (the built in file explorer). Move to the file you want and hit enter. "word/document.xml" has the main document contents in it.
  - The xml will probably need to be run through a formatter to be readable. You can type :%!xmllint --format - if you have xmllint installed.
- Docx (and pptx, and xlsx) is a zipped (not gzipped) composite of several XML files plus any other attached resources. It extracts out to a whole folder structure.
  - Definitely binary once compressed, though, and even when extracted not an easy format to parse. It might be XML, but it’s still representing the full complexity of an MS Office document.

- Git stores a new file anyways. It’s only for packs, that delta compression is applied. And **git delta compression handles binary files**.

- I once thought git for humans would be a great idea but never got around to speccing it out(给... 定规格; 按照规定标准建造). 
  - Later on, a lawyer friend showed me the software they used 'for backup' (that they paid thousands per month for) and it turned out everything about it was just exactly like SVN. 
  - The terminology was different, the UX was laser focused to the intended users, but at the end of the day **it was commits, syncs, merging, pretty much everything but branches**, just laid out with domain specific language instead, professional office UI and simple UX.

- I had a similar thought some time ago and concluded it's an impossible task. The problem is that it would need to understand every file format its users care about and be able to represent changes in a useful way. How do you merge destructive edits to image files?
  - git-lfs with appropriate file types set to use it.

- Many version control systems aimed more toward digital assets do some sort of locking, so only one user edits a file at a time. Advisory or mandatory, with support for breaking locks, etc.

- A modern MS Word document is pretty much zipped XML and mostly ISO standard-compliant.

- I was actually surprised: last time I used Git Bash on Windows it did work quite well with .docx files. Then I switched jobs to avoid touching .docx files...
  - **The best alternative I've found to generate .docx output is R markdown**, which uses pandoc under the hood and let's you program the whole document the way LaTeX would.
- I do the same with markdown in Zettlr using R-markdown, which has a nice inline-preview format and can be used by my non-tech partners. The generated .docx has a limited range of styles, but we see that as an advantage.

- This is one of the main strengths of Obsidian, which I have been using lately and I’m extremely happy with: everything is just Markdown files in some folder on disk. Zero danger of lock in.
  - You can have a disk hierarchy if you desire, or trust that search will find you what you are looking for. For me search works fairly well and if I need something extra I can just grep/sed/awk.
  - This also works well for small organizations. Both GitHub and GitLab are able to render

- Plain text adoption often implies markdown for a richer experience, but we also have the wonderful https://orgmode.org markup.
- I've been intensively using Orgmode for a year and a half (wrote my thesis in it) and then abandoned it to switch to Markdown. 
  - Orgmode quickly turns into not-quite-plaintext with humanly impossible to read and very distracting data structs stuck inside the text. I think these were called "Properties"? 
  - For me the beauty of plain-text is that it can be read and written in any Editor without needing syntax highlighting. 
  - Here Orgmode fails for me, as I found it unreadable and unusable without an Emacs-esque toolkit.

- The faithful are still on Roam. Others have moved to:
  1. Obsidian: has bidirectional linking and knowledge graphs, is faster and better supported, but doesn't have the outlining structure that Roam is based on.
  2. Logseq: basically an open source Roam with 90-95% feature parity and some cool stuff that is its own.
  3. Foam/Dendron/Athens etc: Roam clones.
  4. Notion/Evernote/something else entirely.

- ## [Get Your Book, Make It Free | Hacker News_201905](https://news.ycombinator.com/item?id=19938768)
- EPUB's can dynamically reflow the text and resize the font to be readable on your phone, your Kindle, your PC, etc. And they're far easier to cleanly convert to other formats (even PDF, if that's your only option) 
- If the book is pure text (like fiction), then sure.
  - But non-fiction often includes plenty of illustrations, sidebars, images, footnotes, and so on, which while EPUB can handle in theory, often wind up with all sorts of bugs in reality, things being out of order or not making sense or being clipped instead of resized when converting to PDF, etc.
  - The only PDF's that doesn't work for tend to be full-size textbooks (significantly larger than the average book page), but those are also the ones where layout tends to be the most important and I've had the most disastrous experiences with EPUB. Right now I just don't think it's realistic to read most textbooks on your phone in any format. (Plus you want to highlight, annotate in the margins etc., none of which is great on the phone anyways, but is great with a stylus/pencil on your tablet.)
- If the book contains lots of equations, ePub is not the best
- The problem is, **every single .epub reader renders things slightly differently** so when you tweak your ePub to make it look good on device A, it ends up looking bad on device B. 
  - The fixed layout of PDF is certainly restrictive, but at least it's consistent.

- Either all desktop epub readers suck or the format itself is bad, but as an end user, I've never felt pleased with any epub ever. I've tried many readers, configurations, etc 
  - Epubs always look wrong: the formatting is all over the place, fonts look off, I don't even know what font I'm supposed to use.
  - I've spent many hours trying to like epub, trying to tweak Calibre so that it doesn't look like complete crap (e.g. setting good margins), but to no avail.
  - PDFs almost always look fine. I don't have to think about fonts, margins, etc. it just works.

- 👉🏻 EPUB doesn't let us set a minimum length. EPUB also doesn't have line-folding glyphs. We are unlikely to release an EPUB or MOBI until they offer some way to deal with this problem.
  - What big tech publishers do to get around this problem is **embed low resolution jpegs** of the source code in their EPUBs. This is a terrible solution and we will not put something out that does this.
# discuss
- ## 

- ## 

- ## 

- ## [Ask HN: “Git” for Microsoft Office? | Hacker News](https://news.ycombinator.com/item?id=23245552)
- A couple years back I built this: 
- https://github.com/tomashubelbauer/modern-office-git-diff /js
  - It is a pre-commit script which unpacks Office XML into text contents and tracks that alongside the source file. This way you can consider the binary to be a source of truth, but with each commit you also get a textual diff showing what changed content-wise. More or less
  - This is achieved using a PowerShell script which unpacks the ZIP file to a tracked directory, formats the XML files for nice diff and tracks the formatted files as well.

- An underused feature in MS Word is 'Compare documents' - It's under the Review tab on the ribbon as 'Compare'. It allows you to do a 'diff' style compare on two Word documents - it's invaluable for working out what changed between versions if the place you are working at doesn't have any other document tracking systems.

- ## [Advice: I am planning on self-publishing a very complicated non-fiction book (indexes and endnotes and TONS of images) on two different platforms](https://www.reddit.com/r/selfpublish/comments/nhvtt6/advice_i_am_planning_on_selfpublishing_a_very/)
- Just wanted to say: the more images you have, the more difficulties you will have getting distributed on the ebook platforms 
  - If you 're doing physics, maybe SVG images might consume significantly less space for ebooks although Kindle support would be iffy.
- I use docbook to produce books. Indexes, endnotes, tables are a piece of cake on the printed version. It's possible to do single sourcing for both print and ebook, but I don't do it anymore for various reasons.
- LaTex is the gold standard for print publishing -- very well suited for academic publishing, but not for ebooks.
- MS Word can be good as a good source document, but for bigger projects it becomes unwieldy. You should use separate files for each chapter. The tricky thing about MS Word is using styles consistently.

- ## [Kindle 退出中国市场主要原因是什么？ - 知乎](https://www.zhihu.com/question/615489707)
- kindle的主要目的是为了架构一个电子书的平台资源，是想让你买书的……不是靠了阅读器来赚钱。
  - kindle早期的反盗版做的也不好，几乎就是一有书就立马被人脱库盗版然后发到网上传播。
  - 最近几年，国产的电子书阅读器也起来了，比起kindle的封闭，这些阅读器几乎都是安卓系统，支持更多的电子书平台app，比如多看、微信读书等。
  - 微信读书也是对kindle的一个沉重打击
  - 还有就是中国的网文文化盛兴，老多老多的人对传统读物已经没什么兴趣，但是喜欢阅读网文，网文走的是订阅制，一天一个章节这种。kindle这种拥抱传统读物的封闭玩意，在网文面前显得没有任何的用武之地

- 亚马逊上一本电子书的价格比纸质书都贵；而且基本上都是纯阅读功能，除了看书，你什么也做不了。
  - 带有手写功能的阅读器，KO3，2000多的价格，比同类型的阅读器贵出1000多，还具有性价比吗？
  - 《》里说，所有的事情都是类似情景的重现，以15年为一个循环周期来看，kindle已经撑得够久了。他需要换个崭新的时候重新发展，或者携带全新的产品重新和市场竞争

- 随着国内电子书阅读器品牌的崛起，如掌阅、文石等，Kindle面临着越来越激烈的竞争。

- 另一个不能忽视的因素是政策因素。近年来，中国政府对于国外电子产品的监管力度不断加强。Kindle在中国市场的销售和运营需要满足一系列的监管要求，这对于亚马逊来说无疑增加了额外的压力和成本。

- 中国的纸质书太便宜了。去看下欧美的纸质书，经常是大几百块钱，这时电子书的价格优势相当明显。但国内纸质书几十块钱，电子书也是几十块钱，完全没有价格优势可言。

- 纯阅读就是个伪需求，根本撑不起一个足够大的市场。电子阅读器能干的，成年人的随身必备品——手机，能干的更好。
  - 国内的阅读器现在正在试图把阅读器做成轻度办公本，阅读同样是个微不足道的功能。
