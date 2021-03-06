---
title: note-git-dev
tags: [git]
created: '2021-06-01T16:55:33.625Z'
modified: '2021-06-01T16:55:46.743Z'
---

# note-git-dev

# guide

# discuss
- ## 用 git 来当网盘用如何？
- https://v2ex.com/t/525782
- 相比传统网盘的优势
  - 方便迁移
  - 版本管理更方便
  - 程序员的代码和工作空间可以一起上云了

- 缺点
  - git处理二进制文件太慢了
  - 正规用法是用 GitHub LFS 服务（收费）
  - dropbox一类的网盘都是你编辑完文件保存就自动上传了，git 还需要 commit push，相比之下 git 的存在感还是太强了

- ## 如何减小仓库体积
- [随着版本不断的更新，以前的版本内容会不会越积越多，导致占据太多硬盘容量？](https://www.zhihu.com/question/370933878)
- 会，非二进制文件只记录差异部分
- 会的。git会保留你每次更新的完整文件, 所以随着commit的增加, 仓库所占体积肯定会随着增加。并且git会把远端仓库的所有commit拉到本地, 本地存储也会增加.
  - git设计的初衷主要是为了代码管理, 代码作为文本文件经过压缩之后不会很大. 
- 那么如果一定要添加二进制的大文件怎么办?
  - 建议使用Git LFS, 这个模块专门用来管理大文件的. 大概原理就是, 在添加大文件的时候, 如果被标记为LFS, 相应的git会自动添加一个描述文档. 推送到远端的时候会完整上传文件和描述文档. 在其他开发者拉取代码时, 标记为LFS的文件只拉取一个相关的描述性文档. 只有在必须获取该文件时才会下载. 这样其他开发者反应更快速.
- .git文件主要用来记录每次提交的变动，当我们的项目越来越大的时候，我们发现 .git文件越来越大。
  - git给出了解决方案，使用`git branch-filter`来遍历git history tree, 可以永久删除history中的大文件，达到让.git文件瘦身的目的。

- ref
  - [gitee仓库体积过大，如何减小？](https://gitee.com/help/articles/4232#article-header0)

- ## [为什么其他办公领域不使用git?](https://www.zhihu.com/question/329750471)
- Git对非纯文本内容支持并不好，虽然能管理版本，但是无法方便的diff，merge。
- Git一般对文本文件支持比较好，但word、excel等office文档是二进制文件。
- 最好的方案是在加工内容阶段和格式优化阶段完全剥离。
- svn给美术策划用, git给程序用

- [使用git管理ppt版本等文档吗？](https://www.zhihu.com/question/22322435)
- Git适合管理文本内容, 但不适合管理二进制内容
  - Git 属于分布式版本控制系统, 需要 clone 整个仓库后才能 checkout 出最新的版本, 修改后提交. 而二进制内容比较难压缩, 会导致整个仓库占用的空间飞速增长. 没多久你可能就会发现, 你需要修改一个 2MB 的 PPT, 却需要先 clone 一个 200MB 的仓库, 而且过去的那些版本基本上又不再需要使用了.
  - 出现冲突时, 二进制内容(特别是你使用场景中提到的PPT)基本不存在自动完成 merge 且不出现 conflict 的可能性. 换言之, 一旦出现分歧, 就必然需要手工合并, 代价不小, 而且容易出现操作失误.
  - 根据你的使用场景来判断, 应该主要是在 Windows 下工作的. Git 在 Windows 下相比在其他平台下要难用得多..
- 像你这种场景, 要么使用传统中心式版本控制系统, 比如 SVN, 要么通过在线的协作环境, 比如 Microsoft 自己的 Office Web 版, 或者 Google Doc. 
- 但回到最初的问题: 你需要的真的是一个"版本控制系统"吗? 也许仅仅是一个集中分享的地方, 也许仅仅是希望一个人修改的时候, 另一个人不能修改, 而已.
- 其实！你们忽略了一件事情！pptx文件实际上是个zip文件，解压开来全是文本的xml和你加进去的视频、图片，是可以用git管理的！
