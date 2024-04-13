---
title: lib-office-community-wikipedia-baike
tags: [baike, community, office, wikipedia]
created: 2023-09-21T17:32:34.942Z
modified: 2023-09-21T17:33:01.520Z
---

# lib-office-community-wikipedia-baike

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 🔀🐛 [Ibis, a federated Wikipedia alternative | Hacker News _202403](https://news.ycombinator.com/item?id=39694045)
- I do not understand how federation is going to solve the problems mentioned in the homepage. Surely it is going to make them 10x worse, right? The same incidents can happen, but it becomes impossible to moderate the content.

- The real wikipedia renders (perfectly!) without javascript. This does not render at all without javascript. Not an alternative.

- Automatically merging updates between different variants of the article, in fact, seems like a terrible idea. This is because resolving conflicts between edits is easy, but making sure that (for lack of a better word) semantic conflicts don't make it through requires a manual review of changes.
  - Your CRDT merge can be a technological marvel that will seamlessly stitch together different edits on a topic... that say wildly different things about it, resulting in a completely nonsensical article.

- CRDT adds automatic conflict resolution, wikis need at most, if any, manual conflict resolution, because their page editing has little need for concurrent real-time edits, it's a slower process (ironic given the meaning of wiki in Hawaiian). 
  - About git, OP tried to explain to non-wiki editors what wikis do under the hood, conflict reconciliation in wikis is vaguely similar to git but simpler, and the tech Ibis uses, paired to a design for independence prone to content rotting (every url of the federation can differ even in context about any page), makes me smell of just importing by hand or by trust edits from peers into the backing store.

- I think it depends what you want. Diffs are better if you want to review changes and intelligently merge them.
  - CRDT is better if you want there to be just one document that everyone is editing at the same time, with merging being an automatic process and the rare non-sensical merge being acceptable.

- It doesn't matter all that much whether your servers are federated or served from a single domain, the time users spend with the page editor open is much longer than the latency of a federation request. A server somewhere might be horribly out of sync and cause a lot of conflicts, but presumably those are also the scuffy servers with low traffic that don't see a lot of edits per minute anyways.
  - CRDT is cool, but it's deploying a very shiny new tech for a small problem that doesn't really need anything fancy.

- CRDTs make sure there is only one version, but that version might be garbage. Think taking all the lines from all conflicts in git. Sometimes it's ok, sometimes not. It's even worse than that: you don't know there was a conflict, so you don't know if there was a problem or not. It's trying to solve social problems with technology, it's never enough (but can bring us a good way there)
  - Manual merging is mandatory to have human meaning, so might as well use it all the time.

- CRDTs are cool for tiny concurrent edits. For example two people typing on one line. 
  - But it doesn't save you when you get large conflicting edits. No system can automatically merge instance A removing a sentence and instance B adding some words within the that sentence. It's still the user that will have to make a decision. 
  - And at that point, you're effectively looking at a git style 3-way merge.

- Wikipedia is an amalgam of a large number of humans editing w/ some guardrails provided by the guidelines and tech (clean-up bots, edit alerts). If there's a human problem (corruption, bias), there's no tech solution that'll magically make all of it go away.

- The reason to make a new wiki or wiki-style technology is to serve a different informational niche, guided by different rules. There's a reason each video game has its own Wiki. 

- Reading through, this doesn't sound like a "federated wikipedia"
  - It sounds more like they want to implement the github fork & pull-request model of version control where currently Wikipedia uses a more SVN type of version control.
  - There are pros and cons to both models. However federation it is not. The mentioned controversies also seem entirely unrelated to which model you like.

- I think there's a spectrum of knowledge-base like solutions, but the middle of the spectrum is often poorly served:
  - wikipedia: global, canonical reference material. Is very good, and we almost all use it in some fashion.
  - confluence/notion/gh-wiki: team knowledge base. Often spotty, stale, neglected.
  - logseq/obsidian/org-mode: personal knowledge base, notes. Typically very idiosyncratic, sketchy, but can work very well for the people who put effort into it.
  - What if a "federated wiki" was targeted at the team/personal level? I'm not saying this is Ibis in its present form

- How does moderation work in this system, and if it results in multiple diverging pages on the same topic, how is any of it trusted?
  - As much as it's a complicated mess, a centralised system with a broad army of moderators operating to similar standards, is the feature of Wikipedia. They may be wrong at times, but they're accountable somewhat collectively for that and so hold each other to account.
# discuss-format
- ## 

- ## 

- ## [How to download all of Wikipedia onto a USB flash drive | Hacker News_202210](https://news.ycombinator.com/item?id=33114107)
- I wish one could create new articles in Kiwix’s zim files. Right now, Kiwix is basically a Wikipedia reader. Editing features would be very nice for local wikis to develop, and later on — maybe — to have such local article editions merged into the main Wikipedia, perhaps similar to how git works.

- **The `.zim` file format is heavily optimized for compactness and ease of serving**.
  - For starters, it doesn't even store the original MediaWiki markup, but rather pre-rendered basic HTML. Images only have the thumbnail version (the one that's shown inline when reading the article), there's no full-size to zoom in.
  - And, of course, no edit history.
  - Multiple articles then get bundled into clusters of ~1Mb each, and each cluster compressed using ZSTD.
  - This all lets you squeeze English Wikipedia into 90 Gb. But **it also makes it much more difficult to edit in-place**, and, of course, no MediaWiki means that it cannot possibly work like git pull requests.
