---
title: spec-format-json-patch
tags: [json-patch]
created: 2023-02-26T21:03:46.978Z
modified: 2023-02-26T21:03:56.167Z
---

# spec-format-json-patch

# guide
- [JSON Patch | jsonpatch.com](https://jsonpatch.com/)
  - JSON Pointer (IETF RFC 6901) defines a string format for identifying a specific value within a JSON document. 
  - It is used by all operations in JSON Patch to specify the part of the document to operate on.

- [RFC 6902: JavaScript Object Notation (JSON) Patch](https://www.rfc-editor.org/rfc/rfc6902)

- json-patch未解决的问题
  - 给内层数组添加元素时，该元素后面所有元素会更新
# typewriter-json-patch
- sync实现要点
  - client发送内容op/patch/changes, 发送时机，接收内容
  - server接收，发送内容

## syncable

- It works by using metadata to track the current revision of the object, 
  - any outstanding changes needing to be sent to the server from the client, 
  - and the revisions of each added value on the server so that one may get all changes since the last revision was synced.
  - The metadata must be stored with the rest of the object to work.

- It does not handle adding/removing array items, though entire arrays can be set. 
  - It should work great for documents that don't need merging text like Figma 

- changesSince会保存各个字段的最新值

- 元数据

```JS
// 客户端
{ rev: '07' }

// 服务端
{ rev: '07', paths: { '/ticker': '4', '/content': '07' } }
```

- 客户端发送给服务端 json-patch

```JS
 [{ op: 'replace', path: '/content', value: 0.3967347015756624 }]
```

- 服务端发送给客户端

```JSON
{
  "patch": [{
    "op": "replace",
    "path": "/content",
    "value": 0.4283930603719077
  }],
  "rev": "07"
}
```

# blogs

## [JSON Patch](https://atbug.com/json-patch/)

- JSON Path是一直描述JSON文档变化的格式, 使用它可以避免在只需要修改某一部分的时候发送整个文档内容
  - 当与HTTP PATCH方法混合使用的时候, 它允许在标准规范的基础上使用HTTP APIs进行部分更新

## [Kubernetes中的JSON patch - 掘金](https://juejin.cn/post/6993618347904466957)

- JSON格式文件改动的方案有很多，但是被IEFT官方收录的就两种
  - RFC 6902（JSON Patch）
  - RFC 7396（JSON Merge Patch）

### JSON Patch

- 它适用于 HTTP PATCH 方法，相当于这个方案扩展了http协议，比如 “application/JSON-patch+JSON”的meme.type就是用于标识此类Patch文档，它所定义的参数结构中包含对资源执行部分修改的方法。
- “op”表示操作，有“test”，“remove”，“add”，“replace”，“move”，“copy”这六种操作。
- “path”表示该操作指向JSON文档的目标
- “value”表示操作的具体的值
- 其中比较特殊的是“test"，简单来说他就是"equal"，比较值或JSON Object。
- 根据http patch原子性的定义，原子性的含义就是以下操作不会对源文档产生修改，因为“test”会失败，而整个操作附带“replace”操作也会回滚。
- 规范定义了如果一次JSON Patch操作违反了规范要求，或者操作不成功，则会终止对JSON文档的操作，且视为操作不成功。这里可以参考http patch操作的状态码。

### JSON Merge Patch

- JSON Merge Patch和JSON Patch很像，但是他描述了JSON文档更改的版本。
  - 与上文提到的方式相比，这种方式更像git中的差异文件，而JSON PATH更像操作数据库。
  - 这种方式不包含操作，只包含文档的节点。
- 这种方式一看就很易于理解，但是有一些潜在的限制，比如
  - 没办法将value置为null，因为null的操作在merge patch的场景下是删除的意思。当然如果在处理JSON文档的程序中null就代表资源不存在，那确实也可以避免这个问题。
  - 无法追加数组，因为必须提供完整的数组才能表达元素的修改
  - 一旦Patch是错误的，比如路径错误，他也会被合并到正确的数据中去，因为merge patch看起来是一种非常灵活的数据修改方式，但在JSON Patch中如果路径错误的话，会导致操作失败。
- 综上所述，如果面对的是结构比较简单，校验不要求很强烈的场景，可以选择JSON Merge Patch，
  - 但是更为复杂的场景，建议选择JSON Patch，因为这种方式确保原子执行和错误报告。
- Kubernetes中的webhook采用的就是上文提到的第一种方案（JSON Patch）

## 💡 [JSON Merge Patch: Algebra and Applications](https://github.com/endpointservices/mps3/blob/main/docs/JSON_merge_patch.md)

- JSON Merge patch is a standardized way to encode sparse updates to a JSON document.

- 🆚️ Comparison to JSON Patch (RFC 6902)
  - JSON Patch (RFC 6902) attempts to update a state by applying a sequence of operations
  - The is more expressive, it can represent null values and can also express insertion into an array. 
  - However, it is more complex and imperative. 
  - It does not have as many nice algebraic properties as JSON-merge-patch
  - JSON-merge-patch is functional and elegant, but restricts you to non-null values and dictionaries. JSON patch is applicable in more situations but clunky. I suspect that JSON-merge-patch's constraints force better schema design, smaller code, and fewer edge cases

- If you view a JSON document as the state of a system, then patching can be seen as updating the state.
- Arrays and null values don't work
  - Merge patches have a huge disadvantage in that they only really work well with dictionaries. 
  - Furthermore, because `null` is used to represent delete, it is impossible to use `null` as a value. 
  - You can use arrays, but they are not merged efficiently, and thus array mutations tend to conflict more frequently.

- Merges are associative for structured documents
- Non-overlapping patches are commutative.
- Overlapping writes are last-write-wins
- Merges are idempotent
# more
