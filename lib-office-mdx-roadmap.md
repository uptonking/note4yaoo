---
title: lib-office-mdx-roadmap
tags: [markdown, mdx, office, roadmap]
created: '2021-05-29T14:50:34.724Z'
modified: '2021-05-29T14:51:21.929Z'
---

# lib-office-mdx-roadmap

# guide

- md-rfc
  - collapsible block
# draft
- 不支持在mdx中直接书写import esm-url
  - https://cdn.skypack.dev/jquery
  - https://cdn.jsdelivr.net/npm/jquery@3.6.0/dist/jquery.js
# mdx vs md
- [Where MDXjs is different than Markdown](https://github.com/mdx-js/mdx/pull/1039)

- Most likely breaking changes from MDXjs 1
- You can’t have random `<` or `{` in text anymore
  - 需要使用 &lt; 转义字符
- You can’t have HTML comments anymore
  - use `{/*I'm a comment*/}` , but not `<!--I'm a comment-->`
- Blocks will be blocks
  - now more chill about mixing Markdown with JSX

- new features in v2
  - You can indent your tags and expressions the way you want (within reason)
  - Interleaving Markdown in JSX
  - Blocks can have blank lines now
  - Expressions everywhere(in jsx/md/html)
# roadmap

## [RFC: MDX plugins](https://github.com/mdx-js/mdx/issues/741)

- The plugins from remark and rehype have been great to add in features and functionality, 
  - however I think MDX-specific plugins can take advantage of features more inline with the MDX language.
- common needs in the MDX ecosystem 
  - frontmatter, table of contents, syntax highlighting, oembed, etc
  - which don't make sense in core but are complex to set up or configure.

- The way it works today
  - a single plugin to set up everything it needs across all transformations `MDX => MDAST => HAST => JSX => React|Vue`.
  - use remark-toc to achieve some, but it doesn't give you much flexibility in how/when the toc is rendered and it doesn't allow the heading information to be imported from outside the document.

- Detailed design
  - MDX plugin would be given access to each stage of the transpilation pipeline. This means that a plugin could manipulate the MDAST and HAST
  - MDX plugins would be passed as their own option and would be appended to the existing remark/rehype plugins.
  - The component rendering portion would exist in userland to avoid any magic. They'd have to be manually added to MDXProvider at the layout level.
  - this wouldn't require much engineering effort since we'll be mostly forwarding plugins to remark/rehype/babel.

## [AST node name changes in next.9](https://github.com/mdx-js/mdx/issues/1503)

- An import and an export next to each other are now combined into a single mdxjsEsm node.
  - At the very least, it'd be ideal if we partition/separate exports and imports, they're semantically and intentionally different.
- The reason for having a single node that contains arbitrary JavaScript is (a) in alignment with how it’s parsed, but importantly (b), to allow extensions to what’s allowed. 
  - Such as var/let/const feature without adding new nodes
- That single arbitrary JS node also allows MDX to be extended to support

```
'''js eval
var number = Math.PI
'''

The number is {number}.
```

- Another idea is to allow more vue/svelte like syntax

```JS
<script>
  var number = Math.PI
</script>

The number is { number }.
```

- To answer “they're semantically different”
  - On the JavaScript level they are. 
  - And they are separately available as a subtree. 
  - Folks can inspect and transform those subtrees, which is in my opinion preferable over trying to handle a serialized value (such as what `remark-mdx-frontmatter` does), 
- Exposing the JavaScript in a plugin mechanism is now also a minor release away in @mdx-js/mdx. 
  - This would allow arbitrary JavaScript transforms, such as minification (terser) or bundling (what `mdx-bundler` does currently).

## [MDX v2: Umbrella issue](https://github.com/mdx-js/mdx/issues/1041)

- Please note: Nothing written here is final
- Drastically improved parsing with new parser
  - The new parser will address a large amount of papercuts
  - It also adds JSX usage into the AST which will allow users to perform their own transforms with plugins.
  - support expressions throughout a document
  - [Rewrite how MDX is parsed_202005](https://github.com/mdx-js/mdx/pull/1039)
- Official Vue support
- TypeScript support

- **rfc**
- accepted
  - drop node 8 support 
  - MDX plugins
  - Interleaving(插入) Markdown in JSX
  - Multiple MDXs in a Single File(like mdx-deck)
  - let/const/var support, or [executable code block](https://github.com/mdx-js/mdx/issues/1046)
  - Remove autolink syntax
- declined
  - Consolidate pre/code/inlineCode
- discussing
  - MDX comment syntax
  - MDX block parsing
# changelog
