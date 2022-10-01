---
title: lib-editor-app-blog
tags: [blog, editor]
created: 2021-05-13T04:44:23.155Z
modified: 2022-08-21T10:11:37.453Z
---

# lib-editor-app-blog

# guide
- tldr: Unless browsers will open for the Web multiple crucial features (such as IME, keyboard, selection, touch, on-screen keyboard, spellchecker, etc.) contentEditable is the only sane way to handle text editing.

- contenteditable gives you one very important feature that you can't fake yourself: access to the browser's spell check and corrections
- Yep, we do use contentEditable as an input source and also as the view to which we render (you wouldn't be able to reliably handle the keyboard otherwise).
# repeat

## [ContentEditable  —  The Good, the Bad and the Ugly_201508](https://ckeditor.com/blog/ContentEditable-The-Good-the-Bad-and-the-Ugly/)

- ### ContentEditable is evil and the Selection API is its evil twin. Avoid them as much as possible. 
- You need a custom selection system. 
  - It must be doable nowadays to get position (represented by a range, but we’ll simplify this in a moment) in the DOM on mousedown/mousemove. 
  - You’ll display your custom caret (whoa… you can control its style now) and text selection (it’s a simple ).
- You need to handle typing. 
  - Let’s listen to the keyboard events and insert given character into the editor.
- You need to handle navigation using the Arrow keys. 
  - Left and right seem easy, up and down a bit trickier but if you have point 1, you’ll do this too. 
  - Wait, there’s the Alt modifier which makes the Left and Right Arrow keys jump entire words. 
  - But of course you’ll look for spaces in the text and that’s it — told you, it’s trivial!
- Then you need to do something with pasting. 
  - You see that with the Clipboard API you can listen to the paste event on the document and retrieve the data from the data transfer. 
  - You can also use the old paste bin mechanism.

- ### ContentEditable — the Good Parts
- It’s amazing that adding one attribute to an HTML element enables typing, selection, keyboard navigation, spell checking, drag and drop, pasting, undo manager. 
  - That all of this is integrated with the OS, 
  - that such editor can be used with a screen reader or on a touchscreen device 
  - and that it’s well internationalised. 

- ### CKEditor
- Over the past years, while working on CKEditor I noticed that we were gradually replacing native features with our own implementations. 
- Since version 4.0, CKEditor has its custom “insert HTML into selection” mechanism and a feature allowing reaching non-editable places.
- CKEditor 4.1 introduced highly customisable content filtering (no more mess on paste). 
- CKEditor 4.3 brought support for non-editable islands with editable islands inside which required overriding many native systems (selection, keyboard, focus, clipboard).
- Finally, just a few weeks ago we made a final takeover of the clipboard, which means that in some browsers copy, cut and paste operations are fully handled by CKEditor.
- It means that today CKEditor does not let the browser do anything to the content except handling typing, some deleting and that’s basically it. 
  - At the same time, it still uses the native selection system, keyboard navigation and other APIs such as those related to clipboard or focus management.

- With CKEditor 5 we are planning to conclude this process by letting the browser insert text only, but with CKEditor’s control.
# blogging

## [有道云笔记新版编辑器架构设计_202101](https://juejin.cn/post/6920054071571251208)

- [有道云笔记新版编辑器架构设计（下）](https://juejin.cn/post/6922343979325325319)

- https://techblog.youdao.com/?p=1743
- https://techblog.youdao.com/?p=1761

- 我们将新版编辑器的技术选型、架构和部分实现细节拿出来分享给大家，希望对大家开发富文本编辑器、做复杂系统的架构设计有一定参考意义。

### 编辑器发展简史

- 编辑器在前端开发领域是指可以提供给用户编辑纯文本、富文本、代码、多媒体内容等的功能模块，例如以云笔记为例，编辑器指下图中绿色的区域。
- 一般由编辑区域、光标、工具栏、右键菜单等功能模块组成，一般都包含编辑文字、设置文字样式、设置段落样式、插入多媒体内容、撤销重做、复制剪切粘贴等功能。
- 编辑器的由来可以追溯到打字机时代，我们可以将打字机的构造与编辑器进行类比，打字机的纸张对应于编辑器的编辑，打字机的游标对应于编辑器的光标，甚至敲击键盘的表现，编辑器也与打字机一脉相承：
  - 当敲击字母时，在光标后输入该字符；
  - 当敲击空格键时，在游标之后插入空格；
  - 当敲击回格键时，删除游标之前的字符；
  - 当敲击换行键时，游标换到下一行开始；
- 在计算机中，出现的最早的是文本编辑器，例如我们在 Linux 系统中常用的 vi，vim，emacs 等，它们可以对纯文本数据进行编辑，并引入了撤销重做、复制剪切粘贴、查找替换等编辑器的核心功能。
- 随着用户图形界面的兴起，人们对于文本的编辑不止满足于纯文本了，还需要给文本段落加上各种格式和排版信息。 同时，人们对于在文档中插入图片、图形、表格等更丰富格式的需求也越来越多。
  - 为了满足这些需求，富文本编辑器就出现了，其中的集大成者就是微软的 Word 和金山的 WPS。 
  - 但是它们的设计初衷就是做一款单机的文字处理软件，自然会遇到不支持互联网上的音视频格式、存储备份依靠本地计算机的文件系统、多人协作依靠文件拷贝等问题。
- 在互联网遍及千家万户的今日，人们反而不太需要 Word 提供的交互复杂的各种强大功能，而是需要支持更多互联网数据格式、存储备份更加方便、能够提供多人协同编辑功能的轻量级富文本编辑器。
  - 基于浏览器的富文本编辑器就是在这样的设计思路下产生的，其中的代表产品有 Google Docs、有道云笔记、印象笔记、石墨文档等。
- 这些基于浏览器的富文本编辑器都有以下特点：
  - 利用 Web 技术开发，需要在浏览器环境中使用；
  - 功能相对 Word 更加简单，只保留了最常用的富文本编辑功能；
  - 支持图片、附件、视频、音频、地图等多种互联网资源；
  - 可以将文档备份在网盘中，实现多端同步；
  - 文档可以分享查看，可以进行多人实时协同编辑。
  - 当然基于浏览器的富文本编辑器，也是经过了几轮的技术迭代和创新，才到了今天这种百花齐放的局面。

###  基于浏览器的富文本编辑器四要素

- 在现代的浏览器框架下，利用 Web 技术开发一款富文本编辑器，一般采用经典 MVC 模型，根据数据模型渲染视图，视图操作通过控制器修改数据模型。具体要解决以下四个问题
- 模型：
  - 模型包含内存模型和存储模型。
  - 存储模型是数据存储、同步和备份时的模型，需要考虑带宽、存储体积、模型序列化效率、模型正确性验证效率等因素。
  - 内存模型则是数据渲染时的模型，结构一般比存储模型复杂，会在存储模型的基础上添加其他渲染时需要用到的属性。
- 渲染：
  - 渲染指如何将内存模型渲染成 Web 页面。
  - 所有的基于浏览器富文本编辑器都将内存模型渲染成为了 HTML 页面。
  - 但是它们在排版上的策略略有不同，大多数编辑器都采用了基于 HTML 和 CSS 的排版方式，也有少数编辑器自己实现了排版引擎，例如 Google Docs。
- 编辑：
  - 编辑指如何提供编辑区域让用户在编辑区域编辑文档，以及如何感知用户编辑区域的编辑动作通知控制器以修改数据模型。
  - 浏览器提供了 contentEditable 的属性可以把元素变为可编辑状态，大部分编辑器都是以这个思路进行编辑的，并且它们可以拦截 contentEditable 元素的事件，将事件通知给控制器。
  - 也有少数编辑器自己实现了编辑区域和事件系统，例如 Google Docs。
- 指令：
  - 指控制器根据收到的编辑区域的编辑动作，生成对应指令修改内存模型，内存模型得以更新完成循环。
  - 这部分与数据模型相关，如果数据模型是 HTML，编辑器可以通过 execCommand 直接修改 HTML 数据，
  - 如果是自定义数据，监听或拦截编辑区域上的事件，也可以推测意图生成出修改数据模型的指令。
  - 通过指令修改数据，可以更方便的实现撤销重做、历史版本恢复、协同编辑等功能。

### 基于浏览器的富文本编辑器技术演进

- 基于以上四个问题，可以将基于浏览器的富文本编辑器划分为四代

- 第一代： 完全基于浏览器 API 设计，数据模型直接采用 HTML 数据，渲染用原生 HTML，编辑区域用 contentEditable 生成，通过 execCommand 执行浏览器自带的修改 HTML 数据的指令
- 基本没有成熟的开源编辑器或者商用编辑器采用这一种设计方式。
- 它们的主要问题处在 execCommand 接口上：
  - 只提供了有限的几个命令，例如 execCommand 就没有办法支持插入待办列表。
  - 提供的命令有些有功能受限，例如 'fontSize' 命令只能支持 1-7，导致不能自定义字体的大小。
  - 修改的结果与浏览器有关，例如 'bold' 命令在一些浏览器上会给选区中的文字添加 b 标签，而在另一些浏览器上则会添加 strong 标签。

- 第二代：由于 execCommand 功能上的限制，第二代的编辑器普遍抛弃了用浏览器的 execCommand 接口直接修改 HTML 文档的办法，而是用自己实现的 execCommand 和指令修改 HTML 文档，这样做就可以实现更加灵活多样的功能。
- 这类编辑器的主要问题是：不同的 HTML 结构可能表示的含义一样。例如下面两行 HTML 都表示一段既加粗又斜体的文字，但是他们的 HTML 结构却不一样，这样对比较数据是否一样就变得非常困难

- 第三代： 针对 HTML 含义不一致的问题，第三代编辑器则抛弃了既用 HTML 做文档模型，又用 HTML 做渲染的策略，而是采用自定义的数据模型，例如 XML 数据模型或者 JSON 数据模型。同样的数据模型渲染生成的 HTML 一样，自定义的操作则可以保证同样的操作修改之后的文档模型也是一样的。 
- 目前常见的编辑器产品例如：有道云笔记、石墨文档等，以及开源的编辑器库例如 Slate、Draft、Quill 等，都是第三代编辑器，它们已经能够满足大多数应用场景。
- 但是由于渲染出的页面中，可编辑区域还是基于 contentEditable，需要根据拦截的事件判断用户行为，生成对应的指令修改数据模型。
  - 一旦有用户数据没有拦截，或者处理的行为不对，用户的行为就可能直接修改了 contentEditable 的元素，导致数据和视图的不一致。因此产生的 bug 定位和修复都比较难，在编辑器的移动端适配中经常出现。

- 第四代：为了解决 contentEditable 引起的不可控事件，以 Google Docs 为代表的第四代编辑器则彻底抛弃的 contentEditable，自己实现排版引擎。排版引擎控制了文档的页面和布局，将数据渲染成为页面上的HTML。同时由于抛弃了contentEditable，还需要解决实现光标和选区的绘制、监听文字输入事件等技术问题，才可以做到和浏览器类似的编辑体验。
- 第四代编辑器相对于第三代，优点是彻底解决了contentEditable 引起的 bug，有更好的可扩展性。对应的代价是开发难度更高、体验不如原生、可能会遇到性能问题。目前只有 Google Docs 等采用了这种架构开发编辑器。

### 云笔记新版编辑器技术选型

- 有道云笔记新版编辑器综合了项目的可扩展性和实现难度，作出了以下的技术选型：
- 模型： 自定义的 JSON 数据格式作为内存模型，它的压缩版本作为存储模型；
- 渲染： 借助浏览器排版，用 React 框架渲染视图；
- 编辑： 不依赖 contenteditable，拦截浏览器事件判断用户交互，自己实现了光标和选区；
- 指令： 实现了丰富的自定义的富文本编辑指令，重新实现了 execCommand 执行指令。

- 总结起来，新编辑器采用典型的 MVC 模式，结合了 React 等前端框架的数据驱动的思想，通过修改数据模型来解决更新视图，由于放弃了 execCommand 和 contentEditable 这两个浏览器的 API，所以自己实现了指令系统、事件拦截和光标绘制。
- 但是由于富文本编辑器除了需要支持富文本的编辑功能，还需要支持图片、附件、表格、代码块等其他复杂功能，在上述框架内如何扩展支持这些功能，如何实现功能的解耦和可配置

#### 模型

- 有道云笔记新版编辑器采用了自定义的 JSON 数据格式作为内存模型。
  - 存储模型与内存模型基本对应，是内存模型的压缩版本，这样可以减少在数据序列化和反序列化过程中出现的错误。
- 文档模型：
  - 新版编辑器的内存模型采用了Document文档-Paragraph段落-Text文本的三层模型，顶层对象是文档，一篇文档包含多个段落，每个段落中有至少一个文本。
  - 很自然的想到用树的结构来表示它
- 对于富文本编辑器的数据模型，需要考虑文本的行内样式和段落样式：
  - 行内样式是作用于文字的样式，每个文字都可能有不同的行内样式，例如文字的粗体、斜体、文字颜色、背景色、字体、字号等
  - 段落样式是用作与段落的样式，整段文字只会有一个段落样式，例如对齐方式、行高、段落缩进等。
  - 由于我们三层文档模型中段落是单独一层，有对应的段落节点，所以对于段落样式只需要在段落节点上添加表示段落样式的字段，我们是在 paragraph 添加了 data 字段，其中添加了 style 属性表示该段落的段落样式
  - 如果要表示行内样式，目前文本节点中只保存一个 content 字段就没有办法胜任了，需要将它拆分为一个一个字符在每个字符上添加表示行内样式的字段，例如我们可以用一个 chars 数组，里面的每个元素表示一个字符，text 字段表示字符的内容，marks 数组表示字符上的行内样式
- 上述的富文本行内样式的表示方法中，我们可以看到rich的样式粗体、斜体、红色背景色保存在了 r, i, c, h 四个字符上，存在着冗余数据。
  - 我们参考了HTML渲染结果和部分开源编辑器的实现定义了合并规则。
  - 如果连续的字符节点，具有完全相同的行内样式，则它们可以合并成一个叶子节点。
- 简化后支持行内样式的文本节点也是一个树状结构，它包含一个或多个叶子节点，每个叶子节点包含文本的内容和这些内容共同的行内样式，且相邻的叶子节点的行内样式必须不完全一致

```JSON
{
  "type":"document",
  "nodes":[
    {
      "type":"paragraph",
      "data":{
        "style":{
          "textAlign":"center"
        }
      },
      "nodes":[
        {
          "type":"text",
          "content":"plain text",
          "chars":[
            { "text": "p" },
            { "text": "l", "marks":[{"type":"color","value":"red"}] },
            { "text": "..." },
            { "text": "t", "marks":[{"type":"bold"},{"type":"italic"}]}
          ],
          "leaves":[
                 { "text": "p" },
            { "text": "lain", "marks":[{"type":"color","value":"red"}] },
          ]
        }
      ]
      }
  ]
}

```

#### 渲染

- 云笔记新版编辑器依旧采用了浏览器进行排版渲染，没有像 Google Docs 那样自研排版引擎，
  - 原因是我们认为浏览器的排版引擎已经足够强大，基本满足日常的文本编辑需求，只有诸如图片的文字环绕、分页、分栏等比较高级的功能无法实现，
  - 而自研排版引擎需要大量的开发和测试工作量，还可能会产生性能问题，所以我们暂时还是用来浏览器进行排版和渲染。
- 我们采用了 React 框架，采用了组件化的方式渲染数据模型。针对文档-段落-文本的三层数据模型，以及文本节点的叶子模型，我们设计了对应 React 组件嵌套进行渲染
  - Document 组件渲染文档数据。
  - Paragraph 组件渲染段落数据，它是 Document 组件的子组件。
  - Text 组件渲染文本数据，它是 Paragraph 组件的子组件。
  - Leaf 组件渲染叶子节点，它是 Text 组件的子组件。
- 对于叶子节点包含的文本片段和行内样式，只需要渲染成一个带 style 属性的标签就可以了，这也印证了我们设计的富文本模型，简化了富文本的渲染逻辑，使得富文本渲染代码变得非常的轻量化。

#### 编辑

- 由于 contentEditable 会产生不受控事件，导致很多 bug，例如，一开始数据是 abc，对应渲染出的视图是一个 span，内容是 abc。由于需要提供可编辑，span abc 是一个 contentEditable 的元素。
  - 正常情况下，当编辑 span abc 时，例如输入了 d，我们拦截 keyup 事件，在处理函数中将事件 preventDefault，这一步是不让 contentEditable 元素自己修改 span abc为abcd，然后我们在处理函数里调用自定义的 insertText 指令，修改数据 abc 变为 abcd，再用新的数据进行渲染，修改 span abc 为 span abcd。
  - 但是，一旦出现 span abc 上的事件没有被拦截或拦截了但没有正常处理，就会出现 bug。
- 例如我们旧版的编辑器就没有拦截 ctrl + delete 的事件，
  - 如果在 abc 这一行按 ctrl + delete 就没有对应的事件处理函数修改数据模型，数据模型还是 abc，但是由于 span abc 是 contentEditable 的，ctrl + delete 事件会直接修改 span abc 将 abc 整行删除，这样数据模型和视图上就出现了不一致。
  - 后续如果再输入 d，则会将数据模型修改成 abcd，这时候视图会根据新数据渲染为 span abcd，表现为已经删除的 abc 再次出现，对用户的使用造成困扰。
- 👉🏻️ 针对 contentEditable 的问题，我们决定将完全抛弃它，由此带来两个问题：
  - 没有可编辑的元素，不会触发输入事件
  - 没有可编辑的元素，无法使用浏览器自带的光标
- 触发输入事件：
  - 我们采用了在用户光标位置后画一个隐藏的 Input 组件，Input 组件中有一个 textarea 来接受用户的输入，触发输入相关的事件
- 自绘光标/选区：
  - 由于不能使用浏览器默认的光标，我们只能自绘光标。
  - 我们参考浏览器的 Selection 的结构，设计了类似的Selection模型，并用Selection组件渲染 Selection 模型，在屏幕上用绝对定位画出用户的光标，同时用户拖蓝时产生的选区，也可以用这种办法绘制，由于光标和选区本质上一样，我们就放弃了浏览器的选区绘制，也改为自己绘制选区。
- 选区实现具体流程如下：
  - 用 anchor 表示用户开始托选的位置，focus 表示用户结束托选的位置。anchor 和focus 都包含了 nodeId 和 offset 两个属性，nodeId 表示位置所在的文本节点，offset 表示位置相对于文本节点开始的偏移量，以字符为单位。
  - 当用户点击鼠标开始拖选时，找到鼠标所在的 dom 节点对应模型上的文本节点，我们拿到 id 存储在 anchor 的 nodeId 中，再计算鼠标在 dom 节点上的位置，转换为数据模型上相对文本节点开始处的偏移量，存储在 anchor 的 offset 中。
  - 当用户移动鼠标或者抬起鼠标时，我们用类似的办法更新 focus 数据，将 anchor 和 focus 数据组合成为一个区域（Range）放入 Selection 模型中。这样我们就可以根据用户的点击/拖蓝操作构造出用户的光标/选区对应的Selection模型了。
- 然后，我们开发 Selection 组件渲染 Selection 模型。
  - 当 anchor 和 focus 在同一个位置时，Selection 组件将 Selection 模型渲染为一个闪烁的短线，表示用户的光标，
  - 当 anchor 和 focus 不在同一个位置时，Selection 组件将 Selection 模型渲染为一个从 anchor 位置到 focus 位置的一个或者多个矩形区域，表示用户的选区。
- 总结这一节，我们用 Input 组件触发用户输入事件，构造 Selection 模型和 Selection 组件用于自己绘制光标和选区

#### 指令

- 新版编辑器实现了丰富的自定义的富文本编辑指令，自己实现了 execCommand 方法来执行指令。
- 我们将光标定位到 ‘This is a ’ 之后，然后点击工具栏的颜色按钮设置颜色为红色，再输入字符串 'rich '，根据用户操作生成指令的过程
  - 在用户点击将光标定位到 ‘This is a ’ 之后时，我们更新了 Selection 模型，它的 anchor 和 focus 中的 nodeId 变为当前文本的 id，而 offset 变为 10。
  -  然后，用户点击了红色按钮，这时候我们在Selection模型上记录用户当前设置的行内样式，将在下一次输入时生效（如果点击其他地方，这个行内样式将会重置为新光标前面一个字符的行内样式）。
  - 最后，在用户按下按键输入文字时，我们拦截用户的keydown事件，从event.data中拿到需要插入的文本r，再根据当前的Selection模型，拿到anchor节点的nodeId和offset，以及存储在Selection模型上的行内样式，根据这几个参数就可以生成insertText指令了。

- 指令直接会有一些公用的逻辑，为了指令逻辑的复用，我们将一些公用逻辑也封装成指令。
  - 简单的指令(Operation)可以组合成复杂的命令(Command)。
- 例如选中一块区域并输入文字，理想的表现是删除区域内的所有文字，再插入输入的文字，这个复杂的命令我们将它定义为 insertTextAtRange，它实际上是由三步组成：
  - 第一步，先删除选区中的所有文字，这里我们用 deleteByRange 命令实现。而要删除选区中所有的内容，因为选区跨了三个段落，我们需要首先将第一个段落中的 ‘world’ 删除，用到了 deleteText 指令；然后将第二个段落节点 ‘hello javascript’ 整个删除，这里用的是 deleteNode 指令；最后我们还需要将最后一段中的 hello 删除，这里用的也是 deleteText 指令。所以一个 deleteByRange 命令又由多个 deleteText 和 deleteNode 指令组成。
  - 第二步，删除完选区所有文字之后，我们需要插入 editor 到第一段的 hello 之后，用到了上面提到的 insertText 指令。
  - 第三步，我们发现 hello editor 和2020都是文本段落，按照需求我们要将他们合并到一起变为'hello editor 2020'，就用到了mergeNode 的指令。
- 由此可见一个复杂操作对于的命令是有多个指令和命令共同组成的，这种方式能充分解耦和复用的指令，让每个指令只关注于实现一类对数据模型的修改。

- 将对数据模型的修改抽象成指令之后，撤销重做就变得比较好实现。
  - 我们规定指令都是成对出现的，每个指令都有对应的逆指令，例如 insertText 的指令它的逆指令是 deleteText，文档模型 Document 在 insertText 指令的修改下变为了Document'，那么根据 insertText 指令构造出的逆指令 deleteText 就可以修改Document‘ 让它恢复成 Document，这就是实现撤销重做的基础。
- 对于复杂的命令，我们会在他执行的时候收集执行的所有简单指令。
  - 在撤销时，根据指令的执行顺序，反向的执行所有收集到的指令的逆指令。
  - 在重做时，则只需要正向的执行所有收集到的指令。

### 新编辑器的分层架构

- 首先我们用图片功能为例，说明如何在现有框架下实现。
- 我们先只考虑占据一行的图片，这类图片可以单独当做一个段落，所以是可以放入我们的三层文档模型的第二层
- 对应的我们需要开发 Image 组件渲染图片，它与 Paragraph 组件一样，也是 Document 组件的子组件
- 点击工具栏按钮，我们需要在文档光标处插入对应的图片，这就需要我们生成 insertImage 命令，用它修改文档模型，生成 insertImage 命令的过程
- 由上述添加图片功能的做法可以看出，新添加一个功能，我们需要设计实现对应的模型定义、组件渲染和命令cmd，
  - 每个功能都涉及到这三处功能的修改，随着功能越来越多，不同功能之间的代码会互相耦合。
  - 并且，在不同应用场景下，需要不同的功能，例如编辑器 A 只需要图片附件和表格的功能，编辑器 B 需要图片、代办、列表的功能，这种编辑器定制是比较难实现的，之前只能通过屏蔽入口实现，js包里有很多无用代码。

- 为了解决编辑器核心功能和业务功能的解耦，我们将云笔记新版编辑器的架构分为了核心层和业务层：
  - 核心层 只负责提供富文本的编辑能力，以及多种拓展机制。
  - 业务层 负责实现各种各样的扩展功能，例如图片、附件、表格、代办、列表等。

#### 核心层

- 核心层的主要能力是通过MVC框架提供富文本编辑能力。 
- 首先，是 Editor 组件，Editor 组件提供包含富文本编辑能力的编辑器组件，业务层只需要将它作为一个 React 组件进行调用就可以了。 
- 其次，是 editor 全局对象，它上面挂在了执行编辑命令、撤销、重做等富文本编辑的核心接口。 
- 最后，核心层还提供了丰富的扩展机制，用于业务层对编辑器能力进行扩展。常见的扩展机制包含数据模型扩展、组件扩展、插件扩展、自定义命令等。

#### 业务层
- 在核心层提供的富文本编辑器的基础上实现云笔记编辑器的众多复杂的业务功能。 
- 首先，需要将核心层提供的 Editor 组件与业务层开发的工具栏、右键菜单等组件组合成为一个功能完整编辑器。 
- 其次，需要利用核心层的扩展机制开发相互解耦的编辑器特性，扩展编辑器的功能，例如图片、附件、表格、代办、列表等等。 
- 最后，还需要开发与云笔记编辑器与不同平台宿主 WebView 交互的接口层 editorAPI，实现云笔记编辑器的跨平台特性。


- 编辑器和核心富文本编辑功能和扩展功能之间以及不同的扩展功能之间都是单独开发的，耦合的可能性大大降低。
  - 同时针对不同的编辑器定制需求，可以组合不同的编辑器特性进行打包，这样就可以实现按需打包出定制版的编辑器。

#### 扩展机制
- 用核心层提供的扩展机制，我们重新实现图片的功能。
- 首先，我们将三层文档模型的第二层由段落泛化为块(Block)，
  - 块上提供 name 字段表示块的类型，默认类型为表示段落的 paragraph，针对图片类型，name 可以标志位 image
  - 图片模型中我们需要记录图片的地址，我们在块的模型中添加 data 字段用于存储不同类型块的自定数据，对于图片就可以在 data 中存储 url 字段
- 其次，我们在渲染时，针对块用 Block 组件进行渲染。同时在 editor 暴露registerComponent 接口，针对不同 name 的块，将对应的渲染组件注册进编辑器。
  - Block组件就可以在渲染数据时，根据 name 选择对应的注册组件进行渲染。
  - 例如，针对 name 是 paragraph 的段落数据用 Paragraph 组件进行渲染，针对 name 是 image 的图片组件，则用 Image 组件进行渲染。
- 最后，我们需要实现 insertImage 的自定义命令，通过 editor 的 registerCommand 注册命令，就可以在点击工具栏插入图片时调用 insertImage 的命令修改数据模型。在实现 insertImage 自定义命令的过程中，我们可能会用到 editor 上保留的编辑器内置命令和指令。
- 做完这三步，我们就利用编辑器的扩展机制实现了图片的功能。可以看出这样实现的图片功能，有扩展性强、耦合低、可插拔等优点。

### 总结
- 综上所述，云笔记新版编辑器采用了核心层和业务层的两层架构
- 在核心层，舍弃了存在较多问题的 contentEditable 和 execCommand 接口，自定义了数据格式，攻克了光标绘制、事件拦截、命令系统等技术难题，实现了富文本编辑的核心功能。同时还暴露了丰富的扩展机制。
- 在业务层，通过核心层暴露的扩展机制，我们可以开发各种不同编辑器特性，通过注册机制将它们注册回编辑器丰富编辑器的功能。
- 在开发有道云笔记的新版编辑器的过程中，我们遇到很多实际问题，愈发感觉到这是一个非常有深度的前端技术领域，所以我们将新版编辑器的技术选型、架构和部分实现细节拿出来分享给大家，希望对大家开发富文本编辑器、做复杂系统的架构设计有一定参考意义。

- [[方案]造一个富文本](http://luo0412.gitee.io/core/nav.4-2.ui/ch5-toolbox/02-5047253998648002.html)

## [CKEditor 5 - comparing Revision History with Track Changes](https://ckeditor.com/blog/ckeditor-5-comparing-revision-history-with-track-changes/)

- These two features of CKEditor 5 include Revision History and Track Changes, also known as Suggestion Mode.
- Both Track Changes and Revision History are premium plugins and features within CKEditor 5
- Track Changes is the ability to work collaboratively with others, not necessarily in real time, by seeing the suggestions they made to a document and being able to accept or reject them.
- Revision History revolves around the ability for users to analyze earlier versions of a document, compare them with one another and revert to a chosen version if desired.
  - Writers will need to periodically save states, or versions of their document, so that they show up on the chronological list 

- they are used at different stages of a document editing workflow. 
  - Track Changes enables users to apply suggestions that need to be reviewed by another user. This mode suggests what could be changed in the future; 
  - Revision History looks at what was already changed in the past. However, it may also include suggestions that haven’t been accepted yet within the revisions, if both features are enabled simultaneously.

- Revision History, on the other hand, focuses on providing users with three additional and key functionalities that Track Changes does not have. 
  - creating snapshots (revisions) of content, where such a snapshot is the state of the content at the time the user makes a save
  - comparing individual revisions with each other
  - restoring individual revisions

- In summary, Track Changes is more of a functionality improving the aspect of collaboration between users, 
  - while Revision History extends the application’s capabilities with content audit-trail and versioning functionality.

## [从流行的编辑器架构聊聊富文本编辑器的困境_202003](http://yoyoyohamapi.me/2020/03/01/%E4%BB%8E%E6%B5%81%E8%A1%8C%E7%9A%84%E7%BC%96%E8%BE%91%E5%99%A8%E6%9E%B6%E6%9E%84%E8%81%8A%E8%81%8A%E5%AF%8C%E6%96%87%E6%9C%AC%E7%BC%96%E8%BE%91%E5%99%A8%E7%9A%84%E5%9B%B0%E5%A2%83/)

- 几年前，Medium Editor 的开发者写过一篇著名的博文：Why ContentEditable is Terrible?，当中列举了一些 contenteditable 存在的一些问题：
- 视觉内容（用户所见）与实际内容（DOM）的一对多关系
  - 将编辑行为都托管给了浏览器，那么在不同的 DOM 结构下，执行相同的操作，浏览器要能够输出一样的视觉内容。
- 视觉选区与实际选区的多对多关系
  - 一个视觉选区可能映射为多种 DOM 选区，而一个 DOM 选区也可能映射为多个视觉选区

- Why ContentEditable is Terrible? 还有一个副标题： How Medium Editor Works?，它不仅仅描述了 contenteditable 存在的缺陷，还以此为引，阐述了 Medium Editor 的工作机制。
  - 近年来社区活跃度颇高的 Slate.js，Draft.js 、ProseMirror 以及 CKEditor 等也使用了类似的机制，来规避 contenteditable 缺陷，
- 这个机制可以被简单描述为：
- 模型与视图相分离
  - 让编辑器决定数据结构（内容 + 选区），保证视觉与实际一致
  - 方便同样的内容在不同设备设备展示
- 自定义命令
  - 脱离实现不一的浏览器命令（document.execCommand），自行划定编辑器的操作范围
- 这种机制最小程度使用了 contenteditable —— 仅仅让一个节点的 HTML 内容允许被编辑，而如何编辑，编辑器结果则收敛到了编辑器治理

- 防患未然：基于行为的同步策略
- 编辑器使用了视图模型相分离的架构，就需要处理视图与模型间的同步，当用户在编辑器完成了操作后，编辑器据此更新数据模型，再通过数据模型渲染出新的页面视图即对视图
- 编辑器是如何知道用户执行了哪个操作呢？答案就是 DOM 事件，假设监听到了 keyCode = 8 的 keydown 事件（Event），就推测用户是在执行退格（Intent），从而调用自定义的删除指令（Command），修改数据模型，最终用户看到光标前的字符被成功删除了。
- 基于事件拦截的数据同步，是理想型的同步链路，先更新模型，再渲染视图，由于模型和视图一一对应的关系，用户执行了相同的操作，总能获得一致的 DOM 结构，
- 然而，由于 DOM Event 的规范仍然在发展，各个浏览器对其的实现也不尽相同，因此，基于事件拦截的同步也不完全可靠。
- 举个例子来说，beforeinput event 是非常有用的一个事件，该事件在 Input Events Level 1 被定义，并在 Input Events Level 2 中获得完善，规范希望能帮助类似 Web 富文本编辑器这样的应用更容易地处理用户输入。
- beforeinput event 能让开发者在输入反馈到 UI 之前，通过事件的 inputType 属性知悉用户输入意图（例如，当 inputType 是 deleteContentBackward 时，我们就知道用户正在向前删除内容）， 但尴尬的是：
  - 要么浏览器不支持这个事件
  - 要么部分支持这个事件：例如覆盖到的 input type 不全
- 因此，DOM Event 本身的不完美，也就让编辑器难以完全摸清用户意图。
- 而对用户意图的模糊，也会造成：
  - 无法理解 ：编辑器忽略了某个用户操作
  - 理解错误 ：将用户的操作理解为了另一个操作，例如用户是在输入，但被编辑器理解为了删除，造成数据模型发生非预期变更，用户看到错误的视图
- 因此，基于事件的同步模型也是一个理想型模型，受限于浏览器支持，在实际应用中并不完全可靠。

- 亦敌亦友：输入法
- 输入法本身又不受控于编辑器，它完全由第三方厂商实现，其实现也只和操作系统有关
- 输入法和操作系统交互来合成文本，浏览器也通过操作系统，获得输入法状态，在输入过程中抛出对应事件。
- 输入法繁多 ：不同的操作系统版本、浏览器内核，和输入法能形成众多的组合，每种组合在 contenteditable 元素上进行文本合成的时候，难以形成一致的事件流
- 输入方式多样 ：除了键盘能够进行文本合成，还要支持手写、语音等输入方式
- Android 因为其生态紊乱，系统版本分布广泛，使用不同内核的浏览器众多，应用市场的第三方输入法层出不穷，让基于事件进行同步的策略更加脆弱。
- 在 Android 下使用某个第三方浏览器配合上某个第三方输入法编写内容时，可能遇到：
  - 浏览器不会抛出 beforeinput 事件 ：编辑器无法通过 beforeinput 事件中的 inputType 属性知悉用户行为
  - 浏览器没有传递正确的虚拟键盘响应 ：很多 Android 输入法都支持字词联想，当虚拟键盘呼出后，开始进入 Composing 状态，此时 keydown 事件的 keyCode 都会被设置为 229，那么编辑器无法也无法从 keydown 事件知悉用户行为
- 这就会造成比较恶性的现象，举个例子，当用户将光标放置在图片之后时，输入法被唤起，用户通过虚拟键盘按下了退格键希望能够删除图片。但由于编辑器既无法拦截 beforeinput 事件来判断用户是不是在执行删除，也无法通过 keydown 事件判断判断键盘的退格是否被按下，因此，也就不会生成对应的命令去修改数据模型，删除对应节点。此时，用户无论怎么疯狂点按退格，都不能把图片删掉。
- 因此，基于事件的同步策略，在面对输入法时，变得更加不可靠，社区目前流行的开源编辑器也仍在和 Android 输入法作斗争

- 亡羊补牢：基于现象的同步策略
- 编辑器之所以希冀于事件去同步数据模型和视图，是期望在浏览器对页面执行变更前，尽早将用户行为同步到数据模型上，实现实际内容与视觉内容的统一。但我们发现，这个本就不健壮的策略再遇到输入法之后，无法响应用户操作的概率更高了。
- 如果回到架构之前，仍然托管 contenteditable 的控制权给浏览器，那么，我们发现，输入法的增删改查还是能正确响应的，这也就说明了，托管给浏览器去处理 contenteditable，用户最基本的编辑诉求还是可以保障的。
- 当浏览器处理了用户的行为并更新了视图后，我们要尽快的去 “纠正” 数据模型，亡羊补牢，犹未为晚。
- 浏览器提供了 Mutation Observer 来让开发者监听 DOM 变更，它的 API 非常简单，初始化观察者之后，在适当时机开始观察即可，每次观察到的变更序列，其中的元素都是 MutationRecord 对象
- 借助于 Mutation Observer，编辑器在观察到 DOM 变化后，可以根据变化（现象）来反推用户行为，从而生成对应的命令，去修缮数据模型
- 这种 事后同步 ，弥补了浏览器无法派发正确事件时，我们仍能推测用户行为 —— 通过现象去反推用户行为。但是，由于现象的成因可能有多个，因此我们就可能造成错误的推断
- 我们的是人肉学习，为了获得更多特征，去更精确的映射用户行为，开发者将疲于应付不同的 Android 设备，不同的浏览器，以及不同的输入法形成的种种组合。
- 综上，基于现象去同步数据模型，是更不牢靠的手段， 即便开发者投入了大量精力去获得现象和意图间的关联关系，但难免还是有 “漏网之鱼”，导致模型 同步错误 ，这也许比不能响应操作更加严重。
- 而基于事件的同步模型，因为事件本身就表达了用户意图，所以推测会更加精准，所以，只有当事件系统不完善时（例如在 Android 设备下），我们才使用基于现象的同步做兜底，保证用户在编辑器能进行最基本的输入。

- DOM 的虚实调和
- 现代化的前端开发中，已经很少使用真实 DOM 来表达一个组件了，如果选用了类似 React 这样的解决方案去描述实现编辑器视图（Slate.js、Draft.js 就倾向于此），就会让视图的表达 “虚实并存”
- 在 Android 设备上，为了解决输入法问题，编辑器将输入先托管给浏览器，并 Mutation Observer 观察 DOM 变化，而后再去同步数据模型。在这样的策略下，用户的输入过程在没有结束之前，都是浏览器在处理，当中发生许许多多的变更，不再受 React 控制，很容易造成 “虚实不调”，引起编辑器崩溃。
- 因此，当使用了类似 React 这样的方案之后，编辑器需要更加 谨小慎微地 处理数据同步，在容易引起虚实不调的场合（例如段落分裂与合并），强刷（rerender）编辑器组件，调和虚实，让 DOM 与 VDOM 保持一致。
  - 而对于预料不到的场合，可能还需要借助 componentDidCatch 这样的 hook 去俘获异常，强刷组件。
  - 有 React 开发经验的同学都知道，对于编辑器这样内部子孙繁多的组件，重绘的开销是非常的，最终，在终端用户一侧，就是看到页面闪烁和卡顿。

- 上文对 Web 富文本编辑器困局的讨论，还仅仅局限单机版的富文本编辑器，如果还要为编辑器支持多人实时协同，那么面对的挑战更加艰巨。
- 面对这样的生态，做不到抛弃，编辑器只能去适应和妥协，但在其领域范围内，似乎还可以有一些突破：
  - 是否能通过交互绕开缺陷？
  - 是否能脱离 contenteditable 的架构？

## [最近迷上了富文本编辑器！_202111](https://juejin.cn/post/7027040695827300360)

- 于是想起了咱们的国产之光，wangeditor ，因为他们的功能类似，原理指定也类似，区别的地方其实就是设计思路的一些差别
- 在开始wangeditor 的心路历程之前，我们先要明确一定，富文本编辑器之所以可以编辑，其实是得益于 HTML contenteditable 属性 正是由于有了它我们才能实现在标签里面编辑内容。这是实现一个富文本的根本
- wangeditor 从第三个版本开始我基本也都看过，见证了他一步步的从一js到ts 的重构、从重视拓展性到到面向对象再到现在社区流行的函数式、从必须兼容ie到抛弃兼容ie 、从传统的webpack 的工程化构建到 rollup +monorepo的工程化构建
- 刚开始读v4的时候最最高兴的就是他每个方法都有注释, 至少咱知道从哪里入手，然后就是经典的面向对象设计。
  - 整体的设计架构就是利用面向对象的思想，将一个个的功能对象，组合成富文本的功能，主要实现以下功能对象
- 最近在拜读v5的源码，还还整理规划了v5的执行流程的思维导图，当然还没整理完毕
  - v5在slate他提供内核的基础上去自己实现view 的渲染
  - 从v4到v5 能明显的感觉到函数成了一等公民，这也与像vue3这类优秀的开源项目不谋而合。通过不同函数的组合，减少项目中由于引用类型带来的副作用
- 我主要想说的是为什么v5为什么要使用vdom？
  - 在v4 中主要就是利用MutationObserver 去监听dom树的改变，从而触发编辑器的功能
  - 整个v4是有自己的一套渲染规则，并且没有模型整个概念，他的所有的操作都是深深的绑定在当前这个富文本中，无法抽离
  - 而由于v5是基于slate， 所有完美的继承了slate 优点，将模型和视图分离，就可以随意的选用选用现有的效率比较高的view 渲染器去做视图的渲染，在v5中就是用了和vue2同款的snbbdom
- 我觉得（有可能不对）v5中之所以使用snbbdom 的原因有两点
  - 基于slate， 能拿到Slate 的数据模型 ，用最小的成本利用现有渲染器去渲染dom, 并且能通过操作menu等功能修改vdome从而渲染视图
  - 模型视图分离是一个趋势，也是一个更高的抽象思想，能让代码的架构更加清晰，便于理解
- **beforeinput**表示可编辑的dom在被修改前触发
- 为什么要弃用MutationObserver而选用beforeinput ？
  - 早期页面并没有提供对监听的支持，所以那时要观察 DOM 是否变化，唯一能做的就是轮询检测，比如使用 setTimeout 或者 setInterval 来定时检测 DOM 是否有改变。
  - 直到 2000 年的时候引入了 Mutation Event，Mutation Event 采用了观察者的设计模式，当 DOM 有变动时就会立刻触发相应的事件，这种方式属于同步回调。
  - 这种实时性造成了严重的性能问题，因为每次 DOM 变动，渲染引擎都会去调用 JavaScript，这样会产生较大的性能开销。
  - 从 DOM4 开始，推荐使用 MutationObserver 来代替 Mutation Event。MutationObserver API 可以用来监视 DOM 的变化，包括属性的变化、节点的增减、内容的变化等。
- 我觉得（可能有错）有两点原因：
  - MutationObserver虽然很优秀，但是他的监听如果数据发生变化还需要比较，拿不到最新的变化值，并且还会产生很多无用的节点，不适合slate 的体系
  - 主动操作menu修改样式等无需监听，直接更改slate 的数据模型即可
  - beforeinput 他除了能拿到当前改变的值，还能通过inputType知道当前输入的类型
  - 监听到输入之前的事件之后，就能根据不听的类型调用不同的slate 的api 改变slate 的内部数据模型，在触发回调函数，触发path 渲染dom

## [在线协作软件的三个核心引擎](https://juejin.cn/post/7002595221103968293)

- 优秀的协作软件必然由三个核心引擎构建：渲染引擎，协同引擎以及数据引擎
- 渲染引擎
  - 富文本编辑器
  - 表格编辑器
  - ppt/mind-map：图形编辑器
  - bi：布局设计器 + 图标设计器
- 协同引擎
  - 即时性、一致性、健壮性
  - 协同引擎存在的目的，本质就是保持各个终端在展示同一个内容模型时，能够在单个操作消费到模型之后，模型保持一致
  - 阶段1 - 客户端发送操作，
    - 操作等待同步给Server(其他协作者) pendingCommmands
    - 操作同步给Server（其他协作者） sendingCommands
    - 操作已同步给Server（其他协作者） sentCommmands
  - 阶段2 - 客户端模型消费操作
    - 操作作用于Model之后，客户端的Model应当与服务端的Model保持一致
- 数据引擎
  - Word - openxml的设计
  - Etherpad - 采用字符串 Z:1>6b|5+6b$Welcome to Etherpad!
  - Google Docs Word - 采用一个commands集合的设计
  - Google Docs Spread - 设计比较像Excel，但是使用的protobuf
  - Notion - 很明显是结构化的属性数据，并且使用CRDT的冲突解决数据结构
- 在Startup阶段，找到对应领域的合适技术选型，选择做出你协作软件的MVP，当自研能够成为你的壁垒或者优势，再选择自研
# editor-ide

## [LSP-language-server-protocol规范学习](https://zhuanlan.zhihu.com/p/343218679)

- LSP(Language Server Protocol) 语言服务协议，该协议定义了在编辑器或IDE与语言服务器之间使用的协议，该语言服务器提供了例如自动补全，转到定义，查找所有引用等的功能；语言服务器索引格式的目标是支持在开发工具中进行丰富的代码导航或者一个无需本地源码副本的WebUI。

- 每个开发IDE，都要为语言实现类如自动补全，转动定义，悬停在单词上提供文档的功能，传统上，需要个IDE根据自己的API实现上述工作，即使是相同的功能，也要根据不同IDE实现一遍重复的功能，代码却不同。
- LSP设计的目标是使该语言服务器和开发工具进行标准化的通信，这个语言服务可以在多个开发工具中重复使用，从而以最小的改动支持多种语言。语言服务器后端可以用PHP，Python或Java编写，LSP可以轻松地将其集成到各种工具中，该协议提供通用抽象级别的协议，以便工具可以提供丰富的语言服务，从而无需完全理解特定于底层域模型的细微差别。

- 语言服务器会作为单独的进程运行，同时开发工具使用基于JSON-RPC的语言协议与服务器进行通信。
  - 用户在IDE中打开文件时: IDE会通知语言服务器文件已打开(textDocument/didOpen)，此时文档的内容不会存在于真实的文件系统中，而是保存在IDE内存中。必须在IDE和语言服务器之间同步内容。
  - 用户编辑文件时：IDE会通知语言服务器文件更新(textDocument/didChange)，并且语言服务器会更新文件的语言表示。之后语言服务器会分析此消息，并将检测到的错误和警告，响应(textDocument/publishDiagnostics)通知IDE。
  - 用户执行"Goto Definition" 指令时: IDE发送带有参数的请求(textDocument/definition), params: {documentURI, position} 到语言服务器，语言服务器以文档URI和definition的Location作为响应。
  - 上述示例说明了协议如何在文档引用（URI）和文档位置级别与语言服务器进行通信。这些数据类型与编程语言无关，适用于所有编程语言。
- 当用户使用不同的语言时，IDE会为每种编程语言启动语言服务器
  - 并不是每种语言服务器都可以支持协议定义的所有功能，因此LSP提供了capabilities，一个capabilities可以将一组语言capability组合在一起，IDE和语言服务器使用能力宣布其支持的功能。
  - 需要注意：语言服务器到特定IDE的实现集成不是由语言服务器协议定义的，而是由IDE实现者决定

### [如何评价微软的 Language Server Protocol？](https://www.zhihu.com/question/50218554)

- 我只有一个问题， 这玩意会上传代码到服务器么？
  - 服务器就在你本地。。。懂了没？？只是和编辑器分开了，通过通信来交流
  - 网络传输会让你的ide跑的慢死 目前的都是本地服务器也就是个跨进程通讯而已
# more
- [Text Rendering Hates You](https://gankra.github.io/blah/text-hates-you/)
- [TEXT EDITING HATES YOU TOO](https://lord.io/text-editing-hates-you-too/)

- [为什么 ContentEditable 很恐怖](https://www.oschina.net/translate/why-contenteditable-is-terrible)

- [Slate.js - 革命性的富文本编辑框架](https://s1973.top/blog/0015499011852838c3eb8e0d6d14a3f97bee6e61fa1cd26000)

- [富文本编辑器的技术演进之路_UC-Hugo.js_201908](https://developer.aliyun.com/article/712971)

- [How we use WebAssembly at Fiberplane_202205](https://fiberplane.dev/blog/how-we-use-webassembly-at-fiberplane/)
- [Creating a Rich Text Editor using Rust and React_202204](https://fiberplane.dev/blog/creating-a-rich-text-editor-using-rust-and-react/)
  - We used to use Slate.js — a fine editor — but as we’re implementing our own rich text primitives for collaborative editing, we discovered the disconnect between our own primitives and Slate’s data model to be somewhat of a hindrance. So we got to thinking - what if we just built our own Rich Text Editor (RTE)?
  - From a very high-level perspective, a rich text editor is comprised of two components:
  - A data model and the core logic to operate on it.
  - A view that renders the state of said data model and that handles the user interactions.

- [Text Rendering Hates You](https://gankra.github.io/blah/text-hates-you/)

- [Over 14 years of todos recorded in text: My productivity app is a never-ending .txt file](https://jeffhuang.com/productivity_text_file/)

- [前端富文本基础及实现, 偏综述，基于contenteditable+document.execCommand](https://juejin.cn/post/7124839474575441934)
