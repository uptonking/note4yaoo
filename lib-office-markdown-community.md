---
title: lib-office-markdown-community
tags: [community, mdx]
created: '2021-05-29T18:23:23.944Z'
modified: '2021-06-02T15:26:39.741Z'
---

# lib-office-markdown-community

# discuss-stars

- ## You shouldn't use Markdown for content anymore.
- https://twitter.com/kmelve/status/1494688125980798978
  - The demands of digital content have outpaced MD, so it's time to move on and figure out how we can do better.
  - Developers have shoehorned MD into a lot of places, even though it comes with significant trade-offs being non-standardized (even the attempts at standards aren't reliable) and quirky to parse. Plain text files don't equal being portable.
  - Markdown should be opt-in, and sure, MD-like shortcuts can be neat if you're used to it. But I wish we used our creative energy & engineering savviness to build great authoring experiences and presentation-agnostic formats, instead of forcing MD on people who never asked for it.
  - I'm coming at this as a pro Markdown user. I was _bought in_
  - But I have also felt the huge pain and friction in trying to port and salvage websites with all their content locked-in in markdown files and custom tags. 
  - It's costly and nearly and not a great use of time to get that content into a sensible and workable format.

- [Thoughts On Markdown](https://www.smashingmagazine.com/2022/02/thoughts-on-markdown/)

- ## Shortcodes vs MDX
- https://www.swyx.io/shortcodes-vs-mdx-3d4e/
- There are two prevalent solutions for injecting dynamic content into markdown: Shortcodes and MDX. 
- I think most people should use shortcodes, but there are also valid cases for picking MDX. 
- ### Defining Shortcodes
- The earliest instance I can find of Shortcodes is in WordPress.
  - Wordpress: [gallery id="123" size="medium"]
  - Dev.to: { % twitter 834439977220112384 % } (remove spaces)
  - Elder.js: {{shortcode foo=""}} optional inner content {{/shortcode}}
- The whole goal is that you can continue writing in standard plain text, but insert special components just by using a special syntax that wouldn't show up in normal writing
  - Shortcodes are the plaintext analog of Web Components - where a `<custom-element>` might extend HTML, shortcodes extend plaintext (typically Markdown). 
- ### Defining MDX
- MDX, introduced in 2018, inverts this model of content vs code. 
  - It renders your markdown as a React component (or Svelte component, with MDsveX), so it is very natural to add more React components inline
  - In my 2020 survey of the React ecosystem, all blogging documentation tools now offer MDX support by default.

- ### Comparing the Two
- #### Portability and Future-proofing
- MDX requires you to use React and a bundler plugin, tying you in to that ecosystem. 
  - Great if you stay within the lines of what they imagine, 
  - problematic if you want something slightly different or need to move off React (you now have to go through and convert all your content)

- Shortcodes are framework and platform agnostic. 
  - This is how I can blog on Dev.to and render on my own site (the inverted POSSE pattern), and have both render correctly in their native environments.
  - Though shortcodes still require a build chain to process them (including injecting scripts if needed), the minimal viable shortcode processor is no more complex than String.replace. 
  - Ultimately, shortcodes are more likely to show graceful degradation

- #### Scope
- MDX has a broader scope than Shortcodes in that it transforms the entire file - meaning that you can (and often should) supply your own versions of markdown components. 
  - This is handy for, for example, adding classes and preload handling to `<a>` tags, or adding hash links and id's to `<h2>` headers like I do on my blog.
- Shortcodes are limited to their immediate responsibility area - starting and ending with the brackets that designate them.
- #### Customizability
- With MDX, you can compose components as freely as you do JSX
- Shortcodes require you to predefine all the components you are going to use up front. 
  - If you'd like to add a new type of component, you'll have to jump out of your writing mode, go add some code to your components folder, and then jump back in to keep writing.
- #### WYSIWYG
- This is a minor point, but the fact that everything in markdown corresponds to a visible rendered element is a nice correspondence. 
- MDX breaks this by having `import` and `export` statements that compile away to nothing. 
- In practice this is no big deal but it slightly rankles me.

- ### Conclusion
- I think most developer bloggers spring for MDX because they enjoy using JSX, but they end up using the same 3-4 components on every single post or document they write. 
  - In those scenarios, they are accepting the downsides of MDX, without really benefiting from the customizability.
- However, there are still valid usecases of MDX.
  - For a design system or frontend component library, one might argue that MDX allows you to display the exact components 
  - Storybook's **Component Story Format** also provides a nice convention that keeps your documentation agnostic of MDX.
- Because MDX compiles to a React component, you could build tooling that can typecheck MDX
  - The same is doable for shortcodes, but since there is very little restriction on how shortcodes are processed, it is far less likely that successful shared tooling will arise.

- Finally, there's the question of customization. 
  - If you need to compose components inline as you write, then MDX is unquestionably the right choice. 
  - This is why Hashicorp went with MDX

- Perhaps a third "alternative" to Shortcodes vs MDX is structured content - discrete "blocks" of content rendered inside of a CMS, like you see in Notion, Sanity.io or in WordPress Gutenberg. 
  - I don't have a lot of personal experience with this, but my sense is that it locks you in to these systems, in exchange for WYSIWYG and no-code editing. 
  - In a way, structured content is what would happen if your writing is entirely made up of data inside shortcodes.

- ## Markdown编辑器 做成 WYSIWYG（所见即所得）形式会不会有什么弊端？
- https://www.zhihu.com/question/47789842
- 这取决于你如何看待 Markdown：
  - 一个方便生成 HTML 的工具，及其使用的「纯文本精简版 HTML」语法。
  - 一套用纯文本表达语义的语法，以及将使用这种语法的文档转换为实际表现的工具
  - 前者：并没有什么弊端。因为 Markdown 只是用来减少按键数的，关注的是最终的显示结果，而非 Markdown 文档本身。
  - 后者：弊端太明显了，这样的编辑器根本不是 Markdown 编辑器，而是借用了 Markdown 语法的所见即所得的 HTML 编辑器。Markdown 本身就是可以给人看的，转换为 HTML 并不是必须的步骤。typora 这样的所见即所得把 Markdown 本身当作「不必要的细节」处理了。

- ## How should markdown be saved and rendered?
- https://dev.to/michael/how-should-markdown-be-saved-and-rendered-51f
- All the responses here are right, and I definitely would stress @mortoray's point
  - There's a general rule for for asset transformation: **always keep the original**
  - I like to think of the HTML as a function of the markdown. 
  - Every time the markdown changes, run the function to output HTML. 
  - Within the main function are a series of other functions to handle each subtask and return the latest state of the HTML. 
  - I think the functional approach makes the process easy to modify and reason with.
- Storing as markdown keeps a lot of flexibility for later. 
  - In particular it lets you alter the design. 
  - HTML is overly structured and too strict to be design-change friendly. 
  - Many simple design changes would require altering the HTML, not just the CSS. 
  - IF you keep the markdown, the true source, it's easy enough to render new HTML.

- [How would you store Markdown?](https://www.reddit.com/r/Database/comments/iwvjse/how_would_you_store_markdown/)
- It's just text, store it in a text field.

- [What is the best way to store a field that supports markdown in my database when I need to render both HTML and “simple text” views?](https://stackoverflow.com/questions/17250972)
- Decide like this:
  - Store the original data (text with markdown).
  - Generate the derived data (HTML and plaintext) on the fly.
  - Measure the performance:
    - If it's acceptable, you're done, woohoo!
    - If not, cache the derived data.
- Caching can be done in many ways... 
  - you can generate the derived data immediately, and store it in the database, 
  - or you can initially store NULLs and do the generation lazily (when and if it's needed). 
  - You can even cache it outside the database.
  - But whatever you do, make sure the cache is never "stale" - i.e. when the original data changes, the derived data in the cache must be re-generated
  - One way to do that is via triggers.
- just store the data as HTML in the database and then process it to turn it into plain text. In my opinion there are some downsides to that:
  - You will likely need application code to strip the HTML and extract the plain text.
  - Processing the HTML blob can be slow.
  - HTML parsers don't always work well/they can be complex. 
- I would propose what most email providers do:
  - Store a rich text/HTML version and a plain text version. Two fields in the database.
  - As is the use case with email providers, the users might want those two fields to have different content.
  - You can write a UI function that lets the user enter in HTML and then transforms it via the application into a plain text version. This gives the user a nice starting point and they can massage/edit the plain text version before saving to the database.
  - 可参考gmail，可以切换标准视图 和 简单视图，注意是邮件网站自身变简单了，邮件内容还是很花哨但很慢、简单了一点
- Always store the source, in your case it is markdown.
  - You may need it for various purpose, e.g. the same input can be edited, audit trail, debugging etc etc.
- Also store the formats that are frequently used.
  - No overhead for processor/ram if the same format is frequently requested, you are trading it with the disk storage which is cheap comparing to the formars.
- Use on demand conversion/rendering for less frequent used formats.
  - Occasional overhead

- ## Need to fetch markdown from remote source via getInitialProps NextJs
- https://github.com/mdx-js/mdx/issues/789
- Fetching remote Markdown is something that an application I am working on needed to do as well. 
  - Using `@mdx/runtime` as the example posted by @millette is the same approach we ended up using 
  - and it has been effective for **returning compiled JSX to react** for render to the page.

```JSX
import Link from 'next/link'
import MDX from '@mdx-js/runtime'
import { MDXProvider } from '@mdx-js/react'

const FrontPage = ({ MDXContent }) => (
  <MDXProvider>
    <div>
      <p>Hello <Link href="/p2"><a>Earth</a></Link></p>
      <MDX>{MDXContent}</MDX>
    </div>
  </MDXProvider>
)

FrontPage.getInitialProps = async ({ req }) => {
  // console.log('FrontPage.getInitialProps') // , a, b, c)
  const res = await fetch('http://localhost:3000/c1.txt')
  const c = await res.text()
  // console.log('CCC', c)
  // return { MDXContent: '### more stuff' }
  return { MDXContent: c }
}

export default FrontPage
```

# discuss
- ## 

- ## 

- ## I like markdown-it plugin: `# A heading {#​id-for-heading}` .
- https://twitter.com/rauschma/status/1430458279096893440
  - Alas(不幸的是；哎呀), the available TOC plugins don’t pick up the custom ID. 
  - Thus, I’ll probably need to write my own TOC plugin. 
  - Last time I tried Remark, custom IDs + TOC didn’t work, either.
- AFAIK markdown-it is also the fastest tokenizer (i.e. it's ~easily extendable) for Markdown that we can use in the browser. 
  - markdown-wasm compiles it ~2x faster than that but it doesn't output tokens.
- To make it both more semi-standard and a syntax extension, do something with `remark-directive` , which is the best bet on a generic extension mechanism to markdown: `# heading :attrs{#​id.class title="text"}` .

- micromark’s has three primary goals:
- To allow really complex stuff (e.g., concrete syntax trees) that open up interesting stuff for the future
- to be a better base for remark (and the rest of unified) — it’s architecturally better, more readable/reasonable/powerful, CM and GFM compliant, etc
- to provide an alternative for what most folks think they want out of markdown. 
  - remark and ASTs are powerful but also a bit complex; 
  - folks coming from marked or markdown-it and the like *just* want HTML out (w/ maybe a couple extensions)
- Generating a toc is hard in micromark (it’s build in a way that could be streaming, so it spits out HTML immediately), and easy in an AST (find all headings, get their slugs and text, ...)
  - (also this example was specifically on rehype/hast/html, which is even closer to what people are familiar with, e.g.,  `a` and `h1`, compared to remark/mdast/markdown, which has different link constructs)
- Interesting. Pandoc’s filter system supports multiple passes. Especially for TOCs that’s a very clean approach.
  - Yeah, that’s intentionally, those filters are closer to the AST stuff that unified does. micromark doesn’t have an AST; it’s straight to HTML (or to an AST), exactly for people that don’t need multiple passed!
- If I were to add a TOC to micromark, I’d:
  1. Run micromark a first time, collect the headings.
  2. Insert the TOC when running micromark a second time.
- Ah. That might work.
  - micromark is intentionally low-level so there’s no knowledge of a “filename” for a stream/buffer/string. 
  - So assuming multiple files are processed you’d have to track that yourself. But otherwise, that could work!

- ## Joplin Note: Alternative markup like Asciidoc
- https://discourse.joplinapp.org/t/alternative-markup-like-asciidoc/2059
- Joplin is really built around Markdown so alternative markups will not be supported. However it might be possible to add the features you need via markdown plugins.
- Yes I see what you mean but this is currently not an objective as it would be complicated to support multiple markups, and it’s not something that we do and it’s done - it’s a lot of complexity that we’ll have to deal with permanently afterwards. It’s not just rendering, there are other parts of the code that expect Markdown. For example:
  - There’s a service that index the resources used by notes - to do that we need to parse the Markdown note.
  - Likewise, there’s a TOC popup that is planned and it will be built based on the markdown text.
  - The search engine indexing most likely will need to be tweaked for each markup.
  - We could have a tool that helps creating Markdown tables.
  - When we import Markdown file, currently we just copy the text to the note. But if we support multiple markup, it would be logical to convert the MD text to the currently active markup.
- Now every time we change something to these parts of the code, it will have to be updated x times, for each supported markup. There are several other examples like this. So that’s why in this case it makes sense to restrict the scope of the project to allow building other useful features.
- Asciidoc is a superset of Markdown, even with flavors, so with a fixed Markdown flavor it is feasible to convert from Markdown to Asciidoc

- ## Reasons to not use Asciidoc as a foundation for a software documentation language__202002
- https://www.eclipse.org/lists/asciidoc-wg/msg00003.html
- After many years using Asciidoc in larger projects, I have come to the conclusion that Asciidoc is not a good foundation for writing technical documentation though. Some reasons are:
1. The syntax is not consistent. There are different syntax constructs for different things. 
  - E.g., setting parameters for certain elements does not follow a single concept. 
  - In some cases a dot is used as prefix, sometimes not, in other cases assignments are used ([.xxx] vs. [xxx] vs. [xxx=yyy]). 
  - And the “+” sign at the end of a line is really a pretty bad idea.
2. The syntax is not intuitive nor readable. 
  - The Github flavored markdown spec contains a nice comparison of Asciidoc vs markdown. 
  - I think the example is self-explaining.
3. There is no clear definition of blocks and nesting. 
  - This makes it really hard for longer texts to write and read. Some things can be nested, others cannot — very confusing.
4. The output cannot be split-up into multiple HTML files. 
  - This is a severe issue when it comes to really long documents, which could easily be the case for specifications. 
  - You can see the difference here: While the first one needs quite some time to load, the latter loads very fast. I wrote the split-up tool myself, see below as well.
5. PDF output is not acceptable. For example, footnotes are not supported. Overall the PDF quality is very poor. 
  - So if you use Asciidoc, you are limited to HTML. 
  - As a site note: Also epub is not supported.
6. Important features for technical documents and specifications are missing, such as special numbered blocks, e.g., for requirements, examples etc. 
  - As a consequence no list of these special blocks, such as list of requirements, list of examples etc., can be created.
7. Linking is an issue. 
  - In particular for documenting software projects, it would be crucial to refer to code (e.g., in the source code repository).
- Issues 4 to 7 may be solved with newly written tools — however that would require a lot of effort, basically writing a new Asciidoc processor from scratch. 
  - But then there are still the issues 1 to 3, which cannot be solved except for simply not using Asciidoc.
- In the Eclipse N4JS project, we have used Asciidoc (and Asciidoctor) for quite some time. 
  - n order to understand why I would not use Asciidoc in the future, simply have a look at some of the Asciidoc sources linked above — they are very hard to read, aren’t they?
- Instead of establishing an AsciiDoc Working Group, I would recommend to establish an (Eclipse) Markdown Working Group
  - Markdown is better readable, and it would be possible (as a working group at Eclipse) to define a defined set of extensions (similar to the Github flavor md), a clear definition of blocks (via indention for example) and other things. 
  - I would strongly recommend to not use Asciidoc as a base for a software documentation language due to the problems described above. 

- ## MyST markdown provides a markdown equivalent of the reStructuredText syntax, meaning that you can do anything in MyST that you can do with reStructuredText
- https://twitter.com/simonw/status/1272744281531285504
  - 

- ## HOW TO ESCAPE A BACKTICK WITHIN A CODE BLOCK IN MARKDOWN
- https://www.danvega.dev/blog/2019/05/31/escape-backtick-markdown/
- The first solution to our problem is to use more backticks. 
  - 比如下面顶层使用4个反引号，缺点是默认的格式化工具会打乱格式

~~~~markdown
This is some text

```js
console.log('Hello, World!');
```

```js
console.log('Hello, World!');
```

~~~~

- 方法2: using the tilde character

~~~markdown
This is some text

```js
console.log('Hello, World!');
```

```js
console.log('Hello, World!');
```

~~~

- ## Next.js love MDX, but there are tradeoffs:
- https://twitter.com/ericclemmons/status/1400577327201984517
- hashicorp/next-mdx-enhanced
  - deprecated: next-mdx-remote is ~50% faster, more flexible with content storage, does not induce memory issues at scale
- hashicorp/next-mdx-remote
  ✅ get*Props
  ✅ Local/Remote content
  ⚠️ eval
  ❌ No `import` in MDX
- mdxjs.com
  ✅ .mdx pages
  ✅ import Post from "./post.mdx"
  ❌ getStaticProps
  ❌ frontmatter
- xdm might have the right trade offs you need?

- ## Why do bloggers love Markdown? Why use MDX? And other notes from MDXConf_202008
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
