---
title: ing-solution-noter
tags: [note, pm, solution]
created: '2020-05-10T07:13:28.652Z'
modified: '2020-07-14T10:24:54.328Z'
---

# ing-solution-noter

- local/offline first markdown-based note app

## noter-features-亮点

- core
  - local/offline/private/privacy first markdown-based note app
    - offline means no ad，强调数据由用户完全掌控
    - full control of your note data, born to keep data private
    - online sync is optional
    - extended md support, including GFM
- themeable markdown editor and viewer  
  - optimized table editor and viewer 
- don't
  - inline preview: 边书写边预览，会隐藏实际文本，只预览部分内联元素
  - video/audio 
  - paste html into md
- rfc
  - format: 一级标题的相互替换，如 `### 标题名` 与 `标题名 ---`
  - smart-tab-name
    - small-tab,tiny-tab:: 缩短tab上的标题文字
    - head-tail:显示标题部分开始和结尾的文字，便于区分
  - collapse-to-level
    - toc折叠到2级标题，方便浏览和跳转
    - 有时候一级标题只有1个总的大标题，此时2级标题才能看到文字结构
- edit
  - 链接预览标题、图片
  - 类似ide的同时打开多标签页并编辑
  - 记住不同tab的上次编辑位置
- globalOptions
  - defaultViewMode/defaultEditMode
  - indentationSpace

## noter-requirements-需求

- io模块
- 编辑模块
  - markdown-editor-monaco
  - markdown-editor-lite
- 预览模块
  - toc目录设计成类似书籍目录，单行且缩进，悬停查看完整目录
  - 文字块: Note块，warning块
- 样式
  - link: 网址来源信赖标记，如github这类链接
  - text: 使所有匹配的文字变暗，如链接文字只高亮最后2个单词，前面的 `https://xx.x` 变灰色
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

## notable

### notable-xp-todo

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
- [ ] edit: 粘贴后，批量删除中文段落中部分英文单词两边的空格
- [ ] edit: write x to checkbox without deleting following whitespace `- [ ]`
- [ ] keyboard: alt+arrow, move current line up/down
- [ ] file: 第一次直接使用第一行文字作为标题，之后需要在中间栏修改标题，不能直接在文件中修改标题

### notable-docs

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
  - Markdown files: `md` , `mkd` , `mdwn` , `mdown` , `markdown` , `markdn` , `mdtxt` , `mdtext` or `txt`
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
