---
title: lib-office-notable-dev
tags: [dev-log, notable, note-taking, office]
created: 2020-05-10T07:13:28.652Z
modified: 2024-01-29T23:05:26.855Z
---

# lib-office-notable-dev

> local/offline first markdown-based note-taking app

# features
- pros
  - no vendor lock-in with local markdown files
  - nestable tags
  - attachment
  - multi-note editing for tags/pins

- cons
  - 不支持移动端
  - 未实现同步
  - 会在打开新文件时自动在文件头部添加时间戳front-matter
  - 对本地文件的结构组织有要求，包括顶层`notes`文件夹、附件`attachments`文件夹
  - 未实现文件管理器，用户使用tag对笔记文件进行管理，所以笔记文件在同一层级

- features
  - core: edit/view-local-files; tags; search-contents
  - 文件显示为扁平结构，无文件夹视图，但可用标嵌套标签tag来表达层级结构
  - local/offline/private/privacy first markdown-based note app
    - local note data as first class data source
    - local means personal,born to keep data private,强调数据由用户掌控
    - offline means no ad，强调可通用易移植
    - full control of your data, free for sharing and exporting
    - 如何解决版权问题？只能localize本人的创作
  - online sync is optional
  - Split Editor
  - extended markdown support, including GFM/MDX

- toc
  - toc优先采用docked/sticky的设计
    - 因为文章内容较长时，对于随页面滚动的toc会滚动到页面顶部然后消失
- themeable markdown editor and viewer  
  - optimized table editor and viewer 

- draft
  - inline preview: 边书写边预览，会隐藏实际文本，只预览部分内联元素
  - video/audio
  - paste html into md

- format
  - 一级标题的相互替换，如 `## 标题名` 与 `标题名 ---`
  - 当逗号后紧跟`符号时，每次格式化都会加一个空格
- smart-tab-name
  - small-tab, tiny-tab:: 缩短tab上的标题文字
  - head-tail: 显示标题部分开始和结尾的文字，便于区分
- collapse-to-level
  - toc折叠到2级标题，方便浏览和跳转
  - 有时候一级标题只有1个总的大标题，此时2级标题才能看到文字结构
- edit
  - 链接预览标题、图片
  - 类似ide的同时打开多标签页并编辑
  - 记住不同tab的上次编辑位置
- copy
  - 复制包含代码的文字时，代码自动加上`符号
- globalOptions
  - defaultViewMode/defaultEditMode
  - indentationSpace
# 本地服务api
- 采用非web方案而在本地开启rest服务可支持的功能
  - 协作冲突处理
  - 本地书签/剪藏服务
# 存储与持久化的问题
- ❓ why choose db instead of files
  - 👉🏻 移动端不需要纯文本文件，桌面端支持export即可
  - 思源笔记已抛弃纯本文而只支持数据库，notable也受到文本困扰而考虑单文件数据库
  - 数据库和本地文件的双向同步很难，db>file简单，file>db需要打开软件或长期后台服务才行
  - 基于文本文件难以实现版本管理
  - 实现双链或分享需要唯一id，数据库更方便
  - 浏览器没有文件系统，使用数据库方便支持更多环境
  - 从数据库读取元数据比本地重新扫描要快得多
  - 附件也支持版本管理
  - windows文件名不区分大小写可能导致跨操作系统产生命名冲突问题
  - 操作系统文件名和路径长度的限制
    - win8实测文件夹与文件名最长244个字符
    - linux实测文件夹与文件名最长255个字符
  - 数据库支持存储更多文本内容无关而样式相关的元数据，如删除、评论与回复

- 本地数据库与本文文件的折中方案
  - 本地保存为文本过于灵活，易损坏格式，折中选择是本地保存为office格式如docx/xlsx
  - db支持导出为文本文件也是一种折中方案
  - 同时支持两种模式也是一种方案，数据库全功能，文本文件有限功能

- 页面id要唯一且稳定
  - 页面内容标题id要稳定，可不全局唯一，但不能依赖标题从上到下顺序，要支持修改标题名后仍然能跳转到对应位置

- 集成第三方同步
  - icloud
  - 坚果云
# dev-to
- [ ] fix: lgt symbol not rendered properly, e.g. `Pick<Props, "name">`.
- [ ] fix: note file name shouldn't change when cut the most front text
- [ ] search: hightlight search results on current page
- [ ] toc: 一级toc目录点击后会切换页面，但toc能保持原位，而不是回到第一项
- [ ] edit: edit at where you click  
- [ ] edit: collapse current node  
- [ ] edit: insert one blank line below  
- [ ] edit-character: special character support, like `「Microsoft Store」`.
  - https://copychar.cc/symbols/
- [ ] edit-emoji: emoji with different theme, 素描线划风格的表情字符
- [ ] edit-list: list symbol to number
- [ ] edit-list: toggle lines to list
  - 直接添加`- `将多行文字里的每行转换成列表中的一项，甚至可以添加`- [ ]`转换成待办事项列表
