---
title: lib-editor-app-blog-vendors
tags: [blog, editor, vendor]
created: 2022-10-19T20:08:55.194Z
modified: 2022-10-19T20:09:13.427Z
---

# lib-editor-app-blog-vendors

# guide

# editor-cn

## [vivo_富文本编辑器之游戏角色升级ing_202107](https://juejin.cn/post/6981249485267533854)

## [vivo_富文本及编辑器的跨平台方案_202108](https://juejin.cn/post/6997212807003537416)

## [有道_有道云笔记新版编辑器架构设计 上_202101](https://juejin.cn/post/6920054071571251208)

- [有道云笔记新版编辑器架构设计下](https://juejin.cn/post/6922343979325325319)

- https://techblog.youdao.com/?p=1743
- https://techblog.youdao.com/?p=1761

- [有道云笔记跨平台富文本编辑器的技术演进_旧架构_201806](https://sq.sf.163.com/blog/article/168068797113712640)

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
# editor-ww