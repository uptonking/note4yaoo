---
title: thread-pm-base-office-usage
tags: [office, thread]
created: 2021-01-14T13:17:05.456Z
modified: 2023-03-01T14:10:06.993Z
---

# thread-pm-base-office-usage

# guide

# discuss-builder
- ## 

- ## Webflow 目前在全球拥有超过 350w 的用户，估值达 40 亿美金，有超过 2000 份用户创作的网站模板。_202405
- https://x.com/tuturetom/status/1793859950772650423
- 非常适合用来做创业公司的官网，或者活动的宣发页面
  - Webflow制作前端，Airtable负责后端数据库，甚至连嘉宾提交申请的流程都是自动化。这种生意，只需要Webflow的设计师，加上Airtable的技术专家支持就够了。
- 网站模板本质上就是一种Learn by Example的代码重用软件工程方法吧
- 要拖拉，不一定比code简单
- framer有点要赶超的感觉
- 这个应该是和wordpress+elementor一样的，elementor也是至少百万级用户了。

- https://x.com/bearbig/status/1629437792727203840
- 吐槽下本公司用的Adobe Experience Manager, 难用的一B啊，
- 国内也有类似的无代码设计工具，如zion，更符合国内需求，如能生成小程序等等
- 
- 

- ## 体验了 http://Wegic.ai 的AI建站，UI设计和交互都很惊艳、简洁，整体流程丝滑，很不错的解决了多数低代码、模板库给用户带来的选择困难症、部署困难。
- https://x.com/zQwQs/status/1793216048759754879
  - 看实现像是预定义了少量的组件(可替换文本/图片/动画容器等)，然后让AI生成页面区块，写React组件(Hero/Gallery等)和props，用AI对话去编辑

# discuss
- ## 

- ## 

- ## 

- ## 

- ## Use these CHAR functions to add context to your spreadsheets
- https://twitter.com/benlcollins/status/1395091986626056211
  - google sheets的单元格支持显示符号类字符串
  - CHAR(8594) produces the right arrow. ➡️
  - CHAR(8595) produces a down arrow. ⬇️

- ## This looks like the future of documentation
- https://twitter.com/rauchg/status/1367199228494155786
  - https://code-hike-scrollycoding-preview.vercel.app/posts/lorem-ipsum-three
- Have you seen the Stripe docs lately?
  - https://stripe.com/docs/checkout/integration-builder
  - It's even got selectable options for languages and frameworks at the top, along with Choose Your Own Adventure bits at the bottom if you want to keep customizing. It's really phenomenal documentation.

- ## Despite all its warts, MDX is a gamechanger for writing documentation and technical content. 
- https://twitter.com/dan_abramov/status/1364652922055835648
  - It removes the friction between the desire to add a bit of interactivity, and actually doing it in a way that surpasses your original intent. 
  - I can’t imagine going back to plain Markdown.
  - Unlike with a traditional CMS-backed writing, I don’t need a vendor to tell me what kind of blocks I’m allowed to use. I want to make my own in a few minutes.
  - My biggest problem with MDX is complexity of the stack. Hoping Server Components can simplify it in the long term.
- This uses a fresh new fork of MDX: xdm

- ## Live Edit "playground" type component using @Alpine_JS and some @tailwindcss
- https://twitter.com/kevinbatdorf/status/1287783480567271429
  - it's almost like codepen-ception
