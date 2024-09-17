---
title: lib-editor-codemirror-community
tags: [code-editor, codemirror, community]
created: 2023-01-29T10:52:26.160Z
modified: 2023-01-29T10:52:44.183Z
---

# lib-editor-codemirror-community

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 🆚 [Difference between state field and facet? - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/difference-between-state-field-and-facet/3650)
- How do you update the facet’s content? The way these are designed, fields are useful for independent bits of state, and facets are more applicable for derived state and inter-module communication.

- ## [Expose API for browser extensions - v6 - discuss. CodeMirror _202303](https://discuss.codemirror.net/t/expose-api-for-browser-extensions/5864)
  - Browser extensions that act on editable content, such as Grammarly or LanguageTool, currently cannot fully work on CodeMirror 6 because of viewporting. 
  - Would you be open to exposing some kind of (possibly read-only) API for such extensions? Specifically, as a minimum, some way of obtaining the full editable document text from a CM6 editor root DOM node
  - Being able to add something like an `updateListener` would also be useful.

- I feel browser extensions that insert themselves into the page’s script are fundamentally incompatible with the kind of closed-world model that page authors need to actually write reliable software
  - I can imagine browsers eventually supporting some kind of interface for this kind of editing helper, or even something being standardized in JavaScript, in a way that is well-defined and that page scripts can work with. But until that exists, I don’t really want to encourage the invasive monkey-patching that these extensions are doing.

- 202303: In the case of Grammarly, I’m not sure whether you’re aware that its approach changed fundamentally around a year ago. The short version is that its decorations are now drawn in a separate layer outside the editor content, and it doesn’t touch the content itself. It already works reasonably well with CM6, but without access to the full document text, it can’t, for example, provide an accurate number of how many suggestions it wants to give you. It also doesn’t pick up viewport changes accurately, which it would be better able to do with access to an update listener.

- ## [Listen to text changes of an existing state/view - v6 - discuss. CodeMirror _202303](https://discuss.codemirror.net/t/listen-to-text-changes-of-an-existing-state-view/5952)
  - Is there a way to attach a listener to an existing item on the page? I need to do this from an extension so I want to make sure I don’t break the 3rd-party editor by recreating the whole state.

- There is a way to attach extensions, but for that you do need StateEffect.appendConfig 