- I totally understand the reason why **it is made for read-only consumption**. However, we live in a moment where storage is significant cheaper, and so is processing. There could have a compromise, though I do not see any indication of such. SQLite could very well be used here.

- I was curious how they achieve this. It looks like the underlying file format uses LZMA, or optionally Zstd, compression. **Both achieve pretty high compression ratios against plain text and markup**.
  - Its file compression uses LZMA2, as implemented by the `xz-utils` library, and, more recently,          `Zstandard`. 
- The more important thing is that they **aggressively downsize the images and omit the history and talk pages**. Even if they were using LZW it would probably only triple the filesize.

- 👉🏻 File size is always an issue when downloading such big content, so we always produce each Wikipedia file in three flavours:
  - **95.2 is the "maxi" file. 49.48 is the "nopic" file. 13.39 is the "mini"**.
  - Mini: only the introduction of each article, plus the infobox. Saves about 95% of space 
  - vs. the full version. nopic: full articles, but no images. About 75% smaller than 
  - the full version Maxi: the default full version.

- Kiwix's maxi-all Wikipedia zimfiles have pretty much all the pictures that are used in articles, but not the video and audio. And the pictures are too small; often you can't read the text in them.

- There is a ZIM file that contains all of stack overflow. Super useful if you have to program without access to the internet.

- How does this scale with the need to update data with time, corrections etc? Having to download everything again doesn't seem that elegant. I think this wold benefit a lot from some form of incremental backup support, that is, download only what was changed since last time. A possible implementation of that could be a bittorrent distributed git-like mirror so that everyone could maintain their local synced one and be able to create its snapshot on removable media on the fly.
- **Given that the ZIM format is highly compressed, I'd assume that any "diff" approach would be computationally quite intensive** – on both sides, unless you require clients to apply all patches, which would allow hosting static patch files on the server side.
  - Bandwidth is getting cheaper and cheaper, and arguably if you can afford to get that initial 100 GB Wikipedia dump, you can afford downloading it more than once (and vice versa, if you can download multi-gigabyte differential updates periodically, you can afford the occasional full re-download).

- It looks like Kiwix uses the ZIM file format, which appears to have diffing support (see **zimdiff and zimpatch**). That said, it doesn't look like Kiwix actually publishes those diffs.

