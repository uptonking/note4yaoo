---
title: lib-editor-slate-dev-log
tags: [dev-log, slate-editor]
created: 2022-05-15T18:46:55.840Z
modified: 2023-02-05T19:03:12.722Z
---

# lib-editor-slate-dev-log

# guide

- 块级元素前后的光标处理

- table-model
# not-yet

# dev-to
- src
  - createDraft + applyToDraft + finishDraft
  - dirtyPath
# dev-later

# dev-maybe

## model层扁平化

- ❓ 将模型层改为基于扁平key/value + 代表节点关系的map，这样在视图层可以直接getNodeByKey(全表扫面性能比getByPath差)，此时方便实现字段级的crdt，也让持久化层更灵活，无需1:1; 
  - 但旧版slate就是采用key的架构，getByKey底层还是基于getByPath实现
  - key的全量查找没有path快
- v0.50+版本的模型层基于自带节点关系的json，然后在视图层动态添加key，这样op中包含路径关系，方便实现op
- 另一种方案是op.apply时保存会受影响的path+value，这样也可以方便实现字段级crdt
# answers

## noseditor中点击bullet和checkbox list的空白行无法显示光标，数字列表可正常显示光标

- 原因未知，坑能和flex布局相关，zero-width字符的span、div宽度都为0，但数字列表是能正常显示

- 解决方法有2种
- 方法1 通用解法
  - 在零宽字符元素的外层div min-width:1px; 
- 方法2 只针对bullet list
  - 在列表符号后添加空字符''，然后才是列表项内容
# done
- src
  - toSlateRange
  - toDOMRange