- [ ] edit: 粘贴后，批量删除中文段落中部分英文单词两边的空格
- [ ] edit: write x to checkbox without deleting following whitespace `- [ ]`.
- [ ] keyboard: alt+arrow, move current line up/down
- [ ] file: 第一次直接使用第一行文字作为标题，之后需要在中间栏修改标题，不能直接在文件中修改标题
# draft
- nice-to-have
  - 该多用一级标题`#`来减少嵌套，与最顶部一级标题作为文档标题并不冲突
    - 可能不符合阅读习惯，比如word中顶部一级标题常用最大号，此处渲染可用代码修改
- table
  - 对于数据对比类的表格，要注明制表日期，方便更新和维护
# requirements
- io模块
- 编辑模块
  - markdown-editor-monaco
  - markdown-editor-lite
- 预览模块
  - toc目录设计成类似书籍目录，单行且缩进，悬停查看完整目录
  - 文字块: Note块，warning块
  - frontmatter: 默认不显示，可选择显示成内容为tag的表格
- 样式
  - link: 网址来源信赖标记，如github这类链接
  - text: 使所有匹配的文字变暗，如链接文字只高亮最后2个单词，前面的 `https://xx.x` 变灰色
  - 格式化时，长数字间的逗号分隔符后不要自动添加空格
- 笔记文件管理模块
  - 按日期
  - 按标签
  - 按文件夹
- 窗口模块
- product形式
  - electron-app
  - vscode-extension
  - mobile-app

- 其他需求
  - 打开一个文档后，标题栏中标题应显示为文档第一行的标题，而不是/path/to/README.md
- discuss
  - markdown顶部元数据采用注释形式，而不是多级键值对
  - 添加快捷键：复制文字的链接url
# [changelog](https://github.com/notable/notable/releases)
- resources
  - https://github.com/notable/notable-insiders/releases

- v1.9.0-beta.10_2022-04-27
  - Editor: added a decoration class for each heading, to be used potentially for styling purposes via some custom CSS
  - Editor: added support for parsing HTML tables in the clipboard as Markdown tables when pasting as Markdown
  - New palette: template
  - PDF preview: added "first page" and "last page" navigation buttons
  - Import: added support for importing ".qmd" files
  - Fuzzy Search: added a fast path for queries that are exact matches from the start of the target string

- v1.9.0-beta.0_2020-12-02
  - New setting: tabs.alwaysVisible
  - Export: added support for targeting different export modes via custom CSS
  - New commands: tag.new.notebook, tag.new.template
  - Docs: refactored and unified documentation notes

- v1.9.0-alpha.0_2020-06-12
  - Most of the app has been completely rewritten
  - Bringing the app closer to supporting plugins
    - Many built-in features are now implemented as internal plugins; 
    - based on VS Code-like primitives like settings, context keys, commands
  - Bringing the app closer to being able to run in the browser and on smartphones
    - Electron's "main" and "renderer" processes have been almost completely decoupled from each other
    - Electron's "renderer" process is close to being completely sandboxed, which would make it not that much different from a regular browser ta
  - With 448 commands, 241 shortcuts, 83 context keys, 177 customizable colors, 19 standalone palettes and 18 context menus implemented
    - The codebase grew from 14k lines of code to 26k lines of code
  - The UI has been redesigned to be cleaner and more pleasant

- v1.8.4_2020-01-22
  - Bundling OS-specific dependencies only when needed
  - Ensuring both creation date and modification date are updated when duplicating a note
  - Multi-cursors: using “Ctrl+MouseEvent” rather than “Alt+MouseEvent” as the latter switches the focus to the menu bar (Windows)

- v1.8.0_2019-11-07
  - Upgraded Electron to v7
  - Rewritten “Select Data Directory...” window as a modal window

- v1.7.0_2019-08-10
  - Added support for adding image attachments via copy and paste
  - Added support for writing footnotes
  - Added support for importing HTML notes

- v1.6.0_2019-07-09
  - Added support for linking to search queries
  - Using natural sorting

- v1.5.0_2019-05-12
  - Upgraded to Electron v5
  - Added context menu actions for copying attachments/tags/notes names
  - Markdown: improved stripping of headers, emojis, images, links, wikilinks and todos

- v1.4.0_2019-03-15
  - 💰 Switched to the AGPL license
  - Added a “Toggle Sidebar” menu entry
  - Search: added a button for clearing the input
  - Replaced CodeMirror with Monaco

- v1.3.0_2019-01-31
  - Added Wiki-style links supports
  - Added support for linking to attachments from `source` elements

- v1.2.0_2019-01-25
  - Added “Undo” and “Redo” to the menu
  - Added basic support for range selection when holding shift key
  - Added a Split-View mode

- v1.1.0_2019-01-04
  - Added KaTeX support
  - Added support for double-click to collapse/expand tags
  - Search: searching notes contents (non fuzzly) too

- v1.0.1_2018-12-27
  - Multi-Editor: improved confirmation messages for adding/removing tags
  - Tagbox: ensuring their never share the same name
  - Tags: updating the tree instead of completely rebuilding it, O(n) -> O(1)
  - Ensuring the special “Tags” tag is collapsible too

- v1.0.0_2018-12-22
  - 支持win/linux/mac
# more
