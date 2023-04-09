---
title: ux-color-palette
tags: [color, ux]
created: 2020-07-17T09:55:30.767Z
modified: 2022-10-23T14:57:23.473Z
---

# ux-color-palette
- https://github.com/nordtheme/nord /MIT
  - https://www.nordtheme.com/docs/colors-and-palettes
  - A total of sixteen, carefully selected, dimmed pastel colors
  - #1d2129
  - #2E3440 #434C5E #434C5E #4C566A
  - #D8DEE9 #E5E9F0 #ECEFF4   #f1f3f5 #f2f4f8
  - #8FBCBB #88C0D0 #81A1C1 #5E81AC
  - #BF616A #D08770 #EBCB8B #A3BE8C #B48EAD

- https://github.com/yeun/open-color /MIT
  - https://yeun.github.io/open-color/
  - an open-source color scheme optimized for UI like font, background, border, etc.

- [Tailwind CSS Color Generator - UI Examples & WCAG Contrast Ratios](https://uicolors.app/browse/tailwind-colors)
  - 提供了 wcag v2/v3 的对比度

- 对比度是指显示屏上两种相邻颜色之间的亮度或发出光线的强度的差异计算值。
  - AA   普通文本是4.5:1，大型文本3:1
  - AAA  普通文本是7:1，  大型文本4.5:1

- [不要依赖 WCAG 2 的对比度计算，试试 APCA - 知乎](https://zhuanlan.zhihu.com/p/555769196)
  - 如果你的产品有暗色模式（Dark Mode），请不要依赖 WCAG 2，它几乎不起作用
    - 问题在于 WCAG 2.x 使用了完全基于亮度的计算方式，会过分夸大暗色的对比度权重，会否决一些实际上比较容易识别的色彩组合
  - 将 WCAG 2 移植到 APCA 时的推荐实践标准
    - 75 对应 WCAG 7:1
    - 60 对应 WCAG 4.5:1
    - 45 对应 WCAG 3:1

- pgd色板设计，10级色彩，根据对比度
  - 0，11，22，33，44，55，63，72，81，90
  - 中间未严格遵守标准，是考虑到深色用的少
# nice css named colors: variant/alike/light
- Grey: #808080
  - slategrey/lightslategrey: #708090 / #778899
  - silver: #c0c0c0 银灰色，比grey浅
  - snow: #fffafa
  - ghostwhite: #f8f8ff
  - dimgrey/grey/silver/lightgrey/lavender/gainsboro/whitesmoke：灰色，由深到浅
- Red: #ff0000
  - coral: #ff7f50 珊瑚红，有点黄
  - tomato: #ff6347
  - linen: #faf0e6 亚麻布
  - seashell: #fff5ee 海贝壳
  - blueviolet: #8a2be2
  - slateblue: #6a5acd
  - mediumpurple: #9370db
  - mediumslateblue: #7b68ee
  - darkslateblue: #483d8b
  - lavender: #e6e6fa 薰衣草
  - darkorchid: #9932cc
  - purple: #800080
  - darkorchid: #9932cc
  - darkviolet: #9400d3
  - violet: #ee82ee 紫罗兰
  - hotpink: #ff69b4
  - indigo: #4b0082
  - antiquewhite/oldlace：古董白，粉红色
  - orangered: #ff4500
  - fuchsia/magenta: #ff00ff
  - lightcoral: #f08080 珊瑚红，艳丽
  - lightpink: #ffb6c1 粉红
- Yellow: #ffff00
  - darkorange: #ff8c00
  - gold: #ffd700 金黄色
  - lightyellow: #ffffe0
  - khaki: #f0e68c 卡其色，米黄色
  - lemonchiffon：粉黄色，有点浅
  - orange: #ffa500
  - wheat: #f5deb3
  - bisque: #ffe4c4 浅黄，有点红
  - darkorange：深橙色
  - lavenderblush：淡紫红，有点浅
  - cornsilk：玉米穗黄，极浅黄偏白，适合背景色
- Green: #008000 ~~#00ff00~~
  - teal: #008080 深青色
  - mediumseagreen: #3cb371 海绿色，适合文字
  - beige: #f5f5dc 浅绿泛黄
  - ivory: #fffff0
  - 浅绿: #add
  - lightgreen: #90ee90 亮绿色，艳丽
  - seagreen: #2e8b57 深海绿，都有点深
  - darkseagreen: #8fbc8f
  - lightseagreen: #20b2aa
  - darkcyan: #008b8b 深青绿
  - yellowgreen: #9acd32
  - lightskyblue: 深蓝色
  - mediumslateblue：中暗蓝，深蓝偏紫
  - lightgoldenrodyellow：浅金黄，新绿活力
  - 松柏绿: #21a675
  - teal5: #20c997
  - 松花绿: #057748
  - 竹青: #789262
  - 碧绿: #2add9c
  - 青碧: #48c0a3
  - 黛绿: #426666
  - 苍翠: #519a73
  - 铜绿: #549688
- Blue: #0000ff
  - royalblue: #4169e1 墨蓝，又亮又深
  - dodgerblue: #1e90ff
  - aliceblue: #f0f8ff 浅灰蓝
  - azure: #f0ffff 亮蓝色，有点浅
  - lightblue: #add8e6 淡蓝，有点深，有点陈旧感
  - skyblue: #87ceeb
  - deepskyblue: #00bfff
  - cyan/aqua: #00ffff

- ref
  - https://developer.mozilla.org/en-US/docs/Web/CSS/named-color
# guide
- tips
  - 各设计系统都会有自己的调色板

- bolivian beauty  偏冷小暖又干净
  - https://www.color-hex.com/color-palette/25309
  - ivory/浅粉黄浅灰白
    - #f4e8c1
  - azul verde/青浅灰
    - #a0c1b8
  - bolivia/蓝深灰
    - #709fb0
  - jacaranda/紫浅灰
    - #726a95
  - malbec/极紫深灰
    - #351f39

- 莫兰迪色
  - 高级灰色调，饱和度低，不鲜亮

- 色彩参考
  - 马蒂斯
  - 夏加尔
  - 德加
  - 梵高

- [GitHub 上赋予每个编程语言一种颜色，似乎成了一种标准的色盘。](https://twitter.com/magic_akari/status/1489853045110235136)
  - go蓝、ts蓝、python蓝
# brand-color
- [google-logo-brand-color](https://www.designpieces.com/palette/google-new-logo-2015-color-palette-hex-and-rgb/)
  - red 
    - #db3236
    - 219, 50, 54
  - green
    - #3cba54
    - 60, 186, 84
  - blue
    - #4885ed
    - 72, 133, 237
  - yellow
    - #f4c20d
    - 244, 194, 13
- Google Spreadsheets Green Color
  - #0F9D58
- Excel Logo Color
  - #1D6F42
- handsontable-blue
  - #039be5
- linaria-red 洋红
  - #f15f79

- https://github.com/keeev/brandcolors /201507
  - Brandcolors (LESS & Sass Variables) for all known brands like Facebook, Twitter, Kickstarter and many more.
# color-repos
- https://github.com/adobe/leonardo
  - https://leonardocolor.io/
  - Generate colors based on a desired contrast ratio
  - [WCAG 3 APCA Lc contrast calculations](https://github.com/adobe/leonardo/issues/197)
    - APCA is already a supported method of contrast generation in Leonardo.

- https://github.com/primer/prism
  - https://primer.style/prism/
  - A tool for creating and maintaining cohesive, consistent, and accessible color palettes

- https://github.com/jxnblk/palx
  - https://palx.jxnblk.com/
  - Automatic UI Color Palette Generator
  - Inspired by Open Color, Palx takes a single input color, then spreads the hue across the color spectrum in 12 steps, and spreads each hue across 10 luminance steps. 

- https://github.com/ardov/huetone
  - https://huetone.ardov.me/
  - A tool to create accessible color systems

- https://github.com/proteanstudio/contrast-tools
  - https://contrast.tools/
  - Color contrast value in WCAG 3.0 is calculated using the Advanced Perception of Color Algorithm (APCA). Unlike previous contrast calculations, the APCA considers the context in which colors are used to determine their readability

- apca
  - [Colour Contrast Tool](https://cliambrown.com/contrast/)
  - [Accessible Palette: Create color systems with consistent lightness and contrast](https://accessiblepalette.com/)
  - https://github.com/bruskowski/color-contrast-checker
    - [Color Contrast Checker](https://contrast-checker.vercel.app/)

- https://github.com/Myndex/apca-w3
  - https://apcacontrast.com/
  - APCA is the Accessible Perceptual Contrast Algorithm, a new way to predict contrast for text and non-text content on self illuminated displays.

- https://github.com/radix-ui/colors
  - https://www.radix-ui.com/colors
  - A gorgeous, accessible color system.
- https://github.com/dmarman/dmarman.github.io
  - https://tailwind.ink/
  - an AI palette generator trained with the Tailwindcss colors.

- https://github.com/ant-design/ant-design-colors
  - https://ant.design/docs/spec/colors-cn
  - Color palettes calculator of Ant Design

- https://github.com/arcticicestudio/nord
  - https://github.com/arcticicestudio/nord
  - 冷绿色系
# 中国风色彩
- https://colors.ichuantong.cn/
  - https://github.com/zerosoul/chinese-colors
  - 中国传统颜色在线手册
  - 技术栈 create-react-app，styled-components，html2canvas，pinyin: 汉字转拼音
  - 颜色数据来源：[weibo 中国传统颜色](http://blog.sina.com.cn/s/blog_5c3b139d0101deia.html)
  - ui参考 https://nipponcolors.com/

- https://colors.flinhong.com/
  - https://github.com/flinhong/colors
  - 中国传统色彩，日本传统色彩
  - 纯css

- more
  - http://zhongguose.com/
    - 列出了很多颜色
  - http://color.xunmi.cool/
  - https://htmlcss.jp/color/china.html

- 乾隆色谱
  - 由中国丝绸博物馆通过染色实验还原，在博物馆内展出，网上能找到通过拍照加整理的版本，虽总数不多但具备较高的参考价值，不过网上能找到的版本自身也有色差
- 金成熺《染作江南春水色》
  - 作者虽为韩国人，但本书其实很下功夫，网上其实能下到PDF全书
  - 对于《天工开物》和《多能鄙事》记录的染色方法有做还原实验，但是《布经》《辍耕录》里的颜色是怎么得出来的就有点模糊，感觉准确性也有所下降，主要推荐《天工开物》和《多能鄙事》部分的色卡

- ref
  - [在哪里能找到中国传统色彩的RGB色卡？](https://www.zhihu.com/question/30491221)
# Open source color system from components.ai
- https://components.ai/theme/sRr4Q9BGmH0jAOA99nc2

- 提供了多套色板数据
  - bootstrap.v5, open color, material 2014, palx, tachyons.v5

- 132 colors
- 5390 accessible color combinations
- The first 6 steps in each scale are accessible with white
  - the last 6 steps are accessible with black
- Export as CSS, JS, JSON, or Sass 
# [canva color palettes](https://www.canva.com/learn/brand-color-palette/)
- 01. Rich and Adventurous  温暖饱和感
    - sheer/浅蓝灰           #c5d2db
    - shutter blue/深天蓝    #2096ba
    - papaya whip/粉橙浅灰    #e7b183
    - puce/紫红浅灰           #c5919d
    - terracotta/深黄灰       #df6e21
- 02. Warm Antique
- 03. Waimea Waters
- 04. Tropical Punch
- 05. Bolivian Beauty  
- 06. Fall Collection
- 07. Very Venice
- 08. Vintage Sundown  一点点温暖
    - pink horizon/深粉浅灰   #e7baa0
    - sand surge/深灰浅白     #e5dace
    - moss tide/青灰偏灰      #b2b2a2
    - marine green/深青浅灰   #6d7973
    - black sand/棕黑色       #3f3931    
- 09. Marigold Mix
- 10. Nordic Woods
- 11. Green and Gold
- 12. Balearic Bounty
- 13. Aqua Army  青绿有点亮
    - aquapoise/亮蓝     #7bd4cc
    - honey/深青黄       #bea42e
    - army/深绿浅灰       #7b895b
    - celadon/深青       #037367
    - sangria/极黑色      #00281f
- 14. Siesta Hour
- 15. Mellow Musings 淡暖治愈系  *
    - powder blue/浅蓝    #c4d4e0
    - nantucket/深蓝灰    #9aabb9
    - apricot/浅橙红      #e2b49a
    - jasmine/深黄灰      #e9c77b
    - ink/极深蓝          #193446
- 16. Afternoon Delights  冷紫色
    - linen/灰白          #d1d3cf
    - raisin/紫灰偏灰      #757081
    - lavender/深蓝浅灰    #6b82a8      
    - grape/紫灰           #6c4f70
    - black cherry/深紫黑  #39324b
- 17. Greek Salad
- 18. French Connection  严肃沧桑感
    - cashmere/深灰浅青      #cbc5c1
    - french blue/浅蓝灰    #a2aab0
    - white wash/灰白       #ebeced
    - denim/深蓝深灰         #4c586f
    - gunmetal/黑浅灰       #3e3e3b
- 19. Serene Sakura
- 20. Morning Mist  深青厚重感
    - dew/浅蓝灰           #91b3bc
    - rain/深青灰          #5b7d87
    - currant/深紫偏黑      #45415e
    - slate/极青深灰        #2b4251
    - creosote/深黑深灰     #2e323c
# yaoo-color-palettes
- open-color with contrast
  - https://leonardocolor.io/theme.html?name=pgd-green&config=%7B%22baseScale%22%3A%22green-teal%22%2C%22colorScales%22%3A%5B%7B%22name%22%3A%22gray%22%2C%22colorKeys%22%3A%5B%22%23adb5bd%22%5D%2C%22colorspace%22%3A%22RGB%22%2C%22ratios%22%3A%5B%220%22%2C%2211%22%2C%2222%22%2C%2233%22%2C%2244%22%2C%2255%22%2C%2263%22%2C%2272%22%2C%2281%22%2C%2290%22%5D%2C%22smooth%22%3Atrue%7D%2C%7B%22name%22%3A%22red%22%2C%22colorKeys%22%3A%5B%22%23ff6b6b%22%5D%2C%22colorspace%22%3A%22RGB%22%2C%22ratios%22%3A%5B%220%22%2C%2211%22%2C%2222%22%2C%2233%22%2C%2244%22%2C%2255%22%2C%2263%22%2C%2272%22%2C%2281%22%2C%2290%22%5D%2C%22smooth%22%3Afalse%7D%2C%7B%22name%22%3A%22orange%22%2C%22colorKeys%22%3A%5B%22%23ff922b%22%5D%2C%22colorspace%22%3A%22RGB%22%2C%22ratios%22%3A%5B%220%22%2C%2211%22%2C%2222%22%2C%2233%22%2C%2244%22%2C%2255%22%2C%2263%22%2C%2272%22%2C%2281%22%2C%2290%22%5D%2C%22smooth%22%3Afalse%7D%2C%7B%22name%22%3A%22yellow%22%2C%22colorKeys%22%3A%5B%22%23fcc419%22%5D%2C%22colorspace%22%3A%22RGB%22%2C%22ratios%22%3A%5B%220%22%2C%2211%22%2C%2222%22%2C%2233%22%2C%2244%22%2C%2255%22%2C%2263%22%2C%2272%22%2C%2281%22%2C%2290%22%5D%2C%22smooth%22%3Afalse%7D%2C%7B%22name%22%3A%22green-sea%22%2C%22colorKeys%22%3A%5B%22%233cb371%22%5D%2C%22colorspace%22%3A%22RGB%22%2C%22ratios%22%3A%5B%220%22%2C%2211%22%2C%2222%22%2C%2233%22%2C%2244%22%2C%2255%22%2C%2263%22%2C%2272%22%2C%2281%22%2C%2290%22%5D%2C%22smooth%22%3Afalse%7D%2C%7B%22name%22%3A%22green-pine%22%2C%22colorKeys%22%3A%5B%22%2321a675%22%5D%2C%22colorspace%22%3A%22RGB%22%2C%22ratios%22%3A%5B%220%22%2C%2211%22%2C%2222%22%2C%2233%22%2C%2244%22%2C%2255%22%2C%2263%22%2C%2272%22%2C%2281%22%2C%2290%22%5D%2C%22smooth%22%3Afalse%7D%2C%7B%22name%22%3A%22green-teal%22%2C%22colorKeys%22%3A%5B%22%2320c997%22%5D%2C%22colorspace%22%3A%22RGB%22%2C%22ratios%22%3A%5B%220%22%2C%2211%22%2C%2222%22%2C%2233%22%2C%2244%22%2C%2255%22%2C%2263%22%2C%2272%22%2C%2281%22%2C%2290%22%5D%2C%22smooth%22%3Afalse%7D%2C%7B%22name%22%3A%22blue%22%2C%22colorKeys%22%3A%5B%22%23339af0%22%5D%2C%22colorspace%22%3A%22RGB%22%2C%22ratios%22%3A%5B%220%22%2C%2211%22%2C%2222%22%2C%2233%22%2C%2244%22%2C%2255%22%2C%2263%22%2C%2272%22%2C%2281%22%2C%2290%22%5D%2C%22smooth%22%3Afalse%7D%2C%7B%22name%22%3A%22blue-indigo%22%2C%22colorKeys%22%3A%5B%22%235c7cfa%22%5D%2C%22colorspace%22%3A%22RGB%22%2C%22ratios%22%3A%5B%220%22%2C%2211%22%2C%2222%22%2C%2233%22%2C%2244%22%2C%2255%22%2C%2263%22%2C%2272%22%2C%2281%22%2C%2290%22%5D%2C%22smooth%22%3Afalse%7D%5D%2C%22lightness%22%3A100%2C%22contrast%22%3A1%2C%22saturation%22%3A100%2C%22formula%22%3A%22wcag3%22%7D
