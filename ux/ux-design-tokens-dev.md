---
title: ux-design-tokens-dev
tags: [design-system, design-tokens, ux]
created: '2020-12-31T20:07:19.497Z'
modified: '2021-01-01T20:09:10.218Z'
---

# ux-design-tokens-dev

# faq

- 是否该用工具除了自动生成design tokens外，还要自动生成所有组件的样式？
  - 若自动生成组件样式
    - 极大提高复用性，所有组件的样式都自动生成了，但对生成工具高依赖、高要求
  - 若手写各个组件的样式
    - 极大提高组件设计修改的灵活性，花费更多精力，针对某一平台进行优化更方便
    - 很多现有的设计系统采用这种方式

# guide

- design-tokens-awesome-catalog
  - 主流tokens工具及标准参考
    - system-ui-theme-specification
    - salesforce-theo-spec
    - style-dictionary-properties
    - airbnb-lona-spec
    - universal-design-tokens-schemas
  - https://github.com/sturobson/Awesome-Design-Tokens
    - A list of repos that contain a companies' Design Tokens
  - [tailwind default theme](https://github.com/tailwindlabs/tailwindcss/blob/master/stubs/defaultConfig.stub.js)

- 使用设计工具生成design tokens的优点
  - 不用写代码，拖拽设计即可完成
  - 方便测试与分享
- 使用设计工具生成design tokens的缺点
  - 没有统一标准，经常面临选择问题
  - 有的插件只生成一个大tokens文件，有的可按自己分类生成多个
  - 用什么属性名，用什么属性值类型，该支持哪些类别的属性
  - 结论是**不推荐**使用拖拽搭建工具生成项目要用的中间配置属性数据
    - 具体业务场景对灵活性要求过高，频繁修改自动生成的代码太繁琐
    - 若工具生成的代码是最终要用的，则可考虑使用工具
    - 若工具生成的代码是中间代码，之后会基于中间代码解析转换，则慎用，多考虑

- design-tokens-doc设计
  - 变量名称和描述，可选实现预览
  - 重要tokens的独立文档
  - design tokens editor
    - [效果类似在线编辑预览](https://twitter.com/Una/status/1352109495565090817)

- https://github.com/system-ui/theme-specification
  - The theme object is intended to be a general purpose format for storing design system style values, scales, and/or design tokens.

- design-tokens-spec
  - [Airbnb Lona Component Definition](https://github.com/airbnb/Lona/blob/master/docs/file-formats/component.md)
    - Currently component data is encoded in JSON.
    - JSON is problematic because it's not easily mergeable or human-editable. 

# pieces

- Should I use theo or style dictionary?
  - 结论是，推荐使用json格式来描述design tokens
  - Both are good! Both have very active communities on the design systems slack. 
  - You can also create a custom one (Adobe did this). 
  - Theo uses `yaml` or `json` and takes a file-in file-out strategy. 
  - Style Dictionary uses `json` or `js` modules and merges all token files into 1 big object.

- Salesforce’s Design Tokens. Amazon’s Style Dictionary. Airbnb’s Style Expressions. Naming is hard.

- I figure a way to implement design tokens on @framer X using style-dictionary.
  - The output is a collection of CSS Variables and I was able to use them on CSS objects, with Styled components, and with Emotion.

# discuss

 

- ## Just shared the First Editor’s Draft of the Design Tokens specification with design tool vendors
- https://twitter.com/DesignTokens/status/1383245282134032387

- ## Why is a design system conflated by so many with code components, where it can be actually expressed as lower level tokens?
- https://twitter.com/oleg008/status/1095652075705434112
  - Why would you want to make the source of truth so much more complex than identifiers of a color or a behavior?
  - Is it basically bc naming things is hard?
- TLDR from responses I see 2 valid points:
  1. Tokens are instructions, someone has yet to build a component properly.
  2. Tokens need to contain very detailed information about each component's property, which is hard because there are a lot of them
- This is going to become a lot more common. We're seeing advanced tools specifically for designing color.
  - we will have tools for shadow, spacing, type scale etc.
  - Export JSON and the engineers take it from here.

- ## You are a web developer. You get handed a design for a Website
- https://twitter.com/elibelly/status/1214591804034764801
  - For simplicity's sake, let's say it's a one-pager with all the trimmings (nav, footer, menu, content, a form, etc)
  - What are the first three things you do?
- eg
  1. Print it and identify the different "components of the page" by drawing around them on paper
  2. Check if there's any further design considerations to be had (responsiveness, error states...)
  3. Identify design tokens (colors, fonts...)
- eg
  4. Write all the semantic, accessible HTML as if CSS and JavaScript don't exist
  5. Parse the design for component patterns, common spacing values, colors, typography, states, alt text, accessible naming, etc.
  6. Begin styling and adding functionality with a design system mindset
- eg
  4. Take the time to look at the design and really comprehend it without doing anything else
  5. Make a judgment whether anything about this is going to require anything more than plain html/css/js 
  6. Make a time/effort estimate 

# ref

- [Documenting Design Tokens](https://dbanks.design/blog/documenting-design-tokens/)
- [design-tokens-in-action](https://sproutsocial.com/seeds/resources/tokens/)