- ## 👷 In his #BOBkonf2023 talk "State Transitions in Complex Systems", @MarijnJH shows how CodeMirror uses persistent state values & first-class transactions to more easily keep all the interdependent data involved in a full-featured editor coherent.
- https://x.com/BOBKonf/status/1613845939361398784
  - [BOB - State Transitions in Complex Systems](https://bobkonf.de/2023/haverbeke.html)

- ## 💡 给一段代码，自动检测编程语言，了解到了以下几个方案：
- https://x.com/wsygc/status/1761928319111684431
  - 1. 微软出品的 https://github.com/microsoft/vscode-languagedetection 似乎vscode就是用的这个包，基于机器学习，给出概率列表，但是只支持nodejs运行时，无法在浏览器运行，而且在nextjs API route里也跑不通，暂时不考虑。
  - 2. Github在使用的 https://github.com/github-linguist/linguist  这个主要用于分析Github Repo代码组成，和Github生态绑定比较深，而且使用的是Python，不太符合我的技术栈和小需求
  - 3. Google的 https://github.com/google/magika （ @hi_yggd 推荐）和微软那个类似，也是基于机器深度学习，给出概率性列表，试了试web demo（https://google.github.io/magika/），准确率还行，支持浏览器运行（https://npmjs.com/package/magika），挺符合我的小需求，唯一有点犹豫的是Google出品，而且处于实验品阶段
  - 4. highlight.js的自带API https://highlightjs.readthedocs.io/en/latest/api.html#highlightauto 这个是自己找的，算是目前为止符合需求的最轻量级的解决方式了，不过准确度如何，有待实践验证
  - 5. 最后一种方式是一个思路（ @KunhaiY 推荐）：扔给AI，直接让它给出答案。至于prompt怎么写，宝玉老师（ @dotey ）推荐让GPT-4给prompt，是个比较新颖的解决方案，效果如何，有待探索验证。
  - 综上，我准备先试试hightlight.js API，这个验证起来最快，效果不太满意的话，再试试google的magika，如果还是不满意，再走AI思路
- 我记得 codemirror v6 是有自动检测编程语言这个功能的。大致原理通过关键字判断。

# discuss-codemirror-🆚️-monaco
- resources
  - [Comparison of JavaScript-based source code editors - Wikipedia](https://en.wikipedia.org/wiki/Comparison_of_JavaScript-based_source_code_editors)

- ## 

- ## For Livebook, we use CodeMirror plus phx-hook, and then use LiveView's push/reply events to exchange the relevant information. It works like a charm
- https://x.com/josevalim/status/1834265447769809225
- Did livebook use to use monaco, or am I getting that wrong? If so, why the switch?
  - Yes, we were used to. I'd need to dig up in the issues tracker the reasons but CodeMirror is quite more lightweight.

- ## why didn't Svelte include Monaco editor into the playground like Vue did. _202406
- https://x.com/Rich_Harris/status/1801212903552401428
  - This way you can run TS worker and have similar to VSCode editing experience with typescript enabled
- We prefer CodeMirror to Monaco - it's smaller, more accessible, more extensible and works on mobile devices. But you don't get as much stuff 'for free' out of the box

- ## We spent two weeks exploring whether a lightweight IDE (using VSCode or  Eclipse Theia) would meet our requirements, 
- https://x.com/NyahMacklinDev/status/1642302520444739587
- Monaco and CodeMirror 6 are both browser-only solutions, without  infrastructure requirements or much user interface out of the box. These  solutions allow for the most customization, which was something the team found appealing.

- ## What code editor would you use for your site? Monaco, CodeMirror, PrismJS, or something else? 
- https://x.com/meijer_s/status/1726978119947694527
  - Not just syntax highlighting, editing with suggestions.
- Haha as someone who has used a ton of v5 and a now exclusively v6, facets are your friend! Feels way more composable.
- If you want a powerful editor with support for completion, hover, navigation, formatting, basically everything VS Code supports, I recommend Monaco. I also strongly recommend monaco-editor over some wrapper library. But Monaco is quite a heavy dependency

- ## [Spike(尖钉；尖刺): Investigate CodeMirror as a replacement for Monaco · GitLab.org/GitLab _202301](https://gitlab.com/gitlab-org/gitlab/-/issues/387586)
- Monaco has served us well as a foundation for the Source Editor for the past couple of years. But some changes to our overall tech stack and the direction of our other categories warrant re-visiting the underlying editor for Source Editor.
  - Monaco continues to lack basic support for touchscreen devices. 
  - The Content Editor is maturing and the underlying combination of Tiptap and ProseMirror is proving to be a viable foundation for future development. We are looking to increase the usage of Content Editor in 2023 and it's possible that adopting CodeMirror could simplify the transition between the two editors in places where they co-exist.
  - The Web IDE Beta has moved away from Monaco in favor of a custom fork of VS Code. Without the need for the Source Editor to power this more demanding area of the product, we should re-consider what it needs to do everywhere else and determine which platform best meets our needs.

- considering the PoC for consolidating SE and CE (video), I think the value and urgency of this issue should be lowered. We can get to it eventually, but it should not be seen as a helper or blocker for x-editors' communication.
  - 100% agreed. I only see mobile support as a key differentiator and that may actually be in a better place than we assumed.

- ## 🆚️ [sourcegraph: Migrating from Monaco Editor to CodeMirror _202210](https://sourcegraph.com/blog/migrating-monaco-codemirror)
  - 主要考虑可定制性、体积

- We recently migrated Sourcegraph.com away from Monaco, the code editor component that powers VS Code, to CodeMirror. 
- TL; DR
  - Monaco gives you a lot out of the box, but it’s pretty hard to configure or trim down on features you don’t need.
  - Monaco’s documentation is not great, so we couldn’t always figure out if it was possible to make it do what we needed.
  - Monaco has a global reference model, which makes it tricky to run several instances of it on the same page with small configuration differences.
  - In terms of code size, Monaco accounted for a whopping 40% of our external dependencies.
  - CodeMirror has already been adopted by other large projects such as Replit and Chrome’s developer tools, indicating that it isn’t going to disappear any time soon.
- We’re still getting to know CodeMirror, but so far it has solved all of the above problems and has been delightful to use. It’s been the default component for our search input since May 2022, and we’ll be using it for a lot more in future releases of Sourcegraph

- Although similar, in many ways CodeMirror turned out to be the exact opposite of Monaco. 
  - Monaco gives you a full IDE by default. This includes a multi-line editor, and a code “minimap”
  - CodeMirror is more minimalist and modular. You don’t get as much by default, but you can build exactly what you want by adding and configuring various components. 

- The problems we had with Monaco and how CodeMirror fixed them
- Size: Monaco pushed the amount of JavaScript code that we download on our search page to 6MB.
- Single-line editor: Unlike most IDEs, our search input is a single-line input… most of the time.
- CSS integration: To customize the look of Monaco, we had to hard-code hex color codes into our JavaScript instead of being able to use our site-wide CSS classes and variables.
- Global configuration: It’s tricky to render several Monaco instances per page, each with a slightly different configuration.
- Placeholder text: There has been a long-standing open issue with Monaco requesting a feature to enable a placeholder or default value.
- Code cleanliness: We had some nasty hacks to make Monaco do what we wanted it to.

- We can do a lot more with CodeMirror
- Rewriting our file viewer using CodeMirror
  - For historical reasons, we weren’t using any code editor for this file-view functionality. It’s a read-only view
  - we do need a lot of the same functionality when displaying files, including syntax highlighting, line numbers, and code navigation.
  - Another advantage of using a code editor for a file viewer is apparent when viewing large files. When opening a file with thousands or millions of lines, a code editor like CodeMirror won’t load and render an entire file. Instead, it intelligently only renders what’s on the user’s screen.

- ## 🆚️📝 [Ace, CodeMirror, and Monaco: A Comparison of the Code Editors You Use in the Browser __202112](https://blog.replit.com/code-editors)

- [「译」Ace，CodeMirror 和 Monaco：Web 代码编辑器的对比 - Xheldon Blog](https://www.xheldon.com/tech/a-comparison-of-code-editor.html)

- I’ve been working on Replit for roughly six years now, and as the team has grown, I’ve focused on the IDE (what we call the workspace) portion of the product. 
  - Naturally, I was increasingly preoccupied with the code editor. 
  - While we’ve considered creating a code editor that meets our needs, the complexity involved in developing one, the richness of open-source choices available, and the size of our staff made it a fruitless rabbit hole to enter. Our time is best spent elsewhere.
  - I have had the pleasure (and the pain) of using Ace, Monaco, and CodeMirror in production
- In the early days of Replit, around 2011, there was no code editor. It was a pure REPL interface, a console with a simple input box. 
  - Code editors give us features like syntax highlighting, editor shortcuts, auto-indentation, search and replace, etc. 
  - Cloud9 released Ace at the time as a feature-full, performant web code editor. 
- 🎯 We used Ace until around late 2017 when we switched to Monaco. 
  - While Ace was still being maintained, only one person was working on it. After Amazon acquired Cloud9, it appeared as though they deprioritized the open-source project.
  - The editor was not receiving as many updates, issues were racking up on GitHub, and the maintainers added almost no features.
- Monaco is the editor that powers VSCode; 
  - If we switch to Monaco, we thought we’d be able to get all the cool updates and features from the good folks working on VSCode.
  - Switching came at a cost, it was missing a lot of Ace’s features, but we were confident that it would surpass Ace in no time with the community’s excitement and contributions
  - The first issue was that there were a lot of languages modes missing from Monaco
  - Another problem with Monaco was the build tooling. I had to precompile Monaco as a Webpack DLL and add many Webpack configurations to make it work.
- 🎯 Unfortunately, Monaco also didn’t have an easy way to lazy-load modules and do code-splitting, so it was tough to get small bundle sizes. It added a whopping 5 megabytes (uncompressed) to our workspace bundle, and that’s not something we take lightly.
  - Monaco also doesn’t work well on mobile. 
  - we wound up with two code editors on Replit: one for desktop computers and one for mobile. Every new feature had to be ported over to Ace (mobile). We had to write a language client for Ace for LSP features, and we had to write an operational transformation adapter for Ace to support multiplayer, and so on.
- 🎯 In late 2018 Marijn announced a rewrite for CodeMirror to modernize the editor, CodeMirror version 6 with an excellent design doc. 
  - **One of the primary motivators for the rewrite was adding support for touch devices**. 
  - CodeMirror would achieve that by leaning on native browser text editing (via contentEditable) rather than implementing text editing entirely in the library/javascript.
  - ProseMirror inspired CodeMirror 6’s API design
  - we started to adopt CodeMirror incrementally. We first added it as the defacto read-only editor on Replit, then started adding it to different parts of the website where the code gets edited.

- 🆚️ 比较项目
  - Stability
  - Out of the box experience
  - Modularity, bundling, and footprint
  - Extensibility and advanced features
  - Community and documentation.
  - Performance
  - Mobile support

- If you want a code editor that supports mobile, you should use CodeMirror 6. 
  - Ace has not-bad support but does not come close, and Monaco is unusable on mobile.
  - I'd go as far as saying that CodeMirror is probably suitable even for native applications as a `webview` component. 
  - Most things in CodeMirror are serializable so you can interop with the webview from your native code.

- ## 👥 [Ace, CodeMirror, and Monaco: A comparison of browser code editors (2021) | Hacker News _202203](https://news.ycombinator.com/item?id=30673759)
- CodeMirror improved Replit's performance by a lot and by extension our retention. In fact, after releasing it to mobile in July our weekly retention rate on mobile increased by a whopping 70%. 
- CodeMirror has a brilliant story for realtime collaborative editing. You have two options: OT vs YJS
  - We had to handroll our own OT implementation inhouse (based on https://github.com/ottypes/text-unicode) since we had built the system for it already. I suspect we would've used or forked CodeMirror's collab package if we were starting today.
- The article calls CodeMirror "lightweight" but the minified JS is still over 1 MB. If you want lightweight then you probably want something like CodeJar (https://github.com/antonmedv/codejar) which clocks in at 2 kB.

- The killer app for cloud IDEs is honestly going to be something GitHub code navigation. Imagine being able to do PRs with click to definition, find all references, etc., without having to pull in the changes locally. It's also great even right now for reading open source projects when you are trying to understand how something works.
  - They are great for viewing code, but I'm not convinced they are good for writing code.
- The closest is to press ".", or change url from github.com to github.dev. That opens up the github repo in a VScode/Monaco editor

- Cloud IDEs are the modern version of using X Windows or RDP/VNC sessions, that is the problem that they solve.

- Mobile support means that CodeMirror 6 is often the only option. I think it's a bit of a waste to start of project with Ace or Monaco, knowing that it will never work in mobile.
  - Ace is not perfect on mobile, but it works to some extent.

- Monaco uses it's own build system that requires a lot of configuration twiddling to get it to work. Powerful, but it's first and foremost built for VSCode.

- Any thoughts on Code Server? It’s vs code in a browser, I’ve been used it for one year now and it’s great. But maybe it’s outside the scope of the article?
  - It's using monaco as the underlying editor, just like VS Code that it's based on. Code Server basically takes the VS Code codebase as is and just adds a very light server layer to do auth and static content serving. All of the frontend javascript code, etc. is the same as the desktop version of VS Code.
# discuss
- ## 

- ## 

- ## 

- ## [SyntaxNode not exported by @lezer/common - Lezer - discuss. CodeMirror](https://discuss.codemirror.net/t/syntaxnode-not-exported-by-lezer-common/7600)
- This is a type (interface) export. You can import it in TypeScript, but not regular JavaScript.

- ## [Read-only Facets? - discuss. CodeMirror](https://discuss.codemirror.net/t/read-only-facets/7175)
- Perhaps like a wrapper class
- Regarding computed values, given that defining an extra facet for them already allows you to do that, I don’t think that really warrants another library feature.
  - Introduce `FacetReader`

- ## 🔀 [Should dispatched transactions be added to a queue? - v6 _202206](https://discuss.codemirror.net/t/should-dispatched-transactions-be-added-to-a-queue/4610)
- I was slightly surprised to find that the dispatch method doesn’t put transactions on a queue for processing.
  - While it would be easy enough to add a queue in a custom dispatch function, I’m wondering whether that would be a bad idea for any reason, particularly in a way that explains why it isn’t implemented as a queue by default.

- When creating a transaction, you are basing it on the current editor state. It would often not make any sense anymore when applied from a different state. Also dispatching transactions is synchronous, so a queue seems needless complexity.

- Would it not be correct to say that whenever something asynchronous happens which ends with a call to view.dispatch, there’s always a chance that the view will already be processing an update at that time, which would result in an error being thrown?
  - The way to write asynchronous stuff that dispatches is to do the async action, and then figure out how it applies to the current state. This may in some cases involve mapping a position known at the start of the action forward through updates (which is why it is convenient to define this kind of stuff as a view plugin).

- Ok, I think I see the flaw in my reasoning - thanks for helping to work through it. It’s because the transaction processing is synchronous, any asynchronous code which calls view.dispatch will be run from the microtask queue and can only happen once the current transaction processing has finished.
  - In which case it’s only calls to view.dispatch that are triggered by updates within a CodeMirror cycle that we need to worry about, and these can be wrapped in setTimeout (or, perhaps, queueMicrotask).

- ## today @ValDotTown got its own little code-writing ai-assistant _202406
- https://x.com/tmcw/status/1803132938269175956
  - we built this from scratch using a novel backpropagation algorithm combined with a new concept similar to attention that supports large context windows

- the very first user request for improvement was to stream the openai answers, which will cause this whole nice form/request/response/model to fall apart(破碎; 破裂; 解体; 崩溃)

- ## In CM, there are two ways to decorate a piece or text: _20240422
- https://x.com/antiflasher/status/1782079526740062328
  1. Apply some style to the piece;
  2. Replace the piece with a composed span (widget).
  - I want the backticks to disappear when the style gets applied
  - Сombine them together! I apply Decoration.mark() first, then replace backtick signs with placeholders—a zero-width span.
  - [CodeMirror Code Tokens - Combined Decoration Improved](https://codepen.io/Anton-Lovchikov/full/ExJOBKp)

- ## how do y'all like the new val share images?
- https://x.com/tmcw/status/1782842681267232926
  - we were running our codemirror language mode headlessly and turned that into the very particular subset of html that satori supports, then to svg to png

- ## Hey @discord what do you use for syntax highlighting codefences? _202406
- https://x.com/nullvoxpopuli/status/1801288055334027417
  - in the @emberjs server, we use gjs and gts extensions / tags, and the language is supported on GitHub, but it just shows up as un-highlighted.
- Monaco and VSCode typically use different highlighters. Though that’s probably not applicable to Discord.

- ## 💡 [Nested editors, kind of. - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/nested-editors-kind-of/4654)
- This should be possible (if somewhat messy) using a technique similar to the split view example. 
  - But you’ll have to offset your change sets by the current position of the sub-document when forwarding them between the cell editors and the main editor (which should be possible by iterating over them with iterChanges and building up a new changeset with the same insertions but offset position).

- ## 🆚️ [Implementing WYSIWYG Markdown editor in CodeMirror - discuss. CodeMirror _202005](https://discuss.codemirror.net/t/implementing-wysiwyg-markdown-editor-in-codemirror/2403)
- Do you think using ProseMirror would be better than hacking CodeMirror to accomplish the same thing?
  - Probably. It’ll definitely involve less fighting against the library.

- I dug into ProseMirror some more and felt like ProseMirror is a better choice for something like this, especially with `NodeView` for editing math and code blocks. By storing the markup in Marks expanding/folding should also be doable.

- ## [Inline Codemirror inside Prosemirror? - discuss. CodeMirror _202311](https://discuss.codemirror.net/t/inline-codemirror-inside-prosemirror/7396)
- Yes, it is, there’s even an example like that on the ProseMirror website.

- But I was thinking as an inline node, meaning instead of being a full width div, it just expands as the user types.
  - no, CodeMirror assumes it is a block element, so for this you’d have to wrap it in some kind of `inline-block` container and add a kludge that constantly resizes it to match its content size. It won’t work as a regular content-fitting inline element.

- ## [Synchronising CodeMirror 6 and ProseMirror _202310](https://discuss.codemirror.net/t/synchronising-codemirror-6-and-prosemirror/7339)
- Could you offer any advice on how to translate between the CodeMirror and ProseMirror transactions please?
  - Not really. The way you map between rich text and plain text documents is going to involve some kind of translation, I guess, depending on the text format and ProseMirror schema used. You say nothing about how you’re doing that, but I suspect it involves some kind of parsing. Mapping changes in such a context, and especially translating text changes to structured ProseMirror steps is likely going to be non-trivial. It may be easier to compute a diff of some kind and work from that.

- ## 💡 [Switch from Monaco to CodeMirror and generate AST from Lezer tree _202208](https://discuss.codemirror.net/t/switch-from-monaco-to-codemirror-and-generate-ast-from-lezer-tree/4946)
  - It seems to me that using Lezer as the parser for CodeMirror is a better option than reusing the Chevrotain parser. I wonder if I should now get rid of the Chevrotain parser completely and generate the AST tree from the Lezer tree? 
- That depends. Lezer does not emit an abstract syntax tree, just a set of nodes with types and parent/child relations. So using that for analysis is definitely possible, but more awkward than what you’d get from a regular parser—you have to iterate through child nodes finding the one you’re interested in, and get the name of variables by reading the start/end position of the corresponding node from the document, and so on.

- Is there a way to serialize and deserialize a Lezer tree (to send it to a worker)?
  - No, that currently doesn’t exist. There’s Tree.build 25 to deserialize from the arrays the parser builds up, but no corresponding serialization function. Also, since these are constantly being updated and share structure with previous trees, you’d probably want something more intelligent than full serialization/deserialization (such as tagging subtrees with IDs using WeakMap so that you can reuse them on the other side when they have already been moved to the worker).

- ## [Custom cursor like in Monaco Editor - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/custom-cursor-like-in-monaco-editor/5705)
- Your styles are probably not specific enough to override our shabby default styling. Add a parent selector like `.cm-editor` in front of them, maybe.

- ## [Markdown emoji previewing - v6 _202210](https://discuss.codemirror.net/t/markdown-emoji-previewing/5186/9)
- Yes that can be implemented via “replacing decorations”, see Example: Decorations 

- ## [Anyone Explored a Codemirror 6 Canvas/WebGL Renderer? - discuss. CodeMirror](https://discuss.codemirror.net/t/anyone-explored-a-codemirror-6-canvas-webgl-renderer/3779)
- The Bespin 9 project in 2009 worked this way, but was given up due to, I believe, problems with the approach. Some things to keep in mind:
  - In most situations, for text layout, the DOM will be faster than a canvas
  - Accessibility will be terrible if your text is just pixels on a canvas
  - Doing text positioning, styling, and wrapping is a whole lot more difficult with fillText

- I haven’t worked with WebVR—seems like there’s a proposed 8 standard for making it capable of showing regular DOM elements, but nothing actually implemented at the time. I guess as a workaround for that limitation, mirroring a CM instance to a canvas is a more or less reasonable thing to do.

- ## 🆚️ [v6 Comparison with approach of react-simple-code-editor _201907](https://github.com/codemirror/dev/issues/109)
- react-simple-code-editor: works by allowing users to edit inside a native `textarea` , while overlaying syntax-highlighted code on top of it. On the face of it this seems like quite an elegant and simple approach that works well.

- I find myself wondering what makes the more complex approach taken by CodeMirror superior to that approach, which seems so simple by comparison.
- I can only think of the following drawbacks to the approach taken by react-simple-code-editor:
  - Syntax highlight requires a complete parse on each keystroke. This could be addressed by using `tree-sitter` or `lezer` for maintaining the AST.
  - The syntax-highlighted DOM tree is clobbered and regenerated on each keystroke. This could be addressed by using virtual DOM to update the DOM based on the fresh AST (e.g. using preact or react).
  - Really large files would render in full with this approach, whereas CodeMirror only renders what's visible.
- The above problems can be ignored for use cases where the files will not be large, or syntax highlighting is not required when the amount of text is above a certain threshold.
  - I'm posting this issue as a sanity check, to see if I'm missing some important points that make the complex update patterns within CodeMirror inherently a better choice than the approach taken by react-simple-code-editor. 

- This isn't a new idea—it was also the approach used by Editarea, the only halfway serious predecessor of CodeMirror.
  - Can't use anything but single-font single-style text inside the editor or the characters get misaligned.
  - Reading from a textarea is all-or-nothing, so when the document is big, even if you manage to do incremental highlighting, you have to read the entire string and then diff it against the previous value, which is expensive. (Have you tried pasting a big document into their demo? It becomes unusable.)
- In short, most of the features that CodeMirror provides couldn't be built on top of this approach, and forget about scalability. A component like this is perfectly appropriate if you know your snippets are going to be small and you don't need much extra functionality, but doesn't scale beyond that.

- FWIW I came across this video that I found very informative, regarding why CodeMirror operates the way it does: YouTube: Marijn Haverbeke - Grammar-based language modes for text editors. I'm beginning to grok that by comparison, the approach taken by react-simple-code-editor is extremely crude and wasteful of compute resources.
  - Note that the system I describe there never made it into mainstream CodeMirror (though you can use it if you install it separately), and lezer is a new, different approach.

- 🆚️🤔 Actually one of my main questions about Lezer is why not just use tree-sitter, which appears to do the same thing more or less. That could be a good point to address on the Lezer home page (which surprisingly doesn't mention tree-sitter), as many people will probably be wondering the same thing when they discover the project. The point is partially addressed in the README here lezer-parser/lezer , but it requires a lot of the reader to figure out exactly what Lezer has or does, that tree-sitter doesn't.

- ## 🆚️ Does anybody need a new code editor for the web that's 2x faster than Monaco, 10x smaller than CodeMirror, and works well on mobile?
- https://twitter.com/fabiospampinato/status/1618807374973911046
  - I'm syntax highlighting with the CSS Custom Highlight API, which hasn't shipped elsewhere yet. 

- highlight.js supports rendering to string plugins (the library “marked” uses it) but lacks the line numbers for it
  - I think Highlight.js isn't appropriate for this use case, it doesn't support tokenizing incrementally so it would block the main thread, potentially for multiple seconds for large files, and it doesn't support TextMate grammars, so the syntax highlighting will be sub-par.
- https://copenhagen.autocode.com 1/50 the size of Monaco, with most of the features.
  - It may be the best of its kind that I've seen so far. 
  - Mine uses TextMate grammars so syntax highlighting should be higher quality and smoother. And while scrolling it does ~5x less work (~10x less if we only look at the JS portion). It's  just PoC for now though.
- On a closer inspection Copenhagen seems to weigh 1/9th the size of Monaco (~190kb), not 1/50th. Like the instance of Monaco that I use is ~1.7MB, not ~10MB. And editing doesn't seem to work on mobile for me. Still interesting though.
- What grammar do you end up? tree-sitter? Also, is it canvas2d?
  - I'm using TextMate grammars at the moment, but I want to eventually add support for something else to it, like Monarch grammars, as otherwise it won't be 10x smaller than CM. No canvas, pure DOM.
- Can you use tree sitter for highlighting and ide like features?
  - Maybe in the future, it's very much a work in progress thing right now, currently only a TextMate-based syntax highlighter is supported.
- I think also http://repl.it also was working on something similar.
  - I think they are happy with CodeMirror, which is a fine choice

- ## Observable editor in observable_201909
- https://talk.observablehq.com/t/meta-observable-editor-in-observable/2376
  - One thing that I would like to do is to create a view with a nice text editor (ideally the same as the one used in observable) where users of my notebook can write some code with another linter (e.g. python) 
- Observable’s editor is based on CodeMirror. There’s a nice and simple example of CodeMirror in this notebook
- [CodeMirror inside of Observable](https://observablehq.com/@tmcw/codemirror-inside-of-observable)
  - We use CodeMirror to power a lot of the editing abilities of Observable, but we can also embed CodeMirror inside of a notebook to provide an in-notebook editing experience.

- ## [codemirror 6 _202102](https://news.ycombinator.com/item?id=26039111)
- One of the things I was hoping to see in this release was first-class LSP (language server protocol) support.
  - Sorbet (Ruby type checker) implements the LSP protocol and can be compiled to WASM
  - I'm especially excited to see mobile support as a headline feature, because that's completely lacking in Monaco. 
  - Maybe LSP support can be a future improvement.
- There's still no way to use create-react-app with monaco out of the box with offline support (@monaco-editor/react includes calls to a CDN instead of using the bundled JS).

- ## codemirror6: Decide how to distribute/manage CSS _201812
- https://github.com/codemirror/codemirror.next/issues/40
- Connecting modules to the CSS they rely on doesn't seem to be a solved problem in the JS ecosystem yet. Our plugins will often need a few lines of CSS to work. Requiring people to manually add `<link>` tags for each of those (which come from NPM and are probably not even in their web root by default) is a poor user experience.
  - I'm also not partial to schemes that inject the CSS into the page at run-time. When users are optimizing their page, they'd prefer to have control over how and when CSS is loaded, and not have that done at unpredictable moments by a script.
  - Who knows any existing approaches that we could take inspiration from?
- making it easy to write themes that integrate with the various plugins would be an advantage. 
  - This is one reason current codemirror.css defines all kinds of non-core styles—themes will want to include all of those as well.
- FWIW I took a stab a creating an Ubuntu theme package for CodeMirror 6. It was fun! 🆚️ The biggest difference from CM5 is having to deal with native selections, which can be styled with `::selection` .
  - The main suggestion I have after doing this is to more clearly separate the "core" CSS (required for correct layout) vs. "theme" CSS (that sets colors).
  - Regarding distribution, my gut feeling is that well organized plain old CSS would be best.
- Being a packaged component, we have somewhat different requirements than what most CSS-in-JS/CSS modules libraries are written for.
  - I was somewhat attracted to the idea of making all styles inline at first, since it nicely avoids the problem of having to create `<style>` tags and CSS rules at all, but that will often create really ugly DOM, and (more importantly) makes it impossible to support things like pseudo-classes and media queries, so I think we don't want that.
  - The alternative is to provide a way for scripts to generate class names from descriptions, and directly use those class names in the DOM. That doesn't work very well for highly dynamic CSS, but I guess the bulk of our CSS will fit the pattern just fine, and we can fall back to the `style` attribute for the rest.
- I was also working with styled-components for the past few days (I'm making a file tree component with react-virtualized).
  - I dropped CSSinJS at least for this case where performance IS the core component of the thing.
- Functional CSS makes the DOM directly reference the style. This works fine if you're in full control of the website, but a reusable component that wants to allow outside styling can't do that.
- style-module is much like a classical CSS module library, but works with sets of classes, rather than individual classes.
  - https://github.com/marijnh/style-mod
  - The idea behind that is that a plugin would define its styling as a style module containing classes for all the styleable elements it creates, and export that module. 
  - Client code can then extend this module and pass it back to the plugin as part of a configuration. 
  - If all plugins make sure they do this, and use the configured style module (with their own base module as a fallback) when styling, that should help with the overriding problem (without relying on side effects or global scopes).
  - The editor view itself would use a similar mechanism to allow the editor to be themed.

- ## We are rewriting CodeMirror _201808
- https://news.ycombinator.com/item?id=17858672
- Now I use Monaco aka Visual Studio Code. 
  - What would CodeMirror offer ? 
  - With Monaco I get all the lastest feature of VSCode . Current versions of Monaco include Intellisense etc.
  - I'm honestly curious both what CodeMirror will offer and why even try to compete. 
- CodeMirror aims to be slimmer, and less of a cut-off piece of vs code. I also think our API is more well designed and expressive. And, as Adrian mentioned below, though he got downvoted, CodeMirror works on phones
  - The fact that it works on mobile is the biggest advantage imho. We use it for that reason.
- monaco doesn't even try to work on mobile browsers.

- ## 🎯🤔 [CodeMirror 6.0 Stable Release | Hacker News _202206](https://news.ycombinator.com/item?id=31666186)
- 🆚️ Why wasn't ProseMirror a fit for Obsidian? Seems like that would be better for structured documents.
  - For a good portion of its users, an important feature of Obsidian is the use of flat Markdown files.
  - I'm inquiring about actual implementation not Markdown. Markdown -> AST -> CodeMirror vs Markdown -> AST -> ProseMirror.
- Obsidian uses CM6 on all platforms.
  - A CM5 based editor is still available as "Legacy Editor" in the settings on desktop, to support older plugins.
  - Mobile was always using a CM6 editor, while desktop only got CM6 some time after that. Which is probably the source of the confusion.

- We're currently integrating CodeMirror 6 into Overleaf, and you can try it out by joining our beta program (which will give the option to select the beta source editor, which is the one built using CM6). 

- CodeMirror is also much more usable on touch devices than Monaco (VS Code’s editor component).
