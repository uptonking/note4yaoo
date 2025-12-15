---
title: pm-list-pivot-table-view-table
tags: [pivot-table, pm, table]
created: 2022-12-16T01:52:01.861Z
modified: 2022-12-16T01:52:33.729Z
---

# pm-list-pivot-table-view-table

# guide

- 多维表格的使用场景
  - 充分考虑github实现的业务，如何将任务管理project、issues、discussions关联

- table-usage
  - csv常作为基于文本的表格的一种形式

- roadmap
  - in-memory > virtual-render > on-demand
# [obsidian-bases](https://help.obsidian.md/bases)
- pros
  - 基于文件和简单markdown语法实现
- cons
  - name列的内容不能重复
  - undo/redo在删除一行后不能恢复一行
# features
- ai
  - 针对系统级数据库和用户数据建表优化, 使用llm生成sql来执行查询, 是database的下一代产品

- facets/multi-tables

- table-in-table
  - 加强版支持类似lod的效果，显示表中细节
  - [Bootstrap Table Examples - Sub Table](https://examples.bootstrap-table.com/#welcomes/sub-table.html)

- search-view
# usecase
- 文件列表及搜索，很适合切换为多维表格的交互
# table-in-editor
- [CKEditor 5 table](https://ckeditor.com/docs/ckeditor5/latest/features/table.html)
  - 行列操作在悬浮工具条的二级菜单

- [Atlaskit editor with (huge) table](https://atlaskit.atlassian.com/examples/editor/editor-core/kitchen-sink)
  - 每个单元格右上角提供了行列操作菜单
  - 光标在表格内时会显示表格悬浮工具条

- [tiptap table](https://tiptap.dev/examples/tables)
  - 支持合并单元格
  - 支持拖拽修改列宽度
  - 提供了很多commands
  - 暂未提供悬浮工具条

- [plate table](https://plate.udecode.io/docs/plugins/table)
  - 光标在表格内时会显示表格悬浮工具条，如删除

- [lexical-editor](https://playground.lexical.dev/)
  - 光标在表格内时会显示表格悬浮工具条
  - 提供了2版table
  - 新版table
    - 默认支持sort, filter开发中
    - 点击单元格时默认是先选中单元格，而不是直接编辑单元格

- [tinymce table](https://www.tiny.cloud/docs/tinymce/6/full-featured-premium-demo/)
  - 光标在表格内时会显示表格悬浮工具条，如行列操作
  - 支持拖拽修改列宽度

## table-products

- 表格单元格的选区
  - 飞书通过浅蓝背景色
  - notion通过蓝色边框

- 行高可以通过列宽调整
  - 飞书编辑器表格
  - notion

- 单元格 悬浮工具条
  - 飞书将工具按钮显示在单元格左边那格
  - notion将工具按钮显示在行首和列首

- 单元格 合并拆分
  - 飞书支持合并cells，
    - 鼠标从左上到右下可触发选中合并后的单元格，然后可以在单元格悬浮工具条拆分单元格
    - 拆分后的单元格内容不能还原，内容都在第一个单元格
  - notion不支持合并单元格

- 单元格enter键
  - notion焦点移到下一行
  - 飞书、ckeditor、tiptap都是单元格内新加一行
# draft
- 细粒度的权限，可遮挡价格/电话
# examples-

# maybe
- copy column data
# more

# discuss-table-ux/styling

- ## 

- ## 

- ## [conditional colors on single cells (not entire entry lines) : r/Notion _202511](https://www.reddit.com/r/Notion/comments/1oq3mxd/conditional_colors_on_single_cells_not_entire/)
  - I have a database and I want every cell to have a color if >48 green and <48 red.

- I don’t believe that that is something that Notion can do currently.

- A clunky but possible version would be adding an additional formula property for each property that you want to have this kind of color coating for. 

- Currently not possible for manually entered information. We can give formula outputs a colored background and that is it.

- I agree that this should be implemented. Conditional styling at the database level for rows and at the property level for individual cells (which would also make column colors very easy)
# discuss-table
- ## 

- ## 

- ## 

- ## 💫 Animated Inline Table - Made with Tailwind and Framer Motion.
- https://x.com/ln_dev7/status/1920152796566827366
  - [Inline Table Control Interaction | lndev/ui](https://ui.lndev.me/components/inline-table-control-interaction)

- https://x.com/Lakbychance/status/1914356154660221409
  - I implemented the same here.
  - https://github.com/lakbychance/animations
  - https://animations-lak.vercel.app/inline-table-control

- https://x.com/nitishkmrk/status/1913483954646139265
- This is really interesting, the pencil icon expands the row. I was expecting the table cells to become editable. 
  - inline edit is much easier
- This will work great on mobile where the table header might not be available. Desktop might be an overkill
- By the time user is making the decision to edit, they already know what column is what. Maybe inline editing won’t make the content switch.

- 🤼 Give me one reason why you need this fancy useless shift instead of having simple inline editing?
  - Why not make cells editable immediately, without transforming them into a form? Why is this interaction necessary?
- Because cell editing is for Excel and forms are for the web. What if you want form validation? Now, you have to create a hybrid solution that makes a row behave like a form. And you have to make it accessible.

- ## Learned a cool formula style from reddit
- https://x.com/NotionKristen/status/1900728669641076995
  - 自定义百分比的渲染方式

- ## 🌰 [Linear on X: "How we redesigned the Linear UI (part Ⅱ)  _202403](https://twitter.com/linear/status/1773435685275328542)
- 
- 

- ## 🪧 Data table features tree cheatsheet
- https://twitter.com/101babich/status/1768612940217786754
  - This cheatsheet will help you choose all the features for your complex data table
  - [How To Architect A Complex Web Table — Smashing Magazine _201902](https://www.smashingmagazine.com/2019/02/complex-web-tables/)

- ## [UI considerations for designing large data tables | Hacker News_202401](https://news.ycombinator.com/item?id=38942439)
- ag-grid is pretty great at all of this. 
  - we're using it to infinite scroll / sort / filter a table with 3.2M rows of data and it 'just works'
  - 3.2M rows are not loading into the browser at once, only about 10k. The page size is configurable. The frontend and backend have a contract to agree on how this works, so as the user scrolls (and frontend needs another page) it asks the backend for more. The frontend will keep up to N pages (also configurable) cached in the client. 
- This is exactly what AG Grid Server Side Row Model is designed for. 

- Wish HTML tables supported basic grid features like column pinning. Sadly you have to resort to bypassing table and instead use divs.
