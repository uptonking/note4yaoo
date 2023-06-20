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
- 设置了自定义onSortingChange后，默认的onStateChange就被覆盖不会触发了，要注意具体分析实现细节
  - 自定义插件的onChange不会触发table.onStateChange，但不自定义时就会执行默认的，这里是2选1，要做取舍

- 👉🏻 table-sort有2种实现思路
  - 一种是不使用onSortingChange，以sortPlugin作为数据源，先dispatch手动更新sortState，再手动将最新sortState合并到tableState，sort数据独立操作
    - 优点是可定制性强，缺点是需要自己确定排序算法和顺序问题
  - 另一种是使用onSortingChange，直接获取tanstack最新sort的状态值，然后将tableState最新状态同步到自己的sortPlugin，sort数据以tableState作为数据源
    - 优点是大部分逻辑直接使用tanstack-table

- createTable计算得到的table对象与视图无关，可在视图渲染前计算视图相关数据
# answers
- 为什么watarble里的table实例只执行getRowModel，而未执行 getSortedRowModel
  - 因为options未传入 getSortedRowModel，copy代码时要检查
# more
- 参考useReactTable的实现，每次执行改hook时，会执行setOptions更新table实例的配置
  - 自己封装时，也要在createTable后立即setOptions
