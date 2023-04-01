---
title: lib-editor-app-community
tags: [community, editor, lib, text-editor]
created: 2021-05-14T12:04:27.547Z
modified: 2022-08-21T10:11:19.219Z
---

# lib-editor-app-community

# guide

# discuss
- ## 

- ## The amount of time I wasted because MutationObserver just stops working in @googlechrome is insane.
- https://twitter.com/fabiospampinato/status/1642232960135966720
  - I think that a whole bunch of other issues happen if you reload the page while the debugger is on or something, definitely worth a look, that feature is not stable at all.

- ## [keydown on a table inside a contentEditable div - Stack Overflow](https://stackoverflow.com/questions/26339719/keydown-on-a-table-inside-a-contenteditable-div)
- Only elements that can receive focus (such as inputs and `contenteditable` elements) fire key events. This does not include elements within contenteditable elements.
  - You can use the selection object to check where the caret is and therefore whether the key event originated from somewhere inside the table.

- ## [Get element on which keydown happened in contenteditable - Stack Overflow](https://stackoverflow.com/questions/48346540/get-element-on-which-keydown-happened-in-contenteditable)
  - I have a div that is contenteditable and that div has some contents p > em
  - I want to intercept keydown events and find the element into which the users have tried to write.
  - The event in the callback does not tell me which element has been written into, it only tells my I have written in #editable-div

- Another way I found was to use a `MutationObserver` on the editable element

```JS
const observer = new MutationObserver(mutations => {
  mutations.forEach(function(mutation) {
    console.log(mutation.target);
  });
});

const config = { characterData: true, subtree: true };
const div = document.getElementById('editable-div');

observer.observe(div, config);
```

- You could attach the keydown event to the body of your document. Then on keydown event, use document.activeElement to return the element which currently has focus and will receive the keyboard input.