- [codepen demo](https://codepen.io/KevinBatdorf/pen/rNxbbaJ)

- ## Excited by @swyx‘s React SFC piece, which fuses the new @redwoodjs “cells” and @storybookjs Component Story Format (CSF).
- https://twitter.com/mshilman/status/1237789461166977029
  - Perfect timing as we put the first features of CSF 2.0 in place!
- The gist is we want to export data objects (props) and have Storybook automatically render a story for each data export. 
  - That way you can focus on writing the data instead of the render function.
- CSF 2.0. That’s the long view. 
  - More immediately in SB6.0: auto-generated docs/controls/actions etc for your stories/“cells” with a natural, portable syntax.

- ## I think having a storybook/component library alongside the main app is a good idea, but it needs to use the exact same toolchain.
- https://twitter.com/swyx/status/1246316914306977792
- Tools like Jest and Storybook are great for how flexible and featureful they are, 
  - but I feel like this trend of everything having its own webpack config that can't be shared with other tools just makes the configuration way more complex.
  - webpack 5 solves this lol ??
- I’ve experienced the same pain with adding Storybook to a Gatsby project. 
  - Not sure about your setup but for me Storybook needed all the same providers, TypeScript loaders etc that were part of the build setup for the Gatsby site. 
  - Storybook is its only build if that makes sense
- developers from ant design have had blamed the idea of storybook is awesome, but in practice they still have to deal with some sharp edges. 
  - Instead of storybook adoption, they just developed their own storybook, or doc toolchain for UI components.
- If only we had a native module system and components model for the browser.

- ## @storybookjs decision to introduce Component Story Format was a genius move
- https://twitter.com/aarongarciah/status/1286223740058185729
  - Opened the door to have a simpler (and beautiful) API
  - Portable code since it's plain JS modules, reuse it in other testing frameworks!
  - Simpler story looks like this in SB 6 (RC)
- By introducing CSF, @storybookjs had the ability to add new amazing stuff
  - csf enabled args
  - args enabled auto-generated controls/actions
- I love that note about Portable code. 
  - importing and using the stories for the various states you want to test has been such a huge win. 
  - Test fails? Instead of `debug` or whatever, run through the same steps in storybook.

- ## Storybook 5.3 is here. Write stories & docs in MDX
- https://twitter.com/GHengeveld/status/1217152300130717696
- Use CSF. Optionally add MDX for docs pages where necessary (typically intro pages and longer written docs). 
  - It depends on what your component users need. 
  - Comprehensive design systems often have more written docs, while component libraries have very little (and that's fine).
- Best bet is to do CSF always and import those into any MDX files. That way you have both. 
  - Remember that most tools don't support MDX. 
  - CSF is so simple by design, to enable integrations with other tools. MDX isn't really reusable.

- ## We definitely plan on supporting web components natively in MDX
- https://twitter.com/4lpine/status/1253075231620526085
  - however it won't be a focus in the near future.
  - That said, you can wrap up web components with React to render web components in MDX today.
- [Web components + React + MDX codesandbox](https://github.com/mdx-js/mdx/tree/master/examples/react-web-components)

- ## Stoxy is something I've been working on lately
- https://twitter.com/jaredcwhite/status/1323321554093006848
  - I'm trying to come up with a nice way to handle mutable data like translations and session data with the DX of Web Components.
- Maybe the interpolated values inside text could use a familiar syntax like `{{ key.value }}`

- I was considering using some kind of a templating syntax, 
  - but a big motivator here was to make the markdown as clean and fluent to write as possible, so I opted out of it
  - I might reconsider it at some point though! 
  - With the prefix you could make your own templating tho
- I wish all the folks getting excited about MDX etc would come to realize that writing Markdown with embedded web components is…Markdown. 
  - Because it's just HTML

- ## By the way, you know MDX, where you transpile markdown in such a way it can include JSX components? 
- https://twitter.com/heydonworks/status/1297443487701520389
  - You can do this with web components without any transpilation because they are HTML, and Markdown allows HTML.
- markdown -> html is still compilation/transpilation
- You don't have any bundling, compiling, or minification of javascript at all, while using web components, and while compiling your content from markdown to markup?
- Retweet this when web components are accessible.
  - MDX can be compiled down to pure HTML, that is more likely to be accessible than a web component (that also requires runtime Javascript to load) . I'm sorry, but web components are mostly trash.
- Markdown always requires some processing (be it server or client side) as it's not html
  - Also separating usage and import can be confusing. it works but where/how my-component is defined?
  - 因为react组件需要显式import，而web-comp可直接写标签，查找声明定义就不方便

    - 这也是字符串相对于js变量的缺点

- 

- ## One thing I really really dislike about mdx is that it’s completely unreadable on github.
- https://twitter.com/jxnblk/status/1046921094295429121
- If user-generated web components *could* render on gitHub.com, wouldn't that be a huge security issue?? 
  - I guess generally I wouldn't recommend MDX as a replacement for MD on GitHub, but would be cool if GFM were more extensible somehow
- Before MDX, we had a rough spec that was fully backwards compatible with standard markdown (which is still possible with MDX and fenced code blocks), 
  - but I think opting into the more custom MDX spec sometimes is useful
  - I think the authoring mindset of markdown puts code blocks secondary, and the mindset of MDX puts components and markdown at equal footing
  - but it doesn’t mean we can’t dream about it

    - Why dream when you can embed CodeSandboxes all over the place?

- ## Web components might be great in 5 years, but it's simply too early to adopt them today. Too many major issues.
- https://twitter.com/justinfagnani/status/1198378310356520962
- One of the many reasons cited by WC advocates is usually about "reducing JS framework bloat". 
  - But if you used only the actual native APIs, it would be like writing an app with raw DOM. 
  - Polymer/lit-element is still a framework just like React/Vue.
- Polymer and LitElement are absolutely, in no way, frameworks.
  - They do not define their own component model, and do not invoke the lifecycle callbacks: the browser does that.
  - You don't create components with LitElement: you create them with document.createElement(), etc
  - In React, React defines the component model.

    -  It creates the components. 
    -  It can't create components from other frameworks.

  - With WCs, the spec defines the component model, browsers implement it. The browser creates components. You can mix and match
  - The documentation for how you instantiate a LitElement is the same as for Polymer or Stencil: document.createElement(), innerHTML, etc. 

    - You can switch the implementation of a component to vanilla, or another base class. 
    - These things are not possible with frameworks.

- For a concrete example of how this ripples out into various facets of web dev, see regular Markdown vs MDX.
  - Markdown supports HTML, so it already supports web components.
  - Web components don't require that we re-invent things to play nicely with them.

- ## I'm so glad I used MDX for my blog. 
- https://twitter.com/JoshWComeau/status/1243136771652751360
  - It enables things that otherwise would not be possible with Markdown or a CMS, while still being a consumable data source (unlike having the posts be all-JSX)
  - For tangential(离题的，不相关的) information, I have a `Sidenote` component.
  - For code snippets, I built a little playground component on top of react-live.
  - I use "video GIFs", similar to social media platforms. 
  - Important addendum: MDX is a wonderful tool for developer blogs, but it sucks for non-developers. 
- Not saying mdx isn't powerful, but CMS with good structured content can achieve it too
- Because HTML is valid Markdown. I like using Web Components to do the same thing
  - This way I get to have all my custom interactive components in plain .md files without the weight of React. 
  - No JSX or MDX required. 
  - It even feels familiar to React devs using lit-html + haunted.

- ## Unpopular opinion: MDX isn't suitable for anything other than one-column block content.
- https://twitter.com/hasparus/status/1350227713211166727
- My point is, if you craft a good environment to write slides in React with close to same effort as you do in MDX, you'd notice you don't take much advantage from MDX really.
- I’d rather write Markdown and then add interactive elements instead of authoring in JSX.
  - Especially since my notes are in Markdown already.
  - However, slide decks could be classified as "one column block content" — That’s what you get when you print them / remove presentation logic.

- ## After 6 years of writing in markdown, I've finally mastered the basic markdown table syntax
- I was recently exposed to AsciiDoc table syntax.  It’s…exotic.
- this is why I use HTML for everything. I already know it!

- ## No matter how many times I've written a markdown table, I still have to look it up literally *every* time
- https://twitter.com/Una/status/816511597355077632
- I see it as a failing of HTML that we can't just write `<table src=data.csv></table>` natively.
- no idea what editor you use, 
  - but if it's @code, use markdown-shortcuts ext <-- Tables, fenced codeblocks, nested lists, oh my.
- Save yourself the trouble! I found `csvtomd` on GitHub
  - Never used tablesgenerator ever since.

- ## Read file from local directory in Javascript
- https://stackoverflow.com/questions/19842314/read-file-from-local-directory-in-javascript
- as far as I know this is not possible in JavaScript due to security concerns.
  - If it were, a web page could grab any file on your file system without your consent or without you knowing.
  - A user must be given the option to choose a file from their file system knowingly.
- This is not really possible or recommended for security reasons.
  - If this is only being used on your personal computer or for testing reasons, you can add an option for your browser to allow file access, 
  - `--allow-file-access-from-files`

- It is not possible to access the users file system.
  - However with the `FileSystem` API you can get a temporary or persistent private file system where you can store stuff for you application (cached images for example). 
  - You can then combine this API with the `File` API to allow the user to drag and drop files to your application from the users files.

- ## Do not use FileReader to show local file during uploading it to the server. 
- https://twitter.com/sitnikcode/status/1060157747038208000
- FileReader will copy the whole file to JS memory as a string.
- Use `URL.createObjectURL()` . 
  - It will return short blob: URL with a link, which you can use in `<img>` .

- ## For self-publishing eBooks from Markdown - are there nice alternatives to using a complex LeX toolchain?
- https://twitter.com/alexellisuk/status/1349693214782074882
  - `MD <> LeX <> PDF` is a complicated toolchain with native components and comes out like an academic paper.
- Pandoc is quite popular for this. It can generate pdf, and epub/mobi files as well
  - It's also a huge pain when exporting to PDF with needing LaTeX plugins and lots of native tools.
- If just starting, you could check out AsciiDoc. 
  - Similar-ish to Markdown but has nice support for exporting to PDF, EPUB, MOBI, etc.
  - I'm pretty fluent in markdown - what toolchain do you use to get the AsciiDoc to PDF? And how good is it for eBooks?

    - I used AsciiDoc and pandoc. Worked pretty well, but O'Reilly took care of all the formatting etc. Pandoc also handles markdown.

  - I have been using Pandoc, which is where all the issues are because the MD to PDF uses Lex to convert/generate. Did you ever do any local preview/generation?

    - Sometimes, but to get it to look right I had to run it through the O'Reilly webapp. I assumed with the right templates I could local generation to look as good.

- Ugh, that's exactly the problem I've been having lately. 
  - I resorted to just paying for Leanpub Premium for now. 
  - I write everything in Markdown, then just add the Markua extensions on top. 
  - Leanpub does all the heavy-lifting across PDF, ePub and mobi
  - The added benefit of the Premium option is that I can keep pushing changes to a GitHub repo, and LP will automatically generate unlimited previews each time.

- ## I'd want to be able to read the file's meta, and be able to find all .mp3 files on my PC
- https://twitter.com/trevorblades/status/1155144570251780096
- You might need to implement some kind of file upload mechanism to handle local files on your PC. 
  - Howler accepts base64 data URIs
  - so you could use a file input and handle the uploaded file using the FileReader API