- FYI, the internet archive hosts a ZIM archive that has dumps of wikipedia and many other works
  - [ZIM File Archive : Internet Archive](https://archive.org/details/zimarchive)
  - Archive of MediaWiki . ZIM Files. The ZIM file format is an open file format that stores wiki content for offline usage. Its primary focus is the contents of Wikipedia and other Wikimedia projects.

- The zim file format is far from ideal for compression efficiency - all the best algorithms typically don't allow random access without decompressing everything. Also, wikipedia has a lot of spam and orphan pages, insanely long lists, etc. Those are hard to algorithmically filter out.

- Kiwix has Stack Overflow (and various StackExchange subsites), Project Gutenberg, TED talks, and plenty more. You can also request something.

- ## [The kiwix *Wikipedia-en* full scrape with images has been broken for over 18 mon... | Hacker News](https://news.ycombinator.com/item?id=22681589)
- The whole zim file infrastructure/toolchain is pretty broken. I've been trying to put together a system for generating a WARC file by rendering all the wikitext content in a database dump, which is a lot more reasonable of an approach.
  - Generally I have not been very impressed with the quality of ZIM file tooling. One disadvantage is you need to provide separate search indexing, but that's doable.

- In general, I'd say that ZIM and WARC are not really direct competitors or solutions to the same problems, they're really for distinct use-cases. 
  - ZIM is a highly-compressed format that's designed solely for static articles and flat content, it doesn't really store headers or anything else that WARC does in order to support full request/response replaying.
  - ZIM is optimized for storing thousands to millions of pages of homogenous(同种的; 相似的) content, WARC is optimized for high-fidelity collections of smaller amounts of content.
# discuss
- ## 

- ## 

- ## 

- ## [How to Extract Data from Wikipedia and Wikidata | Hacker News_201703](https://news.ycombinator.com/item?id=13966965)
- Worth mentioning is dbpedia, which is an open database made from extracting data from Wikipedia.
- RDF triple stores were the latest hype during Semantic Web era. Wouldn't a more general NoSQL/Graph or SQL database be suitable as well, if soneone wrote an import script. I read someone achieved in with MySQL and a star table schema.

- By coincidence for another project, I was trying to mine Wikipedia. It is better to try and parse the html than mess about with the text. The wikidata stuff can be quite inconsistent also in what it returns.

- ## [Show HN: Static.wiki – read-only Wikipedia using a 43GB SQLite file | Hacker News_202107](https://news.ycombinator.com/item?id=28012829)

- Shocked to find out that this is very much a static website, it's "merely" downloading a small portion of the 43GB SQLite file in question with HTTP Range requests, and then it uses a WASM-compiled copy of SQLite to query the requested data. Very impressive.
- wouldn't this be vulnerable to DOS attacks? I can make the database run arbitrarily long and complicated queries
  - Since the work all happens in your browser, the only victim of a long complicated query would be you own browse and the S3 bandwidth bill of the person hosting the database (since you'd end up sucking down a lot of data).
  - It's a static file, CDN it.
  - But if you want to jack up someone's S3 bandwidth bill there are already easier ways to do it!

- Read-only Wikipedia is just "Wikipedia" for 99.99% of users. I can't remember the last time I've even considered clicking the edit button.

- The full text search engine in SQLite is sadly not really good for this - one reason is that it uses standard B-Trees, another is that it forces storing all token positions if you want BM25 sorting, which is a huge overhead for articles as long as Wikipedia's.
  - But that doesn't mean full text search isn't possible in a very efficient manner with statically hosted data! I wrote a proof of concept of making the Rust-based tantivy library work in the same way, which has a lot of internal things that can make the index much smaller and more efficient than SQLite's. It's also >10x faster in creating the search index

- I built a wikipedia reader on the ipad years ago, I used two sqlite databases, 
  - one for the article titles using sqlite FTS then I compressed the articles themselves and merged the compressed chunks into a set of files < 2G, the title database had the offset into the compressed blobs. Only including the most popular pages, it was just under 10G.
  - I used 2 sqlite databases just to store the article titles and offsets into binary files (<2GB) that had chunks of compressed data. Each chunk contained 10s-100s of stories, so that the decompressed around was around 20megs I believe. I had planned to store everything in sqlite, but there were too many issues. The FTS extension to sqlite is excellent, it made whole classes of problems literally melt away.
  - Recalling now, the article text itself, I stored in groups of articles concatenated together so that that data compression could take advantage of similar texts.

- Torrents aren't great for random access which this app is doing.
  - Bittorrent can do random access just fine, especially with v2 which enables content verification in 16KB chunks. Clients tend to be throughput oriented which leads to sub-optimal latency, but that's not a limitation of the protocol.

- I've been using static copies of Wikipedia for years; they're great to have when traveling. I mostly use the Kiwix app. Their ZIM format database for all English is 83 GB; 43 GB for one without pictures. Compares nicely to the 43 GB here.

- 
- 
- 
- 
