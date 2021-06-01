---
title: lib-office-markdown-mdx
tags: [lib, markdown, mdx]
created: '2021-05-27T01:41:58.386Z'
modified: '2021-05-29T14:51:54.256Z'
---

# lib-office-markdown-mdx

> easy to read， easy to write， content-centric notebook

# guide
- goals
  - 易读易写
  - 上传mdx，能够渲染出html(~~应该是ssr吧~~)，
  - 能够在渲染的页面编辑mdx
  - 能够在渲染的页面编辑ojs

- is-goal???
  - 导出的使用场景哪个多一点，是docx，还是pptx，office标准的ooxml格式规定了很多属性和配置，在设计实现导出时要参考
  - 样式丰富的图表、地图很难通过文本表达，通过WYSIWYG能实现，此时编辑器最好是block的，可作为后期目标

- non-goals(难用简单文本实现)
  - 不建议定制各种组件的各种样式细节，样式越多输出的代码就越多，就显得凌乱且难迁移；
    - 提前告知用户，支持保存到本地的文件形式有3种，
    - 一种只包含基本样式但易迁移，通常可跨平台设备查看，
    - 一种包含丰富样式但代码乱，且**以后迁移跨应用可能失败**
    - 一种导出office，支持导出的组件有限、样式有限，平台自定义的组件和样式都不会导出
  - 导出高级组件：图表的代码；嵌入的视频
  - 不要执着于mdx的解析器和渲染实现
    - mdx大部分的规则都是兼容markdown的，所以可以考虑扩展markdown现有的工具库，如showdown、json2md、@dimerapp/markdown(remark)、md-2-json(marked)

- mdx-features
  - markdown-based simplicity
  - powerful jsx with large ecosystem
  - everything is a component
    - import jsx components and render components
  - customizable: 可通过MDXProvider替换h1、p
  - blazing fast: no runtime
    - all compilation occurs during the build

- mdx-cons
  - *控制布局、动态修改更新布局*
    - 不建议提供过多定制样式的能力，不方便迁移
    - 建议使用
  - 服务器接收到mdx文件内容的字符串后，应该如何渲染
    - 使用runtime按需渲染

- mdx编辑器：3种输入模式(参考vditor)
  - 要支持输出html/json/.md文本
    - 注意html和md有第三方的转换工具，要考虑是转换而来还是直接获取输入的文本
  - 输入使用文本编辑器分屏预览SV，不适合做成block editor的形式，输出适合使用.md文本，输出json也容易
  - 输入使用所见即所得编辑器WYSIWYG，非常适合做成block style editor，输出适合使用json而不是.md文本
  - 输入使用即时渲染IR，结合WYSIWYG的实时预览和输入标志文本的shortcut，能够减少鼠标操作
  - ??? block-style WYSIWYG

- 如何在mdx中支持observable javascript(.ojs)
  - 方法1: 直接将字符串写在js变量中，也有人尝试htm tag模版函数
    - 优点：实现简单，方便测试
    - 缺点：字符串不适合复杂代码的自动补全和高亮
  - 方法2: 扩展code block，添加 meta string
    - 优点：书写简单；直接支持语法高亮，执行时仍然是获取并解析字符串
    - 优点2: 普通markdown渲染器能正常渲染代码块
    - 缺点：需要实现自动补全提示等
  - 方法3: 基于react-live，(~~无法~~)提供ojs专门的文本编辑器，执行时仍然是获取并解析字符串
    - 优点：充分利用react-live的预览功能，上面预览，下面代码，与observablehq的体验最接近
    - 缺点：不容易书写；复杂度高、链路长，修改ojs需要执行ojs编译器、rect-live计算、mdx热加载
    - 缺点2: react-live编辑的是react组件，无法直接支持编辑字符串
      - 只能再一次实现类似ojs编译器的转换器，将输入的字符串通过反射封装成函数，自动调用此函数返回输入的字符串ojs

- tips
  - mdx的解析，参考remark-parse, mdxc
  - mdx的渲染基于 mdx/jsx -> react组件 -> dom
  - load
    - build time
    - runtime

