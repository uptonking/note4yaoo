---
title: toc-ux-fonts
tags: [fonts, toc, ux]
created: '2020-07-17T10:51:21.597Z'
modified: '2020-07-17T10:54:16.341Z'
---

# toc-ux-fonts

# discuss

- ## How to get the fastest web fonts (Updated 2021)
- https://twitter.com/leeerob/status/1345554813375938561
  - Use a variable font 
    - Variable fonts allow you to combine multiple styles and weights (e.g. bold, italic) into a single font file.
  - Preload your font file
    - The browser assigns loading priorities to different types of resources. 
    - You can influence which resources are most important by preloading critical assets.
    - `<link rel="preload" href="fonts/inter-var.woff2" />`
  - Self-host instead of Google Fonts
    - Since 202010, Chrome no longer allows a shared cache across sites (Safari has worked this way since 2013).
    - Then, you can control caching and add `immutable`.
    - e.g. `Cache-Control: immutable, max-age=31536000`
  - Use `font-display: optional` to prevent layout shift
    - Most browsers have a default strategy similar to `font-display: block`. 
    - The only option that prevents layout shift is `optional` (including FOUT and FOIT).
    - Supported by all modern browsers.

# fonts

- free
  - catalog
    - http://zenozeng.github.io/Free-Chinese-Fonts/
    - https://www.zhihu.com/question/19727859
  - Source Han Sans
    - https://fonts.adobe.com/fonts/source-han-sans-simplified-chinese
      - https://github.com/adobe-fonts/source-han-sans
    - SIL Open Font License
    - the Source Han Sans and Noto Sans CJK typeface families are mechanically identical
      - https://github.com/adobe-fonts/source-han-sans/issues/122
  - Adobe's open source family
      - source code pro
      - source sans pro
      - source serif pro
      - source han sans/noto sans cjk/思源黑体
      - source han serif/noto serif cjk/思源宋体
      - 思源柔黑，由于这款字体是日文改造，所以其中大多都是繁体字，如果要使用这款字体，建议切换繁体输入法
  - 方正免费字体
      - 方正书宋、方正仿宋、方正黑体、方正楷体
      - 免费商用
          - https://www.foundertype.com/index.php/About/powerbus.html
  - 站酷免费字体7种
      - 站酷高端黑体、站酷酷黑体、站酷快乐体、站酷庆科黄油体、站酷文艺体、站酷小薇LOGO体
      - 免费商用
          - https://www.zcool.com.cn/special/zcoolfonts/
  - 王汉宗自由字形 (H. T. Wang Free Fonts)
      - https://github.com/cghio/wangfonts
      - GPL v2
  - 文泉驿字体
      - 文泉驿微米黑、文泉驿正黑
      - http://wenq.org/wqy2/index.cgi
      - GPL
  - 文鼎公众授权字体
      - 文鼎细上海宋、文鼎中楷、文鼎简报宋、文鼎简中楷、文鼎PL明体U20-L、文鼎PL报宋2GBK
      - http://www.arphic.com.tw/
      - 非商业免费用
  - 新蒂字体
      - 新蒂文徵明体免费版、新蒂小丸子小学生版、新蒂小丸子高级版、新蒂下午茶基本版
      - https://www.sentyfont.com/index.htm
      - 非商业免费用
  - 造字工房字体
      - 非商业免费用
  - Droid Sans Fallback
      - apache 2.0
      - Android设备初期时默认的中文字体，由谷歌委托台湾华康科技设计的，与微软雅黑很像
  - fandol fonts
      - GPL
      - https://github.com/guoyu07/fandol-fonts
  - 851 Chikara Dzuyoku is a hand-drawn Japanese font 
      - Free for personal, non-commercial, and commercial works
- western fonts
  - catalog   
      - https://www.fontsquirrel.com/
  - Roboto
      - https://github.com/google/roboto/
      - Apache 2.0
  - ZCOOL Addict Italic 站酷意大利体
  - Arual
      - 免费商用
      - https://www.dafont.com/arual.font
      - http://www.fonts.net.cn/font-18934379648.html
      - 无衬线
- other fonts
  - Airbnb Cereal
      - A new typeface that takes us from button to billboard.
      - https://airbnb.design/cereal/
  - 小米兰亭
      - http://www.miui.com/zt/miui8/index.html
  - 书体坊字体付费标准
      - http://blog.sina.com.cn/s/blog_4e6ac4af0102wpqg.html
  - 濑户字体
  - 华康字体，免费仅限用于阿里巴巴旗下网站
- tools for fonts
  - https://github.com/wentin/font-playground
      - 在线修改和预览

## web fonts

- 问题
  - 中文webfont过大，目前暂无优秀的解决方案
  - 目前中文WebFont的使用大多是将有限数目的字符转换为小字库部署到网站服务器上
- google fonts
  - http://www.googlefonts.cn/fonts
- 有字库
  - https://www.webfont.com/
  - 免费单页500字
- justfont
  - http://justfont.com/
- 腾讯的Font-Spider
  - 可以把页面中没有的字从字库剔除掉，使用的是NodeJS
  - 适合静态页面
