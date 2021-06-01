---
title: lib-office-mdx-community
tags: [community, mdx]
created: '2021-05-29T18:23:23.944Z'
modified: '2021-05-29T18:23:39.607Z'
---

# lib-office-mdx-community

# discuss-stars
- ## Markdown编辑器 做成 WYSIWYG（所见即所得）形式会不会有什么弊端？
- https://www.zhihu.com/question/47789842
- 这取决于你如何看待 Markdown：
  - 一个方便生成 HTML 的工具，及其使用的「纯文本精简版 HTML」语法。
  - 一套用纯文本表达语义的语法，以及将使用这种语法的文档转换为实际表现的工具
  - 前者：并没有什么弊端。因为 Markdown 只是用来减少按键数的，关注的是最终的显示结果，而非 Markdown 文档本身。
  - 后者：弊端太明显了，这样的编辑器根本不是 Markdown 编辑器，而是借用了 Markdown 语法的所见即所得的 HTML 编辑器。Markdown 本身就是可以给人看的，转换为 HTML 并不是必须的步骤。typora 这样的所见即所得把 Markdown 本身当作「不必要的细节」处理了。
# discuss
- ## 

- ## 

- ## Why do bloggers love Markdown? Why use MDX? And other notes from MDXConf 202008
- https://katiekodes.com/why-markdown-mdx-mdxconf/
- Markdown’s main purpose is to make you type less stuff.
- The “MDX library, ” at its core, is a function 
  - that takes an input parameter of a `string` formatted according to the MDX spec
  - and returns a value that’s a `string` formatted according to the JSX spec.

```JS
async function mdx(mdxString) {
  // The "processor" is the thing capable of building a JSX string out of an MDX string
  const processor = ...STUFF - HERE... // Uses the "unified" package
    const file = await processor.process(mdxString)
  return file.contents
}
```

- Do I even want a JSX string?
  - NO
  - I’m just looking for “shortcuts” to blocks of HTML.
  - JSX might be overkill where a bunch of extra objects within a CMS and some static site generator templating would do.

- Yes: CMS previews
  - some CMSes are React apps
  - the same codebase is used twice for both the CMS and the SSG.

- Yes: slight tweaks to the Markdown interpreter
  - highlight code of line 10-13

- Yes: nestable Markdown
  - import md from another-md
  - import component/data/meta from anthor-md

- Maybe: actual React app websites
- Maybe: templating portability
- Maybe: laziness(borrow people's components/)

- ## On the limits of MDX_202002
- https://www.knutmelvaer.no/blog/2020/02/on-the-limits-of-mdx/
- I don't think MDX should be “considered harmful”, nor that everyone should stop using it. 
- But I think there are some things worth considering before locking your, or rather, others’ content to it. 
- Markdown's key feature though, is "easy-to-read, easy-to-write"

- What is the problem MDX tries to solve?
  - Markdown was designed at a time where most of the web authoring was still done in HTML.
  - Web content has moved towards a much richer set of components, from embeds to interactive codeblocks, to between-paragraphs call to actions.
  - MDX seems like an attempt to make these components available to the author in the same syntax used in frontend development 
- But this problem has been solved already. 
  - With something they call “rich text editors”
  - There's plenty of content platforms with plenty of rich text editors that spews out plenty of different formats, including markdown, HTML, and abstractions as MobileDoc and Portable Text. 
  - medium, notion...
  - Arguably, these interfaces are more friendly and more accessible than learning Markdown, or MDX.
- when I have been made to write MDX.
  - mess the syntax up all the time
  - No syntax highlighting
  - No helpful error
  - I had to actually look up a bunch of documentation just to make a code exampe or a “note”

- Writing with a markup syntax should be opt-in, not forced upon you.

- For most uses of MDX, you will end up mixing specific presentation concerns with your content. This is not great.
  - Yeah, it kinda worked for HTML. 
  - 若像html一样定制样式后，mdx代码会凌乱不堪，html代码也很乱
- For people working with content strategy, content is best stored as ingredients from which you can bake the things that you need when you need it.
  - They have been preaching “structured content” for ages, and fighting with CMSes that force content into WYSIWYG page builders and make editors copy-paste their texts around in small layout boxes prisons.
- You should think really hard about how you want to be able to work with your content, the inclinations of whom you want to work with your content, and finally, how sustainable and flexible your structuring of it is.
# ref
- [Rich-markdown-editor: react Dropbox Paper clone](https://news.ycombinator.com/item?id=23462083)