- ref
  - [@mdx-js/loader vs @mdx-js/mdx vs @mdx-js/react vs xdm](https://www.npmtrends.com/@mdx-js/loader-vs-@mdx-js/mdx-vs-@mdx-js/react-vs-xdm)
  - @mdx-js/mdx和xdm都依赖 remark-parse、remark-rehype的unified生态，还依赖 vfile、estree-walker
# faq-not-yet

## remark vs markdown-it

- ### [Consider remark for markdown in svelte](https://github.com/pngwn/MDsveX/issues/20)
- The decision to use markdown-it was relatively arbitrary when I put this together initially
  - the performance was okay and there are a decent array of plugins.
  - I've found it pretty annoying over time, however, and have been investigating alternatives.
- marked is the obvious candidate due to its focus on performance
  - but there don't seem to be as many plugins
- remark was my initial preference but I assumed (without any testing whatsoever) that it would be quite a bit slower due to the fact it builds an AST
  - there are a huge array of plugins available and having access to an AST gives a huge amount of flexibility when it is needed.
  - remark will almost definitely have higher memory consumption than a simple lexer/parser with no intermediary AST 
  - but this seems to be a trade-off that people are willing to make. 
  - There is precedent here as MDX uses Remark and no-one seems to mind much, although what is palatable to one community is not necessarily so for another.

## 如何在.mdx文件中动态导入npm仓库中的js库？

- 若只是动态获取和解析mdx，则参考官方提供的@mdx-js/runtime

- 若通过传统的`<script>`，导入的依赖其实会在浏览器中变成全局依赖，挂再到浏览器的`window`上
- 在.mdx文件中书写`import { useTable } from 'react-table'`时，会由webpack处理
- 若在mdx中import没有预先打包进bundle的库，会提示`Component Checkbox was not imported, exported, or provided by MDXProvider as global scope`
  - 需要预先提供到 MDXProvider
  - 或者修改runtime，动态添加新的库

- ### 尝试解决此问题的参考方案
- observable-notebook支持d3.require和import(url)
- https://github.com/hashicorp/next-mdx-remote
  - 支持获取远程mdx文本内容和动态数据
  - The file content must be local.
  - You are bound to filesystem-based routing. 
  - You will end up running into performance issues. 
  - You will be limited in the ways you are able to structure relational data.
- https://github.com/kentcdodds/mdx-bundler
  - 支持获取远程mdx文本内容
  - The problem: You have a string of MDX and various TS/JS files that it uses and you want to get a bundled version of these files to eval in the browser.
  - next-mdx-remote is not a bundler, it's just a compiler. 
  - mdx-bundler is an MDX compiler and bundler.
  - Webpack/rollup/etc also require that all your MDX files are on the local filesystem to work.
  - mdx-bundler can definitely be used at build-time, but it's more powerfully used as a runtime bundler.
  - You might decide to go with a built-time approach (for Gatsby/CRA), but as mentioned, the true power of mdx-bundler comes in the form of on-demand bundling. 
  - So it's best suited for SSR frameworks like Remix/Next.

## [MDX performance](https://github.com/mdx-js/mdx/issues/1152)

- Numerous babel parse and transformation steps
  - Imports and exports
  - Shortcode generation
  - mdxType

- Returning a compiled string that inevitably needs to be transpiled
# docs

## [syntax for mdx](https://github.com/micromark/mdx-state-machine)

- MDX is the combination of Markdown with JSX.
- Markdown is great
  - easy to read
  - most stuff is relatively simple to write
  - It’s loose and ambiguous: it may not work but u won't get an error
  - Markdown is good for content.
- html has drawbacks
  - HTML in Markdown is naive, how it’s parsed sometimes doesn’t make sense
  - HTML is unsafe by default, so it’s sometimes (partially) unsupported
  - HTML and Markdown don’t mix well, resulting in confusing rules such as blank lines or markdown="1" attributes
  - HTML is coupled with browsers, Markdown is useful for other things too
  - Traditionally, Markdown is used to generate HTML, writing markup in Markdown
- JSX is great
  - familiar syntax (like XML)
  - agnostic to semantics and intended for compilers (can have any domain-specific meaning)
  - strict and unambiguous 
  - JSX is good for components.
  - more and more developers have started using JSX to generate HTML markup.
- Why MDX?
  - MDX is not tied to HTML or JavaScript

- Block
  - A block of MDX is an element or expression that is both the first thing on its opening line, and the last thing on its closing line.
  - Expressions can also be blocks
- Span
  - A span of MDX is an element or expression that is not a block: it’s either not the first thing, or the last thing, or both
- Content
  - block element can contain further Markdown blocks, whereas an MDX span element can contain further Markdown spans.
  - Spans cannot contain blocks
  - Blocks will create paragraphs
  - MDX expressions can contain arbitrary data
- Closing MDX
  - MDX elements and expressions must be closed, and what closes them must be in an expected place
  - “closing” tag cannot be put in a different paragraph/block
  - 在`}`之后注意不要写圆点，如`}.`
- Attributes
  - Attribute expressions: `<Component {attribute expression} />`
  - Boolean attributes: `<Component boolean another />`
  - initialized attributes `<Component key="value" other="more" />`
  - Attribute values can also use single quotes
- Names
  - Element names are optional, which is a feature called “fragments” `<>Fragment block</>`
  - The syntax of the name of an element allows dashes `<c-d />`
  - Names can be prefixed with a namespace using a colon or dot `<svg:rect />` `<org.acme.example />`
- Keys
  - Similar to names, keys of attributes also follow the same syntax, dashes allowed
  - namespaces can also be used
  - Methods don’t work for keys
- Whitespace
  - Whitespace is mostly optional, except between two identifiers (such as the name and a key, or between two keys)

### Deviations from Markdown

- MDX adds constructs to Markdown but also prohibits certain normal Markdown constructs.
- HTML
  - Whether block or inline, HTML in Markdown is not supported.
  - Character data, processing instructions, declarations, and comments are not supported at all. 
  - Instead of HTML elements, use JSX elements.
- Indented code
  - Indentation to create code blocks is not supported. 
  - Instead, use fenced code blocks.
- Autolinks
  - Autolinks are not supported. 
  - Instead, use links or references.`[]()`
- Errors
  - Whereas all Markdown is valid, incorrect MDX will crash.

### Deviations from JSX

- MDX removes certain constructs from JSX, because JSX is typically mixed with JavaScript whereas MDX is usable without it.
- Comments
  - JavaScript comments in JSX are not supported.
- Element or fragment attribute values
  - JSX elements or JSX fragments as attribute values are not supported.
- U+003E GREATER THAN (`>`) and U+007D RIGHT CURLY BRACE (`}`) are fine
- Expressions
  - JSX allows valid JavaScript inside expressions. 
  - We support anything in braces.
  - Because JSX parses JavaScript, but we don’t parse JavaScript
  - Brace counting in expressions，表达式中引号内的{}半个花括号也会计数，要求偶数

### Common MDX gotchas

- Markdown first looks for blocks (such as a heading) and only later looks for spans (such as emphasis) in those blocks.
  - This becomes a problem typically in the two cases listed below. 
  - However, as MDX has parse errors, parsing will crash, and an error will be presented.
- Blank lines in JSX spans
- U+003E GREATER THAN (`>`) seen as block quote

## [mdx parser](https://github.com/micromark/mdx-state-machine)

- The MDX state machine is used to tokenize MDX blocks and MDX spans. 
  - Blocks (also known as flow) make up the structure of the document (such as headings), 
  - whereas spans (also known as text or inline) make up the intra-paragraph parts of the flow (such as emphasis).
  - The initial state varies based on whether flow or text is parsed, and is respectively either Before MDX block state or Before MDX span state.
  - The final state is switched to by the MDX adapter, which right before completion will switch to either After MDX block state or After MDX span state.
- The MDX adapter handles tokens from the MDX state machine, which has further effects, such as validating whether they are conforming and figuring out when parsing is done.
  - Adapters are defined to handle a token either when a token enters right before it’s pushed to the stack, or when a token exits right after it’s popped off the stack
- The purpose of the `mdx-state-machine` is to tokenize.
  - The states of the MDX state machine have certain effects, such as that they create tokens in the stack and consume characters. 
  - The stack is used by adapters.
- The purpose of the adapter is to handle the results of the tokenizer.
  - The MDX adapter handles tokens, which has further effects, such as validating whether they are conforming and figuring out when parsing is done.
- To parse MDX is to feed the input character to the state of the state machine, and when not settled, repeat this step.
- How MDX is handled is intentionally undefined and left up to the host parser. 
  - When to feed an EOF is similarly undefined.
  - Host parsers must not support indented code and autolinks, as those conflict with MDX.

## intro

- MDX is an authorable format that lets you seamlessly write JSX in your Markdown documents. 
  - You can import components, such as interactive charts or alerts, and embed them within your content
# ref
- [Markdown 解析原理详解和 Markdown AST 描述](https://ld246.com/article/1587637426085)
  - [Lute 实现后记](https://ld246.com/article/1567062979327)
