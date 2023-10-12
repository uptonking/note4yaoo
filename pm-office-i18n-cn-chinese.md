---
title: pm-office-i18n-cn-chinese
tags: [Chinese, cn, i18n, office, 中文优化]
created: 2021-04-09T07:10:20.648Z
modified: 2023-01-14T15:47:04.431Z
---

# pm-office-i18n-cn-chinese

# guide

- 针对中文优化的参考
  - vditor lute, 对中文语境优化的 Markdown 引擎，支持 Go 和 JavaScript
  - 直接参考中文编辑器，如wangEditor

- 中文搜索
  - 拼音首字母搜索
# 中文文档特色
- 特殊符号
  - 顿号、
  - 直角引号/方括号

- 中文词组/短语
  - 对调 `甲方和乙方` 中 `和` 字前后的内容

- markdown的中文段落首行缩进的实现
  - 手动输入全角空格
  - slash快捷菜单项

- 菜单、命令、小程序的搜索
  - 支持英文名和中文名

- 简繁转换
  - 渲染时
  - 复制粘贴时
  - 带有中文的url，要考虑转换与编辑
# search
- 中文按拼音首字母排序
# translation
- 很多自动翻译的工具会翻译code block里面的代码单词
# i18n-utils
- react-intl: focalboard, atlaskit-editor
  - 更多使用 FormattedMessage 组件，或intl.formatMessage()方法
  - 翻译可集中定义

- i18n-next: outline, undb
  - 使用 useTranslation() 返回的 t 方法，类似ckeditor
  - 翻译可集中定义

- https://github.com/inlang/inlang /ts
  - https://inlang.com/
  - globalization infrastructure for software && version control for apps
  - [discussion about reactivity architecture](https://github.com/inlang/inlang/issues/1122)

- https://github.com/noveogroup-amorgunov/localizify /ts/NoDeps
  - performant library for translation and localization in Node.js and the browser.
  - Detection user language in browser and in server requests
  - Easy scope system (nested-object translations)
# solutions
- tips
  - 参考各种中文版本标准或产品

- https://github.com/sivan/heti
  - https://sivan.github.io/heti/
  - 赫蹏（hètí）是专为中文内容展示设计的排版样式增强
  - 贴合网格的排版；
  - 预置多种排版样式（行间注、多栏、竖排等）；
  - 中西文混排美化，不再手敲空格，（基于 JavaScript 脚本）
  - 全角标点挤压（基于 JavaScript 脚本）；
  -  繁体中文支持
  - 自适应黑暗模式
  - https://github.com/sivan/devonthink-heti
    - https://sivan.github.io/devonthink-heti/
    - 基于赫蹏为 DEVONthink 的 Markdown 预览和 RSS 阅读器制作的样式，支持黑暗模式。
# discuss
- ## 

- ## 

- ##  `Intl.MessageFormat` proposal progressed to stage 1_202212
- https://twitter.com/sebastienlorber/status/1599740137037914112
  - Useful to inject/format dynamic values in i18n templates
  - Having a std message syntax in JS (and even more languages!) is nice
- React is a pain to work with external string 
- [Consider making it possible to evaluate strings like tagged template literals · Issue #19 · tc39/proposal-intl-messageformat](https://github.com/tc39/proposal-intl-messageformat/issues/19)
  - For complex use cases like DOM or React localization, we're not aiming to necessarily provide a direct solution, but the building blocks that allow for its construction.

# 古文

## [css 古文排版(含阿拉伯数字) - 简书](https://www.jianshu.com/p/7e42b6145101)

- 古文排版：从右到左，从上到下。基本用`writing-mode: vertical-rl;`都能解决。
  - 但是，如果文字中含有阿拉伯数字，排版就会和你预期不一样。
  - 针对阿拉伯数字那块，可以用`text-combine-upright: all;`来处理
