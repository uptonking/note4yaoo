---
title: lib-db-linvodb-codebase
tags: [codebase, linvodb]
created: 2023-01-09T16:29:24.473Z
modified: 2023-01-09T16:29:46.049Z
---

# lib-db-linvodb-codebase

# guide

# not-yet
- update是基于insert实现，作者表示wonky ?

- ❓ 怪异的执行顺序
  - 代码中update操作然后remove，实际上update操作的cb比remove操作的cb后执行
  - 代码中先 insert>update, 但cb顺序update>insert
  - save方法的callback是在insert-cb和find-cb之后执行的

- 为什么使用 bagpipe+async，是否双重异步
  - bagpipe的push方法执行时都是setTimeout
# codebase
- schema的作用
  - 在初始化Model时，生成构建索引的options

- 从db查找对象时，会先在Model的dml方法中注册ids/data/ready事件，然后在Cursor.getMatchesStream中触发相应的事件
  - 在Cursor.getMatchesStream中触发ids，在Cursor.retriever取完数据触发data
  - data/ready都在ids事件内部
  - 在Model的dml方法中注册ids/data/ready事件
    - cursor.exec中注册了ids/data/ready
  - 在Cursor中触发相应的事件
    - 触发ids
      - 在Cursor.getMatchesStream中Cursor.getIdsForQuery找到ids
      - 在Cursor.getMatchesStream中buildIndexes完成后的回调找到ids
      - 在Cursor.getMatchesStream的最后注册ids事件
    - Cursor.retriever触发data
    - 触发ready
      - 在Cursor.getMatchesStream的参数收到ids
      - 在Cursor.retriever的cb

- 在insert和find的过程中，都有  Cursor.getMatchesStream

- ？ insert只插入了一个对象(是否1次)，但get能返回2个对象
  - 分析错了，上次保存的数据未及时清理

## indexes 索引 avl-tree

- 使用旧版构造函数初始化时传入数据，buildIndexes得到的单节点avl
  - 为什么根节点为空，且高度为2
  - root(data=[])
    - left(null)
    - right(data=key=_id)
      - left=null
      - right=null
# code-faq
- insert方法插入`_id`相同的对象时，如从序列化字符串中拷贝出对象，能正常插入吗
  - nedb不能正常插入 Can't insert key xxx, it violates the unique constraint
  - linvodb的测试也会抛出异常
