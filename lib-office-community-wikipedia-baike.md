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
# discuss-format
- ## 

- ## 

- ## [How to download all of Wikipedia onto a USB flash drive | Hacker News_202210](https://news.ycombinator.com/item?id=33114107)
- The `.zim` file format is heavily optimized for compactness and ease of serving. 
  - For starters, it doesn't even store the original MediaWiki markup, but rather pre-rendered basic HTML. Images only have the thumbnail version (the one that's shown inline when reading the article), there's no full-size to zoom in. 
  - And, of course, no edit history. 
  - Multiple articles then get bundled into clusters of ~1Mb each, and each cluster compressed using ZSTD.
  - But **it also makes it much more difficult to edit in-place**, and, of course, no MediaWiki means that it cannot possibly work like git pull requests.
- I totally understand the reason why **it is made for read-only consumption**. However, we live in a moment where storage is significant cheaper, and so is processing. There could have a compromise, though I do not see any indication of such. SQLite could very well be used here.

- FYI, the internet archive hosts a ZIM archive that has dumps of wikipedia and many other works
  - [ZIM File Archive : Free : Free Download, Borrow and Streaming : Internet Archive](https://archive.org/details/zimarchive)
  - Archive of MediaWiki . ZIM Files. The ZIM file format is an open file format that stores wiki content for offline usage. Its primary focus is the contents of Wikipedia and other Wikimedia projects.

- The zim file format is far from ideal for compression efficiency - all the best algorithms typically don't allow random access without decompressing everything. Also, wikipedia has a lot of spam and orphan pages, insanely long lists, etc. Those are hard to algorithmically filter out.

- ## [The kiwix *Wikipedia-en* full scrape with images has been broken for over 18 mon... | Hacker News](https://news.ycombinator.com/item?id=22681589)
- The whole zim file infrastructure/toolchain is pretty broken. I've been trying to put together a system for generating a WARC file by rendering all the wikitext content in a database dump, which is a lot more reasonable of an approach.
  - Generally I have not been very impressed with the quality of ZIM file tooling. One disadvantage is you need to provide separate search indexing, but that's doable.

- In general, I'd say that ZIM and WARC are not really direct competitors or solutions to the same problems, they're really for distinct use-cases. 
  - ZIM is a highly-compressed format that's designed solely for static articles and flat content, it doesn't really store headers or anything else that WARC does in order to support full request/response replaying.
  - ZIM is optimized for storing thousands to millions of pages of homogenous(同种的; 相似的) content, WARC is optimized for high-fidelity collections of smaller amounts of content.
# discuss
- ## 

- ## 

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
