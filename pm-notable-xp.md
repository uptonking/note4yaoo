---
title: pm-notable-xp
tags: [notable, note-taking, pm, xp]
created: 2020-05-10T07:13:28.652Z
modified: 2021-06-02T18:24:28.052Z
---

# pm-notable-xp
- local/offline first markdown-based note-taking app
# features
- core
  - local/offline/private/privacy first markdown-based note app
    - local note data as first class data source
    - local means personal,born to keep data private,强调数据由用户掌控
    - offline means no ad，强调可通用易移植
    - full control of your data, free for sharing and exporting
    - 如何解决版权问题？只能localize本人的创作
- online sync is optional
- extended markdown support, including GFM/MDX

- toc
  - toc优先采用docked/sticky的设计
    - 因为文章内容较长时，对于随页面滚动的toc会滚动到页面顶部然后消失
- themeable markdown editor and viewer  
  - optimized table editor and viewer 
- don't
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
# xp
- nice-to-have
  - 该多用一级标题`#`来减少嵌套，与最顶部一级标题作为文档标题并不冲突
    - 可能不符合阅读习惯，比如word中顶部一级标题常用最大号，此处渲染可用代码修改
- table
  - 对于数据对比类的表格，要注明制表日期，方便更新和维护
# conpetitive-alternatives
- notion

- [我来](https://www.wolai.com/)
- [从Notion到wolai，这些中文细节优化真是让人心动](https://zhuanlan.zhihu.com/p/346197555)
  - 中文排版优化
    - 会自动在中英文内容插入间隔，插入的间隔并非实际空格，只是样式上的限定
    - 一旦将文字复制或者导出为本地文件，却是没有空格的。
  - 直接粘贴markdown图片格式或者粘贴markdown全部图文，图片都会自动加载
  - wolai的编辑体验最让我印象深刻的是对全角字符的兼容
    - 无论是Notion的快捷输入还是markdown格式，一般都是需要在英文输入状态下支持，因此导致在中文输入中需要频繁切换输入法，
    - 但在wolai中则省事多了，如1。也可以识别为有序列表
  - 对拼音的支持非常好，如[/img], [/tupian], [/tp]
  - 支持右侧显示悬浮目录，在窄屏会显示小黑条
  - 多媒体内容与国内服务商结合紧密，特别是视频、地图
  - 表头提供了免费授权的背景图
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
# experimental
- [interactive notebooks](https://nteract.io/)
  - We build SDKs, applications, and libraries that help you and your team make the most of interactive (particularly Jupyter) notebooks and REPL.
# notable

## notable-xp-todo

- [ ] fix: lgt symbol not rendered properly, e.g. `Pick<Props, "name">`
- [ ] fix: note file name shouldn't change when cut the most front text
- [ ] search: hightlight search results on current page
- [ ] toc: 一级toc目录点击后会切换页面，但toc能保持原位，而不是回到第一项
- [ ] edit: edit at where you click  
- [ ] edit: collapse current node  
- [ ] edit: insert one blank line below  
- [ ] edit-character: special character support, like `「Microsoft Store」`
  - https://copychar.cc/symbols/
- [ ] edit-emoji: emoji with different theme, 素描线划风格的表情字符
- [ ] edit-list: list symbol to number
- [ ] edit-list: toggle lines to list
  - 直接添加`- `将多行文字里的每行转换成列表中的一项，甚至可以添加`- [ ]`转换成待办事项列表
- [ ] edit: 粘贴后，批量删除中文段落中部分英文单词两边的空格
- [ ] edit: write x to checkbox without deleting following whitespace `- [ ]`
- [ ] keyboard: alt+arrow, move current line up/down
- [ ] file: 第一次直接使用第一行文字作为标题，之后需要在中间栏修改标题，不能直接在文件中修改标题

## notable-docs

- The data directory is where all your notes and attachments will be stored
  - You can edit your notes/attachments without even using Notable
  - you could also import a Markdown note simply by copying it into the `notes` directory.
- The sidebar is where all your notes are categorized.
  - All Notes: contains all notes
  - Favorites: fixed menu    
  - Tags: all notes tagged with any tag except the special ones: `Notebooks/*` and `Templates/*`
      - You can create sub-categories in the following sections: Notebooks, Tags and Templates by using nested tags. 
  - Untagged: notes that have no tags
  - Trash: notes that have been deleted. 
      - These notes won't be displayed in any other category.
  - Notebooks: notes tagged with the special `Notebooks/*` tag
  - Templates: notes tagged with the special `Templates/*` tag. 
      - These notes won't be displayed in any other category.
- The middlebar shows you all notes contained in the currently active category
  - title of notes is searched in fuzzily
  - content of notes is searched in full-match
  - order by title/modified
  - Pinned notes are displayed before the others.
- The mainbar is where you can preview and edit the currently active note
  - The toolbar contains buttons for triggering actions to the current note
- Edit the markdown notes with Monaco Editor
  - a button in the toolbar for opening the current note in the default Markdown editor
  - When 2 or more notes are selected a multi-note editor will be displayed in the mainbar
- Notes are written in GitHub-flavored Markdown
  - Notes can have some metadata: fav/tags
  - syntax features: GFM, KaTex, AsciiMath, mermaid
  - attachments: simply copied into `attachments` sub-directory
- Tags are useful for better categorization
  - Root tags don't contain any forward slash ( `/` )
  - Tags can also be nested like a path
  - tag starting with `Notebooks/` will show in Notebooks section
  - tag starting with `Templates/` will only show in Templates section
- Shortcuts
  - NoteApp/Editor/Nav/Other
- Importing
  - Markdown files: `md`/`mkd`/`mdwn`/`mdown` /`markdown`/`markdn`/`mdtxt`/`mdtext`/`txt`
  - Evernotes' exports with extension: `enex`
  - Alternatively you could also just put your Markdown notes into the `notes` sub-directory 
  - Newly imported tags will be tagged with a special `Import-XXXX` tag
- Multi-Note Editing
  - When 2 or more notes are selected a multi-note editor will be displayed in the mainbar
  - fav/pin/trash/tag/
- Linking Attachments/Notes/Tags
  - Attachments can be rendered inline, linked to, and linked to via a button
      - The `@attachment` token is used for this
  - Notes can be linked to, and linked to via a button. 
      - The `@note` token is used for this. 
      - Wiki-style links are supported too.
  - Tags can be linked to, and linked to via a button. 
      - The `@tag` token is used for this.
- Synchronization
  - third-party service will take care of the synchronization
- Mobile Editing
  - third-party apps for editing Markdown files
  - if you need to change some metadata or add an attachment, but it would be ok most of the times
- Collaborative Editing
  - not planned
- Version Control
  - not planned
- Encrypted Notes
  - third-party program will take care of the encryption
