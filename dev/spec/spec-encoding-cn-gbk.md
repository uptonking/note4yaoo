---
title: spec-encoding-cn-gbk
tags: [encoding, gbk, spec]
created: 2021-02-16T05:17:07.833Z
modified: 2021-02-16T05:17:27.642Z
---

# spec-encoding-cn-gbk

# guide

# base64
- [Base64 - MDN Web Docs](https://developer.mozilla.org/en-US/docs/Glossary/Base64)
  - When the term "Base64" is used on its own to refer to a specific algorithm, it typically refers to the version of Base64 outlined in RFC 4648, section 4
  - [RFC 4648 - The Base16, Base32, and Base64 Data Encodings](https://datatracker.ietf.org/doc/html/rfc4648)
# blogs-unicode
- [（译）2023 年每个软件开发者都必须知道的关于 Unicode 的基本知识 | 新世界的大门](https://blog.xinshijiededa.men/unicode/)
  - [What every JavaScript developer should know about Unicode_202111](https://dmitripavlutin.com/what-every-javascript-developer-should-know-about-unicode/)
# discuss-emoji
- ## 

- ## 

- ## Swift 是全球唯一一门能正确判断“🤦🏼‍♂️”这个字符长度的语言。
- https://twitter.com/tualatrix/status/1718884629162463370
- 这个其实不是语言的能力，而是 Swift 标准库的能力。但在语言层面，Swift 的 Character 类型确实能表示所有“字符”，而其他语言最多做到 Unicode scalar（或者 rune）
  - 考虑到 Swift 设计之初把 @UIApplicationMain、 @IBDesignable 等都硬编码到编译器里，说明它的定位就是服务上层应用开发。对于类似 C++、Rust 这种系统编程语言，在语言层面做这种事情就很重了，况且 ICU Segmentation 还是有时效性的。
- ICU Segmentation 是有时效性的？这个有什么具体的例子吗
  - 因为规则是随着 Unicode 版本更新的，分词逻辑也要定期更新
- 有意思，我来看看。总之 Unicode 默认不包含在 Embedded 领域应该是没有争议的；另一方面，其他通用编程领域应该默认处理好 Unicode 应该也是没有争议的。
  - 嵌入式领域甚至可能都不会用 GB2312，我这边的屏幕显示模块的代码都是直接硬编码用到的字，总数不超过十个
- The behavior of the length method depends on how it is defined in a particular programming language/library. For instance, In Swift  String.length represents the number of characters in a string. However, in Rust, String.len refers to the length of the string in bytes.

# discuss
- ## 

- ## 

- ## 

- ## [GB2312、GBK、GB18030 这几种字符集的主要区别是什么？](https://www.zhihu.com/question/19677619)
- 首先应当指出，目前的提问是有问题的，因为将三者定性为「字符集」是明显错误的，更妥当的提法是「几份文件」, 而非「几种字符集」。
  - GB/T 2312—1980《信息交换用汉字编码字符集　基本集》；
  - 技监标函 [1995] 229 号《汉字内码扩展规范（GBK）》1.0 版；
  - GB 18030—2005《信息技术　中文编码字符集》。
- 其中，第一份文件既是「字符集」标准也是「编码方案」标准，当然这里提到的「编码方案」和被 GBK 兼容的「事实上的内码标准」（de-facto internal encoding standard）是两回事。
  - 而后两份均为面向 UCS 字符集之子集的「编码方案」标准。这是三份文件的主要区别。

- ### GB2312-80
  - GB 2312 或 GB 2312-80 是中国国家标准简体中文字符集，全称《信息交换用汉字编码字符集·基本集》，又称 GB 0，由中国国家标准总局发布，1981 年 5 月 1 日实施。GB 2312 编码通行于中国大陆；新加坡等地也采用此编码。
  - 中国大陆几乎所有的中文系统和国际化的软件都支持 GB 2312。
  - 共收录了 **7445** 个字符，包括6763个汉字和682个其它符号。
    - GB 2312 标准共收录 6763 个汉字，其中一级汉字 3755 个，二级汉字 3008 个；
    - 同时收录了包括拉丁字母、希腊字母、日文平假名及片假名字母、俄语西里尔字母在内的 682 个字符。
  - GB 2312 的出现，基本满足了汉字的计算机处理需要，它所收录的汉字已经覆盖中国大陆99.75% 的使用频率。
  - 对于人名、古汉语等方面出现的罕用字，GB 2312 不能处理，这导致了后来 GBK 及 GB 18030 汉字字符集的出现。
  - GB 2312 对任意一个图形字符都采用两个字节表示，
    - 并对所收汉字进行了“分区”处理，每区含有 94 个汉字／符号，分别对应第一字节和第二字节。这种表示方式也称为区位码。

- ### GBK
  - GBK即汉字内码扩展规范，K代表汉语拼音扩展中扩，出现于Win95简体中文版中
  - GBK 共收入 **21886** 个汉字和图形符号，包括：
    - GB 2312 中的全部汉字、非汉字符号。
    - BIG5 中的全部汉字。
    - 与 ISO 10646 相应的国家标准 GB 13000 中的其它 CJK 汉字，以上合计 20902 个汉字。
    - 其它汉字、部首、符号，共计 984 个。
  - GBK 向下与 GB 2312 完全兼容，向上支持 ISO 10646 国际标准，在前者向后者过渡过程中起到的承上启下的作用。
  - GBK采用双字节表示，总体编码范围为 8140-FEFE 之间，首字节在 81-FE 之间，尾字节在 40-FE 之间，剔除 XX7F 一条线。
  - GBK 编码区分三部分：
    - 汉字区，包括GBK/2, GBK/3, GBK/4
    - 图形符号区，包括GBK/1，GBK/5
    - 用户自定义区，GBK区域中的空白区，用户可以自己定义字符。

- ### GB18030
  - 国家标准GB 18030-2005《信息技术中文编码字符集》，是中华人民共和国现时最新的内码字集，是 GB 18030-2000《信息技术信息交换用汉字编码字符集基本集的扩充》的修订版。
  - GB 18030 与 GB 2312-1980 和 GBK 兼容，共收录汉字 **70244** 个。
    - 与UTF-8相同，采用多字节编码，每个字可以由 1 个、2 个或 4 个字节组成。
    - 编码空间庞大，最多可定义 161 万个字符。
    - 支持中国国内少数民族的文字，不需要动用造字区。
    - 汉字收录范围包含繁体汉字以及日韩汉字
  - GB 18030 编码是一二四字节变长编码。
    - 单字节，其值从 0 到 0x7F，与 ASCII 编码兼容。
    - 双字节，第一个字节的值从 0x81 到 0xFE，第二个字节的值从 0x40 到 0xFE（不包括0x7F），与 GBK 标准兼容。
    - 四字节，第一个字节的值从 0x81 到 0xFE，第二个字节的值从 0x30 到 0x39，第三个字节从0x81 到 0xFE，第四个字节从 0x30 到 0x39。
  - GB18030分两种，
    - 一种是GB18030-2000，名为《信息交换用的汉字编码符集-基本集的扩充》，也就是GBK，已经被废止；
    - 另一个是GB18030-2005，名为《中文编码字符集》，为现行强制标准。

- ### GB13000
  - GB13000等同于国际标准的《通用多八位编码字符集 (UCS)》 ISO10646.1，就是等同于Unicode的标准，代码页等等的都使用UTF的一套标准。
  - 2009年公安部门在办理第二代身份证过程中，为解决生僻字输入电脑的问题，公安部与有关部门研制开发了GB13000新字库，扩大了国家标准字库的容量（收汉字 **32252** 个），增加收录了涉及姓名、住址方面的4600个生僻字，成为当前计算机系统中所能支持的最大汉字字库。
    - 目前，户籍管理部门都安装了由北大方正研发的“新典码输入法”，应对各种实际问题。
    - 但是医疗机构、金融机构、甚至包括一些政府部门等使用的是系统自带字库和常见输入法，汉字容量小，且未统一配备“造字”软件，因此在遇到生僻字时，基本无法处理。
