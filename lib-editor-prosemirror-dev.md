---
title: lib-editor-prosemirror-dev
tags: [lib, prosemirror, text-editor]
created: '2021-05-06T09:39:21.604Z'
modified: '2021-05-06T09:39:53.522Z'
---

# lib-editor-prosemirror-dev

# guide
- prosemirror-pros
  - modular and extensible

- prosemirror-cons
  - 不支持动态改变schema
  - 与其他框架的集成不是很完美，ReactNodeView用不用portal的最佳实践不明确

- who is using
  - atlassian, nytimes, guardian...

- todo
  - prosemirror-codeblock
  - prosemirror-handsontable/data-grid
  - prosemirror-css/theming
  - vscode-prosemirror

- tips
  - 实现复杂组件可参考
    - 官方基于CodeMirror实现Embedded code editor的例子，使用NodeView，没用contentDOM
    - 官方Footnotes的例子，使用NodeView，没用contentDOM，但用了sub-editor，总共2个editor
  - 一个prosemirror document是一个无依赖的普通js object对象，所以实现第三方renderer也可行
  - 如果关注的重点是markdown和table，那就将更多的工作放在prosemirror层，增强通用性，将react wrapper层的工作尽量减少，方便迁移
  - 提供renderless/themeable不同封装层次/灵活性的组件
  - 类似footnotes使用多个pm-EditorView的例子

- 编辑器问题
  - 光标、选区、输入法、键盘事件
  - 首屏渲染完成后，用户输入文本时，是否还需要走一次完整的解析渲染流程
  - 分析一个产品或框架，需要考虑的方面：存储的数据结构、状态管理(更新转换)、视图渲染、样式主题

- prosemirror-renderer
  - `<canvas>`是标准的html元素，考虑实现nodeViews将特殊文本渲染到canvas，如表格、图表
  - tiptap的drawing示例，可以在空svg元素上画路径
  - atlaskit-editor开源了自定义renderer可以参考
  - atlaskit-editor实现了layout多列插件和图片排版插件

- prosemirror-examples
  - 方向：markdown、collab协作、data-grid、codeblock
  - 大部分的方案是以vanillajs为core，react为wrapper
    - 尝试保留rich-markdown-editor的api，将core用~~tiptap~~重写
- **vanillajs-first**
  - tiptap/dante/wix, tui.editor.v3, remirror, emirror
  - guardian-prosemirror-typerighter/elements/invisibles/noting, stacks-editor(StackOverflow)
  - milkdown(Typora), bangle.dev, pubpub-editor(202003)
  - start-editor, jcmnunes-bc-editor(md), zeditor
  - y-prosemirror, NotionEditor(toy)
- **react-first**
  - rich-markdown-editor/keyboardnotes, @atlaskit/editor-core, wax-prosemirror, xkeditor-next(r-m-e)
  - curvenote-editor(redux), czi-prosemirror(201906), licit(word), perry-white(newspaper)
  - Aditor, smartblock(202003), xen-editor(vanillajs为主，代码不多)，nib-edit(高级功能未开源如comment/collab)
- more-editor
  - pageboard/client(页面搭建), noteworthy(solidjs)
# pieces

# examples-remark-parse

- milkdown
  - https://github.com/Saul-Mirone/milkdown
  - https://saul-mirone.github.io/milkdown/
  - /454Star/MIT/202106/ts
  - 依赖prosemirror、remark、prism、katex，但不依赖prosemirror-markdown、react
  - A plugin-driven WYSIWYG markdown Editor, inspired by Typora, built on top of prosemirror and remark.
  - ⚠️️breaking: @milkdown/core@4.4.0(202107) migrate from markdown-it to remark

- https://github.com/marionebl/prosemirror  /mdx
  -基于react重新实现了部分prosemirror-view的功能，视图层用了pm-EditorState但没用pm-EditorView
  - A personal experiment libraries over prosemirror project
  - prosemirror + remark demos
  - https://www.npmjs.com/package/@marduke182/prosemirror-react-view
    - This library is a full React implementation of the official prosemirror-view package. 
    - Aims to implement a simple React Component that uses ProseMirror Data Model to render the document and bind the right events to synchronize the user selection and created ProseMirror transaction based on user inputs.

- https://github.com/Novartis/mdx-utils  /mdx
  - 实现了将mdx ast转换成PMNode，视图层仍然使用prosemirror-view
  - This package contains utilities for working with MDX syntax.
  - Parses an MDX document and its frontmatter into an AST.
  - Create a custom Prosemirror schema. 
    - This extends the Prosemirror Markdown schema with your custom elements, allowing its AST to represent your MDX document.
  - transforms an MDX syntax tree into a Prosemirror syntax tree. 
    - This way, you can load it into a Prosemirror editor and allow rich-text editing with your custom components.

- https://github.com/dxos/editor 
  - /AGPLv3/202101/js
  - Collaborative editor
  - 依赖 react、material-ui、remark-rehype、yjs、prosemirror、hightlight.js
- https://github.com/benrbray/noteworthy
  - Markdown editor with bidirectional links and excellent math support
  - 参考了prosemirror、zettlr、vscode、notable
  - 依赖solid-js、remark13、prosemirror、electron-window-state、remark

- https://github.com/rexxars/react-prosemirror-document
  - Render a ProseMirror document in JSON-format using React
  - 不使用prosemirror-view，直接转换PMNode然后用react渲染文档，实现过于简单
