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
# notable-community
- ## At the moment I'm leaning toward a sort of hybrid approach:
- https://discord.com/channels/715934079559663646/720653307747500092/969614509037744258
1. 使用本地数据库抹平不同操作系统文件读写操作的差异。The app would work with a single-file database and most of its codebase would only know about that, all the differences between Windows and Linux/Mac filesystems would be abstracted away, all the ugliness of the filesystem for most of the codebase would be just a sad memory.
2. 本地数据库和本地文件双向同步。The app would also have a little program, enabled only in the Electron app, that keeps the single-file database and the files on disk in sync, so that if the database changes the filesystem is updated and vice versa.
3. 新笔记只使用本地数据库。In new data directories, those for which a database can't be found, the app simply asks the user if they want to make a new database with the files in that folder, perhaps providing a list of them so that the user can double check it.
4. Potentially an option for disabling filesystem synchronization could be implemented, in which case the database would be all there is, with options for exporting everything and for turning synchronization back on and all that of course.
5. Potentially a database could be opened directly by the app, so that one could share entire data directories and all their metadata that way.
6. The mobile and web apps would only know about the single-file database.
7. Potentially the app could not touch the metadata section for any note, and some things will work less reliably, with an option for explicitly telling it to write either only the ID or other kind of metadata too into the metadata section.
-----
- Does this sound reasonable? I think something like this is needed because where is the mobile/web app going to store its data? We need something that works in the browser too, and we need something where things like revisions can be stored without (unreliably) writing a million individual files to disk. Also with a couple of settings this gives people the option to throw away the filesystem for the most part and switch to single-file databases entirely, which some people may be interested in. At the same time all files would still be synchronized with the disk and editable directly as regular files, git can be run on top of that and everything else, for people that want that

- I don't see why we really have to get rid of the current approach, isn't the yaml meta data is actually a rather nice solution at the moment? The only thing I really dislike is that it gets added/changed even if I only view the files
  - So apart from the additional effort for adding case distinctions, is there another reason why my suggestion (adding the meta data only when changes are made or when absolutely necessary) would not work?
  Like for example:
  1. Sync is enabled: Add UUID  (and other meta data) to all notes. (Might also be implicitly done by "3.")
  2. Note is changed: Add UUID (and other meta data) to the current note
  3. Actions such as Copy-UUID-Link make use of any internal function, e.g. note.getUUID(). If note.uuid is null, a new UUID will be generated and added to the note's meta data, otherwise the UUID from meta data is returned.
- It's an ok solution for that the app does at the moment, but other than the increased number of bytes stored on disk what's another disadvantage of what I'm proposing?
  - This is doable, although as I said in the past writing the UUID only when some set of complicated conditions are met sounds like a nightmare to me, and I'm not really looking forward to writing the code for that. But also that's only part of the problem, the app has to run in the browser too, there's no filesystem in the browser, so an abstraction layer for that has to be written in any case I think.
- So basically, the app stores all its data in this database, and in desktop environments it will also sync it with an on-disk directory that mirrors the data in the DB? 
  - Even just considering the desktop app though storing revisions as individual files would be a nightmare, just to mention one thing
- Basically it would work the same as far as the user in concerned, but the code for the app should get a lot cleaner, there would be an extra file in each data directory storing all the data plus other metadata like revisions, there would be some reliability and performance advantages, like if notes are read from a single-file database the app can open up in milliseconds even if you have millions of files, and the app would also be much closer to being able to run in the browser, as there the ~only difference would be that the filesystem synchronizer is swapped with the cloud synchronizer, as far as the rest of the codebase is concerned nothing else changed (database-wise)
- I'm guessing that the database only stores note data, and attachments are still in a separate folder
  - It would store attachments too otherwise it wouldn't be able to synchronize them or to keep revisions for them

- ❓ this may be a misstep because in some sense it pushes the app closer to locking your content into a proprietary database, 
  - but like I don't want that to happen and if my "successor" goes for that anyway you'll still have your notes on disk and able to move anywhere else potentially. 
  - And something like this is needed both to cleanup the codebase and to have the app working everywhere, my main doubts are like how should the metadata section written on disk be handled? and is SQLite the right choice for something like this? 
- Metadata is a feature from my perspective, provides a sane way to store useful info I want to know. You could move it into the app and just make it something optionally added?
  - eah it could be written optionally potentially. The main problems are: should it never be written by default? Should the ID always be written? How problematic would it be to not have reliable IDs for notes? If the metadata section is written what should be written in it? Like things like the IDs of revisions, or the ID of shares or maybe metadata that some extension wrote shouldn't be there, it's unclear.
- Code shouldn't be written that way, things internally already have UUIDs, you need something to identify things, it becomes a mess if you don't even have guarantees like "things have unique UUIDs", the burden of what you are proposing is having some system that decides if UUID should be written to disk or not, which means everywhere you rely on UUIDs (which is everywhere) now you need to think "Do I want my usage of the UUID to cause the UUID to be written to disk or not?" And like almost no code in the codebase should even know that there's a disk to begin with, I don't see how to implement this in a non super messy way, and I don't really see the entire point of it either, like either UUIDs are written to disk or they are not, do we really want some notes to have them and some to not have them? That just sounds like a mess to me.
- Code shouldn't be written that way, things internally already have UUIDs, you need something to identify things, it becomes a mess if you don't even have guarantees like "things have unique UUIDs", the burden of what you are proposing is having some system that decides if UUID should be written to disk or not, which means everywhere you rely on UUIDs (which is everywhere) now you need to think "Do I want my usage of the UUID to cause the UUID to be written to disk or not?" And like almost no code in the codebase should even know that there's a disk to begin with, I don't see how to implement this in a non super messy way, and I don't really see the entire point of it either, like either UUIDs are written to disk or they are not, do we really want some notes to have them and some to not have them? That just sounds like a mess to me.
- it would be simpler if the app could make the assumptions that notes on disk come with a UUID or that if they don't have one one can be assigned to them and that won't change across restarts. But as I mentioned in my previous comment I think it's not strictly necessary to have this. The app could check hashes, file names, things like that. 

