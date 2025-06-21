---
title: lib-editor-quill-dev
tags: [quill, text-editor]
created: 2023-02-09T18:17:22.759Z
modified: 2023-02-09T18:23:23.288Z
---

# lib-editor-quill-dev

# guide

- pros
  - 提出delta格式表示编辑器的内容和changes, popular delta format

- cons
  - 线性结构查询一个节点的子节点不太方便，但也可通过attributes自定义属性来实现
  - 架构上model和view的更新分离度不够高，存在边更新model边更新view的情况
    - 架构流程不如prosemirror/slate清晰
  - 默认的编辑功能太简陋
    - 不支持拖拽文本改变位置, 默认的contenteditable支持，prosemirror/slate也支持
  - inactive maintainance
  - lack of classic examples and ecosystem: search搜索示例
    - word导入导出,dark-mode
    - comment

- features
  - stable rich text editor
  - ❓ 是否支持batch/transaction

- who is using #quilljs
  - 石墨文档
  - slab, Reedsy
  - ERPNext
  - devextreme-quill
  - Grammarly Editor
  - opentiny/tiny-editor, 作者在华为工作
  - 若依管理系统(quill.v1)
  - more: miro
  - [vaadin rich-text-editor is built with Quill](https://vaadin.com/docs/latest/components/rich-text-editor)

- tips
  - 视图层的实现可参考: wangEditor/typewriter/blocky/autocomplete, 库和应用层有不同
  - 富文本编辑器可看做重设计而不是重逻辑的低代码
  - 定制ui通过bolt/format，定制功能api通过module

- lazy-loading的另一种思路
  - partial-load只加载部分类似redux的actions/ops
# not-yet
- 按下Enter键时，为何selection-change没触发

- y-quill中`quill.setContents(type.toDelta(), this);`第2个参数不能设为ts类型中的`silent`
# draft

- 
- 

- selection
  - 不支持跨单元格选择文本

- copy-paste
  - 粘贴换行符时会拆断表格 `表t1 换行 粘贴文本 换行 表t2`.

- 
- 

- 长文本优化
  - 结合 虚拟渲染 + 数据库sharding
# dev

```JS
// debug
ql.theme.modules
ql.constructor.imports
```

- 按下文本字符键，会先触发selection-change，再触发text-change
- 按下方向键，会触发selection-change, 不会触发text-change
- 按下Enter键，会触发text-change，不会触发selection-change
- Changes to text may cause changes to the selection (ex. typing advances the cursor), however during the `text-change` handler, the selection is not yet updated, and native browser behavior may place it in an inconsistent state. Use `selection-change` or `editor-change` for reliable selection updates.

- 注意子类Blot的`domNode`属性会覆盖父类属性，ts该使用 `declare domNode`

## dev-table

- create-table创建的ops数量为 单元格数量 + 2(表格前换行 + 列数量定义)

```JS
{
  "ops": [{
      "insert": "\n"
    },
    {
      "insert": "\n\n",
      "attributes": {
        "table-col": true
      }
    },
    {
      "insert": "\n",
      "attributes": {
        "table-cell-line": {
          "row": "row-7nos",
          "cell": "cell-4mdr"
        }
      }
    },
    {
      "insert": "\n",
      "attributes": {
        "table-cell-line": {
          "row": "row-7nos",
          "cell": "cell-935t"
        }
      }
    },
  ]
}
```

- 鼠标点击时，光标无法定位到表格左右

## dev-image

- roadmap
  - fix caption add/remove

- firefox

- 
- 

- 优化
  - 优化大量数据的场景，特别是idGenerator

- 鼠标点击时，光标可以定位到图片左右，但chrome的光标高度为图片高，firefox高度为普通文本高

### img-notes

- 对于同一行2张挨着的图片，鼠标无法点击到中间的位置，但左右方向键可以定位到中间位置
  - prosemirror也这样
# more