- https://github.com/ryaninvents/prosemirror-doc-tpl
  - jsx转PMNode，实现很简单
  - provides a concise way to create Prosemirror documents using a JSX-like syntax, for testing or content generation.
# prosemirror-examples-repos
- @atlaskit/editor-core /Apache2/ts
  - https://bitbucket.org/atlassian/atlassian-frontend-mirror/src/master/editor/
  - https://atlaskit.atlassian.com/packages/editor/editor-core
  - [kitchen-sink-example](https://atlaskit.atlassian.com/examples/editor/editor-core/kitchen-sink)
  - A package contains Atlassian editor core functionality
  - 基于react class组件实现
  - 提供了针对image/file的图文混排工具
  - 还提供了多列布局工具，包括两栏、三栏、按比例、居中
  - 提供了语法树ADF显示
- https://github.com/TeemuKoivisto/prosemirror-react-typescript-example
  - copy the approach by Atlassian editor_v20201205
  - https://github.com/TeemuKoivisto/prosemirror-track-changes-example

- wax-prosemirror
  - https://gitlab.coko.foundation/wax/wax-prosemirror
  - http://wax-demo.coko.foundation/
  - https://waxjs.net/docs/wax/
  - Wax depends on the following libraries.
    - React for the view(UI)
    - Styled-components for theming and styling.
    - Inversify.io as service containers，用的不多，可剥离
  - 依赖注入使用了很多class
  - 大量使用react组件

- tui.editor /11.8kStar/MIT/202009/popular
  - https://github.com/nhn/tui.editor
  - http://ui.toast.com/tui-editor
  - core只依赖 codemirror5，另外提供了react/vue-editor，v3新版本迁移到了prosemirror
  - 全都是vanillajs，react的封装很薄，只有3文件
  - 只依赖prosemirror，mark解析自己实现了toastmark，公司还自研了很多ui组件
  - 代码复杂度高
  - 通过代码块中的图表配置信息生成图表
  - [example: Editor with Chart Plugin](https://nhn.github.io/tui.editor/latest/tutorial-example06-editor-with-chart-plugin)
  - Markdown WYSIWYG Editor. 
  - GFM Standard + Chart & UML Extensible.
  - 编辑器支持：chart、uml、语法高亮、合并单元格、自定义toolbar、i18n、theming

- https://github.com/riboseinc/reprose
  - 渲染自定义组件基于`plugin.props.nodeViews`配置
  - 将插件的功能分为编写author和显示schema两部分
  - Configurable ProseMirror instance as a React component
  - Reprose’s functionality is contained in features. 
  - A feature can provide schema aspects (nodes, marks), and authoring aspects (key bindings, menu items, ProseMirror plugins).

- https://bitbucket.org/jstleger/prosemirror-composer
  - A useful way to keep complex prosemirror projects tidy, maintainable and testable.
  - complex Prosemirror project: [how we structured our code](https://discuss.prosemirror.net/t/prosemirror-composer-wip/3887)
  - Modifier - A modifier function takes a `transaction` and returns a `transaction`.
  - Handler - A handler function takes the `editorView` and composes the modifier functions and `dispatches` them.
- https://github.com/atlassian/prosemirror-utils
  - Utils library for ProseMirror

- https://github.com/YacheLee/Aditor
  - A React component made by ProseMirror
  - nodes和marks的自定义渲染执行发生在pm-plugin的new Plugin()过程中，没有使用NodeView

- https://github.com/shobokshy/rpm-editor
  - A React renderless rich text editor component.
  - 只依赖prosemirror、react
  - 没有提供使用示例

- https://github.com/d4rkr00t/prosemirror-dev-tools
  - Developer Tools for ProseMirror
  - Inspect document – all nodes and marks
  - Inspect selection – position, head, anchor and etc.
  - Inspect active marks
  - See document stats – size, child count

- https://github.com/BlueMona/prosemirror-react-renderer
  - An alternative to ProseMirror's DOMSerializer that converts documents into React elements instead of DOM fragments.
- https://github.com/johnkueh/prosemirror-react-nodeviews
  - An example of how to use React components as NodeViews for ProseMirror
  - 原理是`ReactDOM.createPortal(<Component />, container, shortid.generate())`; 
  - 事件传播会根据组件在react tree中的位置，而不是根据在真实dom tree中的位置

- https://github.com/ueberdosis/prosemirror-to-html
  - Takes ProseMirror JSON and outputs HTML. 基于php实现
  - https://github.com/enVolt/prosemirror-to-html
    - 基于js实现
- https://github.com/ueberdosis/html-to-prosemirror
  - Takes HTML and outputs ProseMirror compatible JSON. 基于php实现
  - https://github.com/enVolt/html-to-prosemirror
    - Takes HTML and outputs ProseMirror JSON.originally written for PHP

- https://github.com/BrianHung/editor
  - 依赖prosemirror-markdown、codemirror6、katex，不依赖react、tiptap、rich-markdown-editor
  - a rich text editor built upon the ProseMirror framework. 
  - It is based off tiptap and rich-markdown-editor, but tries to stay agnostic to Vue and React.

- https://github.com/MO-Movia/licit
  - http://greathints.com/licit/
  - WYSIWYG editor based on ProseMirror & React
  - 依赖express4、jquery、katex、react
  - 典型的适合学术论文的文档
  - 服务端依赖python，实现了协作编辑、图片上传
