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
# dev-to
- src
  - createDraft + applyToDraft + finishDraft
  - dirtyPath
# dev-later

# dev-maybe

- ❓ 将模型层改为基于扁平key/value + 代表节点关系的map，这样在视图层可以直接getNodeByKey(全表扫面性能比getByPath差)，此时方便实现字段级的crdt，也让持久化层更灵活，无需1:1
  - 当前版本的模型层基于自带节点关系的json，然后在视图层动态添加key，这样op中包含路径关系，方便实现op
  - 另一种方案是op.apply时保存会受影响的path+value，这样也可以方便实现字段级crdt
# done
- src
  - toSlateRange
  - toDOMRange
