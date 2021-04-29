---
title: dev-ing-pieces-xp
tags: [dev, xp]
created: '2021-04-28T20:54:34.301Z'
modified: '2021-04-28T20:54:58.126Z'
---

# dev-ing-pieces-xp

# pieces

- ## 

- ## 实现mdx文档编辑后自动更新的思路
- (在当前app界面)编辑内容后直接渲染最新内容到dom，都在内存无需本地
- (在3方编辑器界面)编辑内容后保存到本地文件，然后app扫描目录，渲染内容
- ssg: 首次全面渲染，然后在后台监听新文件的添加，并立即构建
- ssr: 每次点击url，都重新请求mdx的内容

- ## 文件编辑浏览的实现思路
- edit > ~~save(内存或本地)~~ > render
- usecase
  - webpack的热加载

- ## 调试component-docs的文档示例
- npm workspaces的不同子包，可以使用不同版本的react，不会冲突
- 异常信息是 `mini css extract plugin loader has been initialized using an options object that does not match the api schema.` .
  - 修改版本后测试发现，深层原因不是mini-css-extract-plugin的版本问题
  - 查看component-docs项目的issues，有人已经提交了最新版样式错乱broken的bug，所以应该降级component-docs，而不是降级mini-css-extract-plugin
  - 容易看花眼: ^0.20.5，^0.24.0