- The internal ids change each time the window is re-opened, so you probably don't want to use that anyway, those IDs should become public though at some point, 

- ## I think there should be an option to not create any metatag headers if not necessary, and/or to disable the "modified" field:
- https://discord.com/channels/715934079559663646/721056044784025653/930486158440407111
- As long as no custom title is used and no tags etc. are applied, metadata are not really required (created and modified date could be read from the file system instead)
  - Once Notable allows opening arbitrary .md files outside of data directories, this is a must-have feature imo
  - Furthermore, metadata should only be written if the note is changed or if it already contains a metadata header, but not if a file without metadata is only opened for reading. Or with other words: It should be possible to read (rendered) notes without modifying them at all (like a read-only mode that is not enforced)

- 👉🏻 This discussion should be held keeping in mind that each note in a data directory should have an ID associated with it for synchronization, version control, and possibly linking purposes too. The current situation where notes in a data directory don't have IDs is temporary and consequently largely irrelevant.
  - An ID is always needed for notes in a data directory for synchronization etc. For standalone notes sure, a metadata section shouldn't be written. Also polling the filesystem for things like the last modification date is unreliable, slower, and doesn't make sense to begin with in a browser context (currently the app runs only on desktop, sure, but if the desktop app infers those values what is the web app going to do with your notes once you have them synchronized and decide you want to use the app on the browser?)
  - It should be noted that you largely don't need IDs to tell your notes apart, so hypothetically neither the app should need them in the vast majority of cases, but I don't know how to code that
- If I use synchronization - then yes, id/that's needed. But please keep in mind, that there will be plenty of use cases, where either no synchronization is used, or the user uses his own tool (either Dropbox/OneDrive etc. sync, or a VCS as GIT). In those cases, the ID would only be needed for linking purposes. If not, metatadata generation could still be omitted. E.g., the UUID could only be generated if explicitly needed (sync activated, or a command that requires a UUID (like "copy-uuid-link" or so) is called). 
- Reliable links: even if you link to other notes in a spec-compliant way if each note has an ID associated with it then the app could keep some metadata about them under the hood, so that if you move notes around or edit them lightly it can fix broken links for you. Now I think that's obviously a desirable feature to have. Should the app then start adding IDs to every note that's linked from another note? I mean the situation gets messy quickly here. How many people even have only notes without links to any other note (or attachment) and/or they want links to break.
- Sharing: the assumption that things have IDs is pretty fundamental in many areas, under the hood the app is already assigning IDs to everything otherwise they would be a mess to manage. For sharing in particular for example if a note doesn't have an ID you might have to special-case the logic for sharing it. If a note doesn't have an ID you need to put the ID of each share in the metadata section as you can't link it to the note reliably otherwise, hence you need a metadata section anyway. 

- There are various ways to tackle the problem, assuming notes and attachments are stored as plain files on disk as otherwise the problem is trivial to solve. Notes could have an ID and that could be used for linking, that would work for notes, if you don't manually edit the IDs for some reason, but the links in the editor would get unreadable if just the ID is used for them, and that wouldn't be compatible with other apps as there's no standard way to do this. Attachments would still remain a problem though, as it's impossible to stick an ID to each of them, whatever binary format they are using it just doesn't support that, in general. Another potentially complementary approach is kind of storing some metadata about every link, and using that when they break to find where the thing they were pointing to might be now, the problem with that is that's complicated, it's impossible to make it work 100% of the time, and there would probably be the need to prompt the user for a confirmation before rewriting stuff automatically, since the system wouldn't be infallible, and it's probably better to have a link pointing to nothing (obviously broken) than a link pointing to the wrong thing (subtlety broken), an upside would be that that could work with regular links too though. 
- As I understand, obsidian are doing some all-notes-scanning at first time open and put metadata into .obsidian folder at root folder. And I assume that they save and load info about links between notes and attachments. So easiest way to do change-link-on-rename is to store name and links from all notes and then search links for renaming note and change these links.
  - Storing some metadata is not the complicated part, reliably finding back files that changed is the complicated part, like in your example let's say I rename an attachment and then I open the app, how would I fix all links pointing to that attachment? It's doable but it's not easy to do well
  - without a system for rewriting links automatically renaming notes just breaks links... There's a command that will generate a list of all detected broken links, it's something like "Report: Broken Links" in the command palette, better than nothing for now.
- is there a way to link to a certain part of a note? 
  - You can use fragments as urls just the same, though only ids in the same note can currently be linked to, if you right-click on an heading inside a note there's an option for retrieving a link that targets that

- I'm trying to implement a way to link notes that doesn't break when I change the notes' title/name. 
  - Not possible yet, sorry__20220505
  - But actually, depending on how much you want this, you can now disable automatically renaming notes, you can give your notes unique file names manually, then you can just use those as the unique identifiers

- in the future I'd want to store the ID of the note in the metadata section for synchronization, versioning and reliable linking purposes
- https://discord.com/channels/715934079559663646/720653307747500092/969601322292756490 __20220429
  - I think there's no alternative to writing a metadata section automatically?
- You could just ignore notes that don't already have notable metadata, and have a way to explicitly import them?
# notable-docs-xp

## notable-xp-dev-to

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

## docs

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
