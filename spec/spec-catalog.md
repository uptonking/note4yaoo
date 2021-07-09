---
title: spec-catalog
tags: [catalog, spec]
created: '2020-08-17T06:46:13.639Z'
modified: '2020-08-17T07:16:58.844Z'
---

# spec-catalog

# api

- [The OpenAPI Specification](https://www.openapis.org/)
  - a broadly adopted industry standard for describing modern APIs
  - http://spec.openapis.org/oas/v3.0.3
  - https://swagger.io/specification/
  - https://github.com/ferdikoomen/openapi-typescript-codegen
    - NodeJS library that generates Typescript or Javascript clients based on the OpenAPI specification
- rest api
  - [Microsoft REST API Guidelines](https://github.com/microsoft/api-guidelines/blob/vNext/Guidelines.md)

# web

- OEmbed
  - https://oembed.com/
  - oEmbed is a format for allowing an embedded representation of a URL on third party sites. 
  - The simple API allows a website to display embedded content (such as photos or videos) when a user posts a link to that resource, without having to parse the resource directly.

# cultural-regional

- [Tags for Identifying Languages](https://tools.ietf.org/html/rfc5646)
  - [IETF language tag wiki](https://en.wikipedia.org/wiki/IETF_language_tag)
  - [Tags for Identifying Languages (BCP47)](https://www.ietf.org/rfc/bcp/bcp47.txt) (html标签的lang属性值所用)

# music

- [ID3 tags](https://id3.org/)
  - While there are legacy and future standards for ID3 tags, the **most popular version** implemented today is ID3 version **2.3**. 
  - A follow on version, 2.4, is documented on this website but has not achieved popular status 
    - due to some disagreements on some of the revisions and the tremendous inertia present in the software and hardware marketplace.

# more-formats


## DITA(Darwin Information Typing Architecture)
- Lightweight DITA (LwDITA) is a simplified version of DITA(Darwin Information Typing Architecture). 
  - In comparison to DITA 1.3, LwDITA has a smaller element type and attribute set, stricter content models, and a reduced feature set. 
  - LwDITA also defines mappings between XML, HTML5, and Markdown, enabling authoring, collaboration, and publishing across different markup languages.

- LwDITA is a proposed standard for expressing simplified DITA documents in XML, HTML5, and Markdown.

不愿意用，更多的都在使用 Github 上来写 MD 格式。

- [业界有哪些结构化文档写作软件包？](https://www.zhihu.com/question/55048996)
  - Arbortext是写作工具，dita是一种写作标准。
  - 书写结构化文档工具目前有 PTC的Arbortext，以及Syncro Soft的Oxygen xml

- [DITA 与 DOCBOOK 对比](https://www.ossez.com/t/dita-docbook/10050)
  - DITA和DocBook是数字出版领域的两种标准，通过定义规范化的文档描述规则，来解决文档交付过程中遇到的问题
  - DITA解决了出版物的结构化描述和内容重组问题，且支持多语言版本制作，适用于对格式有严格限定的技术手册类出版物。但DITA不能实现很完美的 样式渲染，且对于内容与格式一体化的复杂出版物，DITA很难进行主题和界定与划分。所以使用DITA进行书籍出版的成本和难度较高。
  - DocBook适用于通用出版物，文档易于组织和排版。但DocBook内容以Section段落组织，不具备DITA的内容映射机制，无法做到类似Topic这样粒度的内容划分与重组。且对于内容需要频繁修改的文档排版，Docbook略显力不从心。 
  - DITA和DocBook专注于交付技术信息，但DITA侧重于交付主题，而DocBook侧重于交付书籍。
  - DITA提供基于主题级粒度的信息分类，允许作者组织并描述特定信息领域。在生成多种文档格式的信息重用过程中，能够保持内容的高度一致性。在最终交付物的输出格式方面，DITA能够生成 PDF、CHM、HTML等大部分的出版交付类型。
  - DocBook常用的交付格式为PDF和HTML，其他输出格式需要借助相关的功能插件。

- [DITA 已死](https://zhuanlan.zhihu.com/p/345260365)
  - DITA 作为文档交付应该已经是日薄西山了。应该没有什么人通过写 XML 的方式来写文档了。
  - 相反，MD 和 AsciiDoc 格式的文档却大行其道。主要原因是能够随意部署，并且文档结构少，约束少，更加容易写作和阅读。
  - DITA，编译太复杂，PDF 生成问题太多，CHM 格式的文档很多时候大家都
