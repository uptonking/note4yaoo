---
title: lib-excel-focalboard-codebase
tags: [codebase, focalboard]
created: 2022-03-16T20:47:15.710Z
modified: 2022-08-21T09:56:38.596Z
---

# lib-excel-focalboard-codebase

# guide

- 前端webapp开发历史记录
  - https://github.com/mattermost/focalboard/commits/main/webapp/src

- xp
  - 桌面版不支持share，但web版支持share
# roadmap
- theme
- 支持 notion/airtable
# design
- focalboard底层数据库设计包括 blocks/boards
  - block表拥有 boardId 属性与业务关联，还有type/fields
  - board表不直接与block相关，通过props和cardProps描述内容
# faq
- 删除或编辑卡片的操作，状态是如何变化、更新的？
  - 数据操作通过调用全局的mutator方法
# 多维表格相关
- 视图切换原理
  - `activeView.fields.viewType` 支持 kanban/table/calendar/gallery 4种视图

- 多维表格视图入口 CenterPanel
  - 定义了会传给所有视图进行数据更新的方法，如addCard
    - kanban视图添加卡片会执行 addCard
    - table视图添加行会执行 addCard
    - 注意onClick方法里执行addCard时传入的参数不同

- 多维表格各种视图的前端实现入口在 src/components/centerPanel.tsx
  - TopBar 最顶部，不能算作导航条，只有feedback/help
  - PageTitle
    - left: ViewTitle 页面标题、描述
    - right: ShareBoardButton
  - ViewHeader 多维表格的公共工具条组件
    - 所有视图共用的工具条组件
    - 左边是多种视图切换
    - 右边是全局排序、过滤、分组工具
    - view dropdown with Editable view name 视图下拉列表
    - ViewHeaderPropertiesMenu 所有字段
    - ViewHeaderGroupByMenu 分组
      - ViewHeaderDisplayByMenu GroupName
    - FilterComponent 过滤
    - ViewHeaderSortMenu 排序
    - ViewHeaderSearch 搜索
    - ViewHeaderActionsMenu more actions
      - export .csv/.archive
    - NewCardButton add new row
      - new template (card)
      - insert card/row from template
  - view Kanban
  - view Table
  - view CalendarFullView
  - view Gallery

## Kanban jsx vdom

- 实现细节
  - 卡片拖动时，放置位置高亮预览很方便，拖动时高亮哪一张卡片最后就会插入到某个位置
    - 拖到一列末尾时就没有高亮，因为如果高亮在最后一个，则会插入到倒数第2个位置
  - 不能直接拖到最右边 add a group 那个空列
    - notion也不能直接拖到最右边添加新列

- 👉🏻 顶层是 scrolling div
  - 未考虑一个页面多个表格的情况

- 👉🏻 kanban-header 所有列的标题
  - visible KanbanColumnHeader 每列标题
  - hidden columns 所有被隐藏的列作为单独列
  - add group button 添加列

- 👉🏻 kanban-body 所有列的卡片组
  - visible KanbanColumn 每列所有卡片
    - KanbanCard
    - new card 添加卡片
  - hidden columns
    - KanbanHiddenColumnItem

- KanbanColumn
- 一个简单的容器div

- KanbanCard
  - 状态管理
    - 会从 useAppSelector 中获取全局数据
    - 全局的数据操作通过调用全局的mutator方法
  - 操作菜单工具条
    - 删除、重复、复制链接
  - card icon + title
  - visiblePropertyTemplates => PropertyValueElement
  - CardBadges
  - OpenCardTourStep / CopyLinkTourStep

## Table jsx vdom

- 👉🏻 顶层是 ColumnResizeProvider
  - 传入 更新方法、cellRef、updateRef

- 👉🏻 TableHeaders 标题行，包含所有列的标题
- 👉🏻 表格内容行
  - TableGroup Rows
  - No Grouping Rows
- 👉🏻 Add New Row 最下面一行
- 👉🏻 CalculationRow
- 👉🏻 HiddenCardCount

- table-cons
  - 不支持删除行
# data-fetching
- 表格中修改行数据时，只触发一个http请求
  - /api/v2/boards/boardId/blocks/cardId
  - 修改数据的请求方法类型是 PATCH，而不是 POST

- 依赖多个全局工具类的实例
- `Mutator` is used to make all changes to server state; 
  - It also ensures that the Undo-manager is called for each action
  - 前端操作基本都借助undoManager实现
- `UndoManager` General-purpose undo manager
  - 每个action都抽象为一个 UndoCommand，使用数组保存所有 UndoCommand
  - perform方法，先执行redo，再注册undo，最后返回redo方法的返回值
  - execute方法，执行command，并保存结果到command对象
- `OctoClient` is the client interface to the server APIs
  - 更新block数据依赖 OctoClient
  - 服务端api对应的前端请求工具类
  - 这里定义了这个操作的url: const path = '/api/v2/login'
# state-management
- 💡 典型的数据更新流程
  - 先执行http请求，触发服务端数据更新
  - 等服务端更新完成后，再在 `afterRedo` 方法中传入服务端返回的最新数据，更新前端redux数据
# codebase
- 前端整体结构
  - MainApp 传入reduxStore、处理用户初始化、首次连接websocket
  - App 准备ui相关Provider数据，IntlProvider/DndProvider
  - Router 基于路由守备定义了核心ui与路由对应的结构
    - /:boardId?/:viewId?/:cardId?
    - 所有核心路由对应的视图组件统一都是 `<BoardPage />` 组件
    - 路由导致的变化，最后都会先在本组件处理，如更新数据

- webapp/src/pages/boardPage/boardPage.tsx 
  - 作为Workspace的入口
  - 注册了websocket事件处理函数、undo/redo快捷键
- Workspace
  - 定义了核心视图的左右布局，左侧边栏展示视图列表，右侧内容区展示表格等视图
  - CenterContent会渲染多维表格的核心视图组件 CenterPanel
    - 这里从全局store中取出了核心数据 board、cards、activeView、groupByProperty、views
# 桌面版 b/s架构
- windows基于wpf、c#、WebView2简单封装
  - Windows Personal Desktop packages a lightweight C# Windows App with the Windows build of the server, and the webapp. 
  - The server is run in a single-user mode.
  - 启动服务端的代码 `DllImport(@"focalboard-server.dll"`

- linux版基于webview简单封装
  - runServer(port)
  - w := webview. New(debug)
  - `w.Navigate(fmt.Sprintf("http://localhost:%d", port))`

- mac版基于swift简单封装
  - WKWebView
