---
title: thread-format-dev-usage
tags: [format, json, json5, thread]
created: 2021-01-20T04:23:21.917Z
modified: 2021-01-20T04:24:24.783Z
---

# thread-format-dev-usage

# guide

# discuss-files-format
- ## 

- ## SaaS弱化了文件的概念，一方面大家对“新”品类都有着自己的理解，各有各的玩法。
- https://twitter.com/mayneyao/status/1778549269924065556
  - 只有等市场沉淀到一个合适的时间节点，有了共识之后，才能“车同轨，书同文”
  - 无限白板是一个“新”品类，它值得拥有自己的通用格式。
- 软件的可逃逸性
  1. 导出文件而不丢失信息，并且存在多个支持该文件类型的同类软件。
  2. 导出退而求其次的通用格式文件，丢失部分非关键信息
  3. 提供 API 
  4. 不支持导出
- 文件格式越复杂，表达能力越强。相应的，越难存在一个通用的文件格式。富文本和 markdown 之间的关系很好的诠释了这一点。

# discuss
- ## 

- ## 

- ## JSON5 is pretty cool. Babel uses it for its configs._201711
- https://twitter.com/jdalton/status/935761621804339200
  - Other projects like eslint, npm, & node might find it useful too.
- Ok so JSON5 was cool and all but now there's JSON6
- Chromium also adopted json5 a bit ago
- JSON5 remains a strict subset of JavaScript“ in the article which is why I closed the tab again. Too bad
- JSON5 will do half of what CSON, YAML and others were doing 5 years ago, hooray!

- ## I honestly find that "//": "This is a comment" as an object key/value works pretty well for most of the times I need comments in JSON.
- https://twitter.com/domenic/status/962144752320811008
- The other thing I like about JSON is that it doesn't allow silly style differences; it picks one. 
  - No extra commas; always double quotes; keys always quoted; no leading/trailing decimal points... 
  - Making everyone's JSON follow the same rules is really, really nice.
- This is why I can't recommend JSON5; 
  - sure, it adds one or two nice things like comments or multiline strings, 
  - but it also does everything in its power to resurrect(使复苏；重新使用) the style/formatting wars that have plagued JS and foist them upon JSON.
- I’ve recently delivered a project to a client that uses JSON as the config file format. 
  - Lack of comments means I can’t self document the file and all options inline. 
  - And a “//“ as an object key (or an item in an array) is not going to cut it.
  - Can’t use it in an array without stripping out elements in the comsumer
  - Can’t use it for 3rd party  code unless you’re certain it doesn’t barf on unknown keys or depend on count of keys. 
  - Someone also has to maintain the code I hand over that’s makes the in-band signalling ok.
  - + most tools that read in the json, edit it and serialize it often remove duplicate keys or reorder them which results in chaos and sadness. 
- Can’t comment array items though :/
- I think this has a problem if you ever process the file (e.g. package.json is often machine and hand edited). 
  - Duplicate comment keys will clobber each other!

- ## For a while I was in favor of using YAML for storing tokens and metadata in a design system, as it looks simpler and cleaner than JSON, and supports comments.
- https://twitter.com/kaelig/status/1305239486687711232
  - Having seen people struggle with it, I think JSON5, vanilla JavaScript or TypeScript are more appropriate.
  - The main struggle I witnessed was with producing valid YAML, especially when editing directly in GitHub. 
  - It’s very easy to mess up indentation, and multiline strings are fantastic but so unfamiliar that people almost always get them wrong.
- I loathe JSON (y u no number interop or comments!?!!!) and find YAML worse in every practical way.
  - It all makes me want to suggest some nice, simple XML Schema
  - Srsly, tho, JSON5 > YAML every time.
- We’ve had computers for 80 years now and we still stump ourselves with indentation?
- I still like YAML but have been interested in exploring ideas for agnostic inputs (not just outputs).
- Agree. YAML is not user-friendly.
