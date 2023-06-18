---
title: lib-excel-tanstack-table-dev-log
tags: [dev-log, dev-xp, tanstack-table]
created: 2023-06-17T14:10:53.128Z
modified: 2023-06-17T14:11:16.672Z
---

# lib-excel-tanstack-table-dev-log

# guide

- ideas
  - 似乎将ospreadsheet的ot去掉就是基于llw的协作了，可复用undo/branch，需要调整crud的op
# not-yet

# architecture
- tanstack-table的设计偏向以react state作为唯一数据源
  - 每次编辑会更新react state中的数据，然后触发全量rerender

- feature代码量较少的
  - columnVisibility
  - Expanding
  - Pagination
  - columnOrddering
# dev-log
- createTable计算得到的table对象与视图无关，可在视图渲染前计算视图相关数据
# answers
- 为什么watarble里的table实例只执行getRowModel，而未执行 getSortedRowModel
  - 因为options未传入 getSortedRowModel，copy代码时要检查
# more
- 参考useReactTable的实现，每次执行改hook时，会执行setOptions更新table实例的配置
  - 自己封装时，也要在createTable后立即setOptions