- [Capture keypress/down/up events on a descendant of contenteditable element - Stack Overflow](https://stackoverflow.com/questions/61068091/capture-keypress-down-up-events-on-a-descendant-of-contenteditable-element)

- ## [contenteditable change event not fired - Stack Overflow](https://stackoverflow.com/questions/38444183/angular-contenteditable-change-event-not-fired)
- The `change` event does not fire on all changes to the value of the DOM element. 
  - The solution is to use the `input` event.
  - Unlike the input event, the change event is not necessarily fired for each change to an element's value.

- ## [The slowest part of TinyMCE: SaxParser_202110](https://github.com/tinymce/tinymce/issues/7341)
- What we're currently aiming for is a swap to the built-in browser DomParser then adding DomPurify to sanitise.
  - The problems you are describing seem to be more about how often the parser is run rather than an intrinsic performance issue with the parser itself. 
  - Micro-optimising things like how often a regex is compiled won't make any noticeable difference.
- We chose slate for mostly other reasons than performance we needed a model that would support all the complexity that a full featured editor like tinymce needs and we did look at other engines in the evaluation process during the planning phase. 
  - Some of these other models have a very flat design probably making them faster but also less flexible.
  - Performance is a balance it's all what you are willing to trade. Compatibility, flexibility, future proofing all comes into play.



- ## ACE2 is EtherPad's editor, a content-editable-based rich text editor. 
- https://news.ycombinator.com/item?id=18371309
  - It supports collaborative editing using operation transforms (easysync2), undo/redo, copy/paste.
  - The name "ACE2" is because this is a rewrite of aiba's original content-editable AppJet Code Editor.
  - https://github.com/ether/pad/tree/master/infrastructure/ace

> The name "ACE2" is because this is a rewrite of aiba's original content-editable AppJet Code Editor.

- ## [The CKEditor 5 and CKEditor 4 comparison](https://support.ckeditor.com/hc/en-us/sections/115001489149-The-CKEditor-4-and-CKEditor-5-Comparison)
- When compared to its predecessor, CKEditor 5 should be considered a totally new editor. 
  - Every single aspect of it was redesigned — from installation, to integration, to features, to its data model, and finally to its API. 
  - There is no "drop in" solution for migrating. 
- New data model
  - The new data model is part of the MVC architecture of the editing engine. 
  - It is defined and controlled with pure JavaScript, moving the data model that represents the text totally away from the browser
  - The data structure is normalized and optimized for complex data management operations making implementation of algorithms such as Operational Transformation and real-time collaboration possible.

- ## 开源富文本编辑器技术的演进__20201024
- https://zhuanlan.zhihu.com/p/268366406
- 在2019年8月份左右的时候，我们开始开发自己的知识库产品PingCode Wiki，然后对于在线文档、知识库以及背后的富文本编辑器技术都有了更深刻了解和认识
- 大家公认的富文本编辑器领域在前端里面是天坑的存在，落后的生产力与人们日益增长的需求之间的矛盾
- 落后的生产力：
  - 编辑内容相关标准推进缓慢
  - 浏览器厂商对于相同操作或者场景实现方式的不同，导致兼容性的问题
  - 使用HTML DOM描述富文本内容有太多不可控制的情况
- 日益增长的需求：
  - 不确定的交互意图，比如按Delete键，不同的焦点位置有不同的情况需要考虑
  - 内容输入的多样性，比如有：打字键入、粘贴、拖拽等，每个处理起来都相当复杂
  - 大量需要拦截阻止和代理的浏览器默认行为，保证数据的完整性和正确性
  - 用户对于编辑器的使用要求越来越高，比如：合并单元格、列表多级嵌套、协同编辑、版本对比、段落标注，大家都认为这是基本需求，其实这里面的技术难度是超出大家的想象的。
- 这里我主要从技术实现以及编程思想的演变，介绍编辑器这10年间的变化与发展。
  - CKEditor 1-4（2008）
  - UEditor (2012)
  - Quill.js（2012）
  - CKEditor 5（2014）
  - Prosemirror（2015）
  - Draft.js（2015）
  - Slate（2016）
- CKEditor 1-4可以代表传统编辑器的技术路线（同类型技术的主要是UEditor），
  - 主要依赖于浏览器原生的编辑能力，用户内容的输入是浏览器直接处理，加粗、斜体、回车等这类的处理则是捕获浏览器的事件来覆盖浏览器默认行为来实现，
  - 再辅以一些DOM的嵌套规则（dtd）和复杂数据输入（如粘贴）的过滤规则来约束数据的正确性，这类编辑器整体思路还是比较清晰的。
  - 内容的可编辑主要依赖DOM的contentEditable属性，基于原生execCommand或者自定义扩展的execCommand去操作DOM实现富文内容的修改。

- ## Which one was the one with the bad performance on long documents? ProseMirror or CodeMirror?
- https://twitter.com/thomasaull/status/1314484953686695936
- CodeMirror is normally much faster for big documents, 
  - but from the context, I suspect that in this case the magic layered on top to make CodeMirror behave like a rich text editor is the source of the slowness.

- ## Why is CodeMirror not based on or replaced by ProseMirror?
- https://twitter.com/tjconceptdk/status/1035585261198041088
- They solve different problems -- `structured rich text with configurable schema` versus `plain text with syntax highlighting and lazy rendering` . 
  - On the web you don't want to ship big, overly general code for a smaller problem

- I was doing some research and I was wondering why you didn't use the same textarea technique in ProseMirror as you did in CodeMirror? Is it planned or impossible to implement in a rich text editor? 😊
  - Because it is a more problematic hack than just using contenteditable. CodeMirror 6 will do the same

- ## CKEditor 5: New approach to rich text editing on the web_201710
- https://news.ycombinator.com/item?id=15497972
- It's got to be tough spending a career working on ContentEditable. 
  - "Why are you implementing the caret in javascript? Haven't you heard of ContentEditable?"
  - "Why is your simple WYSIWYG editor component seven megabytes of javascript? Wouldn't it be better to just use ContentEditable and be done with it?"
- Rather than using an all-inclusive editor like CKEditor, Froala or Redacted, I've been thinking a lot about a "block" based content creation like one that is available on notion
  - We have in mind the "block-based editor" or "content builder" solution you're talking about. 
  - This could be relatively easily created having CKEditor as its base. 
  - This means that CKEditor may not be the ready to use way for it but it provides a good framework to develop such solution.
  - For example, its powerful widgets system, which can be used to handle "blocks"
- Block Based Editing...?
  - SharePoint is knocking and asking for it's render model back. Web-parts in SharePoint are the whole reason why SharePoint runs like a dog.
  - For the open web to go down this route is very worrying indeed.
- The block-based content is an idea that has been around for a long time and is embodied in several CMS's. 
  - As a developer, there are 2 advantages I've found to the block-based approach
  - The editing interface can be custom-tailored to the content and the non-technical users who are editing the site via a GUI interface can be more "guided" through the data.
  - The front-end HTML+CSS markup can more easily be customized around the content fields.
- It still uses contenteditable, though, like Quill and ProseMirror, which also use a custom data model and ops. It sounds like CKEditor has caught up to have this kind of architecture too. Not to trivialize this accomplishment. All three are impressive feats of engineering and design.
  - One thing I've realized playing with a ton of different editors is that **contenteditable gives you one very important feature that you can't fake yourself: access to the browser's spell check and corrections**. It's possible that CKEditor ignores everything else about contenteditable, but turns it on just for red squigglies.
- Yep, we do use contentEditable as an input source and also as the view to which we render (you wouldn't be able to reliably handle the keyboard otherwise).
  - tldr: Unless browsers will open for the Web multiple crucial features (such as IME, keyboard, selection, touch, on-screen keyboard, spellchecker, etc.) contentEditable is the only sane way to handle text editing.
  - There's an ongoing initiative to fix this situation but it's an extremely complicated topic. 
  - Fortunately, 2 years later I can still say that things move forward. E.g. the `beforeinput` event landed in a couple of browsers.
- Makes sense.
  - There is a route you can go that doesn’t use contenteditable, except as a small box at the cursor position to handle IME; it’s what Google Docs does. 
  - At my most recent job (stealth start-up) we built an editor like this, painting our own selection and everything. 
  - It makes certain things easy or possible — custom text wrapping, tab stops, custom handling of cursor and selection with regard to embeds. 
  - It doesn’t get you very far on mobile web, though.
- Spellcheck and corrections can be faked, I think, if you decide to compile your own hunspell (or whatever). 
  - IME (i.e. entering text for languages that do not have a one-to-one mapping of key press to character), though, is a lot harder; 
  - you have no idea what languages the user has configured, and showing _everything_ in a list is impractical.
- Few people seem to know about Composition Events. Using those, implementing IME should be relatively easy. The events tell you which partial characters to show, and which completed characters to insert.
  - Unfortunately, it's not that easy. 
  - Composition events are typically controlled by the IME software, which is not part of the browser proper, and tends to be a lot less serious about conforming to standards. 
  - The result is that the data in those events often simply doesn't correspond to the actual DOM changes that they caused. 
  - On Android, you can't even rely on the fact that compositionstart fires when a composition is started—with some virtual keyboards (which act as IME providers) you routinely get compositionupdate or compositionend before a start event.
  - Listening to these events and using DOM diffing can get you a more or less accurate idea of what happened. But 'relatively easy' does not apply.
- IME support sucks, even with contenteditable.
  - I have yet to find a free contenteditable-based WYSIWYG editor that works properly with the Korean IME in recent versions of iOS. Duplicate characters everywhere. Even the Enter key sometimes works and sometimes doesn't, depending on what character is immediately before the line break. 
  - Froala is better, thanks to a Korean guy who helped develop a fix for them despite the fact that it's not even FOSS.
- It is true that working with IME is hard, even though it is kind of supported by operating system and browser.
  - As much as it is doable for standalone editing, it is a nightmare for collaborative editing, where content changes all the time - not only at the place where you type. Each content change may cause composition (IME) to break. That's how the browser works.
  - This is one of the reasons why "real-time collaborative editing" solutions often implement "block limiting" -- one block/paragraph can be edited only by one user at the same time.
- ContentEditable was supposed to bring us a world where things like CKEditor no longer needed to exist.
  - ContentEditable never really specified much of a cross-platform standard API. 
  - If we wanted to replace CKEditor and its ilk, we should have pushed for a standard spec on textareas with rich structured editing support for a variety of formats (Markdown, reStructuredText, HTML, etc.) 
  - But that would then require standardizing structured text formats and/or figuring out how to add extensible functions, what to do with copy and paste especially from third-party apps, how should drag and drop be handled, what about saving, auto-saving, how should you add styles to a drop-down list to let users pick their own fonts, font-sizes, etc. 
  - These are complicated things to get right, often site- and implementation-specific, and contenteditable allowed for direct text manipulation and editing (with spell check and native text cursor flickering) within HTML, which is good enough to build your own rich editing interfaces around. 
  - So, it would be going too far to say ContentEditable was supposed to put these RTEs out of business. 
  - In fact, I would argue that Markdown's popularity has done more to put RTEs out of business recently, and that block-based, template- or widget-integrated text editing is the future, and where these tools' APIs are headed.
- CKEditor 5 uses contentEditable. And that's a good decision—getting bidirectional text, IME, touch selection, spell-check, and screen reader support right without contentEditable, while possible, would require you to reimplement a _lot_ of browser functionality, which would necessarily lead to a blowup of complexity and download size.
  - So sure, the new CKEditor does more or less what Quill, Slate, ProseMirror, and most other modern WYSIWYG components do—it separates its data model from the editable DOM. That's good, but not new.
  - Focus a demo editor and inspect `document.activeElement` in the console. You'll get a parent div of the content whose `contentEditable` attribute is true.
- I've been fascinated with operational transformation for some time, but I haven't found anything that breaks it down into understandable steps.
  - A guy responsible for OT in Google Wave wrote once that he spent 5 years on it and it still does not work well in all cases. 
  - The original OT implementation has been designed for linear documents – texts. It does not fit very well with tree structure – you don’t want elements (tags) to intersect after resolving collision. It also does not fit undo where the order matters.
- I don't see many people talk about Apple's approach to text editing, on iCloud.com Pages. They use svg and it allows them to achieve some pretty fancy effects. Anyone experienced with this method?
  - They use an invisible content editable field that moves to where the caret is placed. 
  - The content editable only contains the current word or selection.
  - Text typed into the content editable is rendered into SVG elements. Unfortunately that doesn't allow a browser's spellcheck to work so they had to implement their own.
  - iCloud Notes works in a similar way but it renders to canvas elements instead of SVG. Also doesn't provide spellcheck.
- The idea to separate the model and the view is as old as MVC itself. However, what matters here is how the model is actually implemented and what mechanisms it supports.
  - In CKEditor 5 we took perhaps the longest possible road so a tree structure with Operational Transformation support and couple of other goodies. It costed us a 3 years of work, but it was worth it. 
  - We proved the concept and validated the results by implementing the Letters app which supports real-time collaborative editing for real (with selective undo, commenting, displaying selections of other users, etc.). 
  - We'll now be working on adding more features like e.g. tables support which rise the bar for the data model and the whole architecture even higher, but we're very optimistic seeing the results to far.

- ## Notes as data
- https://twitter.com/gordonbrander/status/1429105115886018560
  - [If headers did not exist, it would be necessary to invent them](https://subconscious.substack.com/p/if-headers-did-not-exist-it-would)
-  I’ve filed it away as a nice pattern for identifying important problems, e.g. “If we don’t build X, would we need to later invent it?”

- ## I was puzzled why the *same* hex codes in @code produce a different color than in @atom .
- https://twitter.com/LeaVerou/status/1422512437979455507
  - Code’s are visibly more saturated. What’s going on?
  - Atom uses Chromium, and thus interprets colors through CSS. In CSS, hex colors specify coordinates in sRGB, not the monitor color space. 
  - @code not being built with web technologies, just throws raw RGB coordinates at the screen. THIS IS WHY COLOR MANAGEMENT MATTERS PEOPLE!!!
- VS Code is also built on Chromium with CSS & HTML, as others have said, but the **actual rendering of text uses canvas WebGL**, I think, so that may be where the colour space is getting mangled.
- Chromium has a flag for color profile; At some version chrome switched to sRGB by default so colors started to look different than system picker/other browsers. Then switched back or something, I quit it. There’s still discrepancy.
  - Chrome switched to sRGB because that's the spec for how CSS hex colors are interpreted.
  - If system pickers use device RGB that's a poor choice, because it's not portable, the same hex code on my machine is different than on yours.

- ## I needed to augment a simple textarea with keyboard shortcuts for basic Markdown formatting + drop/paste image support like GitHub comments
- https://twitter.com/adamwathan/status/1414216138796449793
- Just a vanilla textarea
  - Yeah definitely a bunch of JS but textareas have the APIs you need for this. 
  - GitHub’s comment field is a textarea too, not a contenteditable div or anything like that.
- It’s just the rendering that is limited, that’s why **bold** is rendered with asterisks. 
  - In a contenteditable you can render HTML, for example a `<strong>` tag or even more advanced things like Vue or React components. 

- ## [在线编辑器, 多人同时编辑, 如何设计undo/redo的逻辑?](https://www.zhihu.com/question/367915946)
- 感觉有三种模式:
- 按action撤销. 
  - 甲/乙撤销, 会消失一个c. (这样做我觉得容易做, 所有状态容易管理)
- 只撤销自己做的. 
  - 甲撤销, 消失一个c; 乙撤销, 消失一个B. 
  - Google docs是这么做的, 但是交叉修改后再撤销重做, 应该会造成极大的混乱, 如何解决?
- 一路撤销到自己做的. 
  - 甲撤销, 消失一个c; 乙撤销, 变成aaaBB. 这样就是有点绝情了. 甲想恢复自己的编辑, 需要乙重做.
- 一般采取的是第 2 种方式，即只撤销自己产生的操作。
  - 那么怎样才能实现只撤销自己产生的操作呢？这就不得不说说 OT（Operational Transformation）和 CRDT（Conflict-Free Replicated Data Type）算法了。
  - CRDT 在 2006 年被提出，用于解决分布式计算结果的最终一致性问题。
  - 相比较还存在很多边缘场景需要打补丁的OT算法，CRDT 可以说是更加先进一些。也有非常多开源的库可以选择，比如 yjs , automerge , gun 或者 teletype-crdt
  - 简单来说，OT 需要一个中心服务器（用于保证正确性），而 CRDT 则可以支持点对点直接传输数据。

- ## Editor.js – Block Styled Editor
- https://news.ycombinator.com/item?id=19555633
- From a data management and flexibility standpoint, I see why block editors are becoming popular with some people. 
  - But as a user, it feels like a downgraded experience.
  - When writing multi-paragraph prose, the first draft isn't always the final draft. Quite often there's some shuffling around of parts of the content. 
  - With blocks, the user can't highlight part of one paragraph and into part of the next one because of the artificial container boundary.
  - Perhaps with some well planned keyboard shortcuts and other UI improvements, the friction can be reduced. Maybe also it will require a change in the way some of us think about content (although I still object to the user needing to think of content in terms of its subtypes and storage structures).

- I'm the current maintainer of https://github.com/madebymany/sir-trevor-js which we started in 2012. 
  - At the time we had a fully block based approach and migrated to more of a document based approach when medium.com gained traction.
  - Since then we've debated what's the best approach for cross block selection as now the expected behaviour is very much that of a text editor such as word rather than a block based editing tool which it started out as. 
  - A couple of years ago we embarked on a rewrite that saw us look for a solution to the problem that would solve this. 
  - Not just a block based selection, but a cursor based selection between blocks, but this never got to a level we were happy with.
  - I think with the evolution of online editing over the years and editors such as notion.so the approach they've taken with the multiple contenteditable elements is a good first step. 
  - Over time we'll see how far they are able to take it. Adding features such as cross browser support, undo/redo and keyboard navigation.
- I'm a maintainer of Editor.js. Regarding to your questions:
- Editor.js doesn't support nested blocks.
  - We keep structure flat and want Tools API to be as simple as possible for new developers. 
  - The target audience of the Editor.js is media and blogs, usually you don't need complex structure there. 
  - However, you can implement some complex plugins for your needs, nested lists as example.
- We consider development of the editor very serious and understand importance of the test coverage. 
  - At the moment we don't have unit neither e2e tests but this is the one of our next steps on the way.

- Two long established predecessors to this: Sir Trevor JS and Colonel Kurtz
- I've used Kurtz extensively and it's been brilliant. 
  - The only downside of all these block-based editors is that you can't easily create layouts where images float to the left or right of text. 
  - Well, you can create them but you don't get a WYSIWYG idea of what it looks like right in the editor. I can live with that!
  - I've explored all sorts of editors and Colonel Kurtz is the one that's worked best: Trix, Draft, TinyMCE, CKEditor, ContentEditable, ProseMirror - just off the top of my head.

- ## Announcing: Work is underway on CodeMirror 6, a full rewrite with accessibility, mobile support, and modularity as design goals. 
- https://twitter.com/teppeis/status/1034581567551631361
- How will this affect ProseMIrror project? What is the difference?
  - ProseMirror is for structured text, CodeMirror for plain text and code. They don't really affect each other
- Will it support the native browser spellchecker?
  - Somewhat. The main issue is that in many browsers, the spell checker gets completely confused (removes most of its underlines) when you programmatically touch the DOM. And in typical situations, CodeMirror will do that to adjust the highlighting.
  - Still, we do take care to only mess with the DOM when necessary, so when in content that doesn't change it highlighting during typing (Markdown without markup, HTML text nodes) it might work pretty well. Haven't done that much testing there yet
- Monaco still doesn't support even arrow keys on iPad/iOS. Ace and codemirror are at least usable.

- ## I have tested/worked with some #javascript rich text editors, here is my feedback. 
- https://twitter.com/nurlannurmanov/status/1409361282889928707
- My criteria were as follows:
  1. Can be used in #React  web apps;
  2. Out of box example which covers most of the use cases (image, formatting, code addition);
  3. Production-ready; 

- ## [在基于前端技术的编辑器中，ObjectURL 的生命周期如何管理？](https://www.zhihu.com/question/553426184)
  - 编辑器中对本地添加的图片素材以 URL.createObjectURL() 生成的 URL 来引用。但是这样生成的链接引用的文件会常驻内存而不会自动回收，需要 URL.revokeURL来释放。

- 的确没有用过 revokeObjectURL()，你是真实发现页面有内存问题了吗，比如会 OOM？
  - 如果你现在引用计数的方式可行，那我下面说的这个设想也许会更方便一点
  - 就是把原生的 createObjectURL() 返回的 URL 字符串包装成字符串对象，如果能不覆盖 URL.createObjectURL，最好不要覆盖，把 new String 的逻辑放在自己的模块里。
  - 这个时候就可以在这个字符串对象被垃圾回收的时候，执行 revokeObjectURL()：

```JS
const _createObjectURL = URL.createObjectURL;
URL.createObjectURL = function(blob) {
  return new String(_createObjectURL(blob))
}

const registry = new FinalizationRegistry(objectURL => {
  URL.revokeObjectURL(objectURL)
})

registry.register(objectURL, objectURL + '') // 第二个参数需要是字符串原始值
```

- ObjectURL需要手动释放是因为它引用了blob对象，导致blob本身不能释放，反而这个引用对内存来说微乎其微。这个场景下可以存储文件的File对象，点击下载时才生成blob再创建引用，下载完成就释放引用，从而让blob对象被回收。

- ## [国内有做类似于Google Docs级别「富文本编辑器」的团队吗？](https://www.zhihu.com/question/397012334)
- 一个叫“一起写”的产品，创始人是 Google docs 出来的，做的就是类似产品，不过好像已经被快手收购了

# more
