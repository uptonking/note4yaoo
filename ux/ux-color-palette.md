---
title: ux-color-palette
tags: [color, ux]
created: 2020-07-17T09:55:30.767Z
modified: 2022-10-23T14:57:23.473Z
---

# ux-color-palette
- tips
  - 通常需要花更多时间精力参考设计稿及交互细节，而不是在颜色上纠结

- pgd色板设计，10级色彩，根据对比度
  - logo可参考田字格
  - 0，11，22，33，44，55，63，72，81，90
  - 中间未严格遵守标准，是考虑到深色用的少
  - 配色风格采用Chinoiserie，整体浅绿/浅灰背景
  - 布局或形状多使用规则的方形或正圆+渐变
  - later
    - hitu插件使用国漫人物

- https://github.com/nordtheme/nord /MIT
  - https://www.nordtheme.com/docs/colors-and-palettes
  - A total of sixteen, carefully selected, dimmed pastel colors
  - #1d2129
  - #2E3440 #434C5E #434C5E #4C566A
  - #D8DEE9 #E5E9F0 #ECEFF4   #f1f3f5 #f2f4f8
  - #8FBCBB #88C0D0 #81A1C1 #5E81AC
  - #BF616A #D08770 #EBCB8B #A3BE8C #B48EAD
  - 苍白: #d1d9e0
  - 苍黑: #395260
  - 苍色: #75878a
  - 苍翠: #519a73
  - 苍青: #7397ab
  - 苍黄: #a29b7c

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
# named-colors: variant/alike/light/单色无色板
- Gray: #808080
  - slategray/lightslategray: #708090 / #778899
  - silver: #c0c0c0 银灰色，比gray浅
  - snow: #fffafa
  - ghostwhite: #f8f8ff
  - dimgray/gray/silver/lightgray/lavender/gainsboro/whitesmoke: 灰色，由深到浅
  - 铅白(国画颜料): #f0f0f4
  - 银白: #e9e7ef
  - 苍白: #d1d9e0
  - 苍黑: #395260
  - 墨色: #50616d
  - 苍色: #75878a
  - 墨灰: #758a99

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
  - 胭脂/燕脂(装扮、国画颜料): #9d2933/rgb(157, 41, 51), #9F353A/rgb(159, 53, 58)
  - 绛紫: #8c4356/rgb(140, 67, 86)
  - 海棠红: #db5a6b
  - 嫣红: #ef7a82
  - 银红(颜料): #f05654
  - 黛螺(画眉颜料): #4a4266/rgb(74, 66, 102)
  - 乌黑: #392f41

- Yellow: #ffff00
  - darkorange: #ff8c00
  - gold: #ffd700 金黄色
  - lightyellow: #ffffe0
  - wheat: #f5deb3
  - khaki: #f0e68c 卡其色，米黄色
  - lemonchiffon：粉黄色，有点浅
  - orange: #ffa500
  - bisque: #ffe4c4 浅黄，有点红
  - darkorange：深橙色
  - lavenderblush：淡紫红，有点浅
  - cornsilk：玉米穗黄，极浅黄偏白，适合背景色
  - 赤金: #f2be45
  - 乌金: #a78e44
  - 琥珀: #ca6924
  - 茶色: #b35c44/rgb(179, 92, 68)
  - 赭土(颜料): #9c5333/#955539
  - 秋色: #896c39

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
  - 松花色: #bce672
  - 松柏绿: #21a675
  - teal5: #20c997
  - 松花绿: #057748
  - 竹青: #789262
  - 碧绿: #2add9c
  - 青碧: #48c0a3
  - 黛绿: #426666
  - 苍翠: #519a73
  - 铜绿: #549688
  - 鸦青: #424c50
  - 松石: #779a99

- Blue: #0000ff
  - royalblue: #4169e1 墨蓝，又亮又深
  - dodgerblue: #1e90ff
  - aliceblue: #f0f8ff 浅灰蓝
  - azure: #f0ffff 亮蓝色，有点浅
  - lightblue: #add8e6 淡蓝，有点深，有点陈旧感
  - skyblue: #87ceeb
  - deepskyblue: #00bfff
  - cyan/aqua: #00ffff
  - 宝蓝: #4b5cc4 (群青-#5666b8)
  - 靛蓝: #065279
  - 靛青: #177cb0
  - 藏青: #2e4e7e
  - 苍青: #7397ab
  - 群青: #4c8dae (吉翠-#427284)

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

- [GitHub赋予每个编程语言一种颜色，似乎成了一种标准的色盘](https://twitter.com/magic_akari/status/1489853045110235136)
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
# gradient
- Gradient design tools
  - https://cssgradient.io/gradient-backgrounds/
  - https://uigradients.com/
  - https://github.com/webkul/coolhue
  - https://www.grabient.com/
  - https://github.com/itmeo/webgradients
  - https://gradientbuttons.colorion.co/
  - https://webgradients.com/
  - https://gradienthunt.com/
 

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
# 中国风配色/色板
- resources
  - [dribbble search 中文风/古风/水墨/复古/诗词/古诗](https://dribbble.com/search/%E4%B8%AD%E5%9B%BD%E9%A3%8E)

- 国风设计参考，传统色+布局
  - [中国风界面-站酷ZCOOL](https://www.zcool.com.cn/collection/ZNTM3MTc0NA==)
  - [ui古风-站酷ZCOOL-基本都是游戏](https://www.zcool.com.cn/collection/ZMzA3NjE2NjA=)
  - https://dribbble.com/zhixuefeng
  - https://dribbble.com/AdonisLee
  - https://dribbble.com/anhuimeng
  - https://dribbble.com/Bossbao
  - https://dribbble.com/yangliming

- http://zhongguose.com /参考《色谱》中科院科技情报编委会名词室. 科学出版社-1957
  - https://nipponcolors.com
  - 每种颜色都有名字

- 中国传统色 系列书籍
  - https://www.figma.com/community/file/932547561953107053
  - [《中国传统色-故宫里的色彩美学》_202010](https://book.douban.com/subject/35166650/)
    - 两位作者查找中日色彩相关文献近400部，严谨考据384种中国传统色名(24组x16色)
    - 根据24节气72物候，在几十万件故宫文物中选取应时应节的96件，从文物中提取传统色
    - 书很美，但是文字就和看百科一样只是一堆资料的罗列
  - [中国传统色 网页版](https://chinesecolor.org/)
    - 本项目根据《中国传统色：故宫里的色彩美学》纸质书籍做成网页形式方便浏览，每个色彩包含 CMYK、RGB、HEX。
  - [因为找颜色太困难，我做了一份excel表格，来源于三个参考，中国传统色-故宫+色彩通识+中科院中国色色谱](https://book.douban.com/review/14384195/)
    - 分为8个色系: 红橙黄绿青蓝紫褐
    - 每个色彩都有有色名、色彩、CMYK和RGB色值、色彩来历或解释，以及参考出处

- [pixso色卡推荐 | 传统中国风配色-及风景图片](https://pixso.cn/designskills/traditional-chinese-color-matching/)
  - https://pixso.cn/community/file/vcQlTWUQ_6GPN_azI4rDjg
  - 蓝墨茶
    - 蓝墨茶 #3E453D
    - 岩砾黑 #24271E
    - 中红驼 #8B6B5B
    - 赤白橡 #D3A488
  - 棉絮灰
    - 棉絮灰 #B5A69C
    - 老茶棕 #655045
    - 淡红鸢 #AF5F54
    - 苍灰绿 #3B4E3D
  - 柴染棕
    - 柴染棕 #967555
    - 薄香橙 #D4A278
    - 青灰蓝 #1D4C50
    - 飞泉青 #3F605B
  - 琉璃蓝
    - 琉璃蓝 #1459CF
    - 天水蓝 #7097DE
    - 古鼎黑 #120E10
    - 血石红 #A9423C
  - 杏叶黄
    - 杏叶黄 #E6B653
    - 鹿角棕 #DFBE96
    - 岩砾黑 #24271E
    - 穹灰蓝 #CCD8D0
  - 瓜瓤粉
    - 瓜瓤粉 #F7CE9B
    - 金莺黄 #F0A72E
    - 淡玫灰 #AE7F77
    - 长石灰 #313534
  - 蟹蝥红
    - 蟹蝥红 #B75A32
    - 淡豆沙 #73361E
    - 藕荷粉 #E7CFBA
    - 搪瓷蓝 #01255E
  - 淡藤萝紫
    - 淡萝紫 #F2E7E5
    - 芦穗灰 #BDAEAD
    - 赤白橡 #D3A488
    - 青灰蓝 #1D4C50
  - 珊瑚朱
    - 珊瑚朱 #DC785D
    - 淡土棕 #824E40
    - 藏花红 #E9A182
    - 铜器青 #283F3E

- [配色方案: Chinoiserie 中国风](https://www.btbat.com/2855.html)
  - Chinoiserie，法语，意即中国风。但与传统源于中国的中国风不同，Chinoiserie 是浪漫的幻象，是 18 世纪欧洲人臆想出来的「中国风」。
  - https://dribbble.com/search/chinoiserie
  - https://www.behance.net/search/projects?search=chinoiserie
  - https://www.zcool.com.cn/search/content?word=chinoiserie
  - https://www.shutterstock.com/zh/search/chinoiserie
  - http://krearte.id/wall-mural/chinoiserie
  - https://www.miltonandking.com/style/chinoiserie-wallpaper/
  - [这位公认的配色高手，又要带火这个惹眼新颜色了！ - 知乎](https://zhuanlan.zhihu.com/p/67653152)
  - [Chinoiserie中国风的消亡与发展（四） - 知乎](https://zhuanlan.zhihu.com/p/260190945)
    - 18世纪当越来越多的欧洲人踏上这片神州土地的时候，惊讶于完全不符合他们的想象。到处破破烂烂，不见金碧辉煌的景象
    - 中产阶级的增长使得越来越多的中国风从贵族家庭走入了普通中产家庭。
    - 中国风潮在从欧洲宫廷渐渐式微之后，在时光中逐渐演变成为一种家居装饰风格。这种风格一直在变化发展，融入了西方现代家居的血液之中。所以我们现在看到的很多家居装饰其实都带着中国风的影子。

- https://colors.ichuantong.cn/
  - https://github.com/zerosoul/chinese-colors
  - 中国传统颜色在线手册
  - 技术栈 create-react-app，styled-components，html2canvas，pinyin: 汉字转拼音
  - 颜色数据来源：[weibo 中国传统颜色](http://blog.sina.com.cn/s/blog_5c3b139d0101deia.html)

- https://colors.flinhong.com/
  - https://github.com/flinhong/colors
  - 中国传统色彩，日本传统色彩
  - 纯css

- https://boxingp.github.io/traditional-chinese-colors/
  - https://github.com/boxingp/traditional-chinese-colors
  - [把 384 种「中国传统配色」写成了网页，太惊艳了](https://www.cailei.net/1239.html)

- https://github.com/coolfishstudio/cfs-color
  - https://coolfishstudio.github.io/cfs-color/
  - 传统色谱

- 满庭芳·国色(2023春晚节目创意背景)
  - [满庭芳配色 色值 - 简书](https://www.jianshu.com/p/7264e726fdb9)
  - [满庭芳·国色 47种中国风颜色带色值完整版](https://www.xiaohongshu.com/explore/63ccebd1000000000200358b)
  - https://www.xiaohongshu.com/explore/63ccebd1000000000200358b
  - [《满庭芳·国色》43张色卡 - 哔哩哔哩](https://www.bilibili.com/read/cv21378771/)
  - [《满庭芳·国色》最全47种中国传统色高清色卡（附 RGB + CMYK + HEX 色值） – 大作社](https://www.dazuoshe.com/mantingfangguosezuiquan47zho.html)
  - [从《满庭芳·国色》看中国传统色彩体系的审美意趣 - 知乎](https://zhuanlan.zhihu.com/p/604312776)

- [525 种「颜值」与「文化」并存的中国风配色 - MasterGo](https://mastergo.com/blog/31)

- [中国传统色](https://peiseka.com/zhongguochuantongse.html)

- more
  - http://color.xunmi.cool/
  - https://htmlcss.jp/color/china.html
  - [颜色库查询-DIC TRADITIONAL COLOR OF CHINA中国传统色](https://www.colortell.com/colorbook/?callbook=s)

- 乾隆色谱
  - 由中国丝绸博物馆通过染色实验还原，在博物馆内展出，网上能找到通过拍照加整理的版本，虽总数不多但具备较高的参考价值，不过网上能找到的版本自身也有色差
  - [乾隆色谱2.0：清代宫廷丝织品的色彩重建-中国丝绸博物馆_202109](https://www.chinasilkmuseum.com/yz/info_18.aspx?itemid=28366)
  - [乾隆色谱：从历史档案复原清代色彩-中国丝绸博物馆_201404](https://www.chinasilkmuseum.com/yz/info_18.aspx?itemid=25761)

- 金成熺《染作江南春水色》
  - 作者虽为韩国人，但本书其实很下功夫，网上其实能下到PDF全书
  - 对于《天工开物》和《多能鄙事》记录的染色方法有做还原实验，但是《布经》《辍耕录》里的颜色是怎么得出来的就有点模糊，感觉准确性也有所下降，主要推荐《天工开物》和《多能鄙事》部分的色卡

- ref
  - [中国风配色卡-花瓣网](https://huaban.com/boards/57122778)
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
# colors-inspiring
- [Pantone潘通色卡将收费？](https://pixso.cn/designskills/pantone-color-card/)
# color-etymology
- [颜色参考来源](https://www.zhihu.com/question/30491221/answer/154649194)
  - [中国国家数字图书馆](http://www.nlc.cn/web/index.shtml)
  - [《色谱》_1957 - 625](http://find.nlc.cn/search/showDocDetails?docId=-3901948874488792801&dataSource=ucs01&query=%E8%89%B2%E8%B0%B1)
  - 《中国色名综览》_1979 - 672
  - 中国的传统色_1986 - 320
  - 中国颜色名称_1997 - 1867(很多流行色)
  - [《国色五百色》完稿，即将付梓，为中国传统色再添一片瓦 - 知乎](https://zhuanlan.zhihu.com/p/588827592)

## [在哪里能找到中国传统色彩的RGB色卡？](https://www.zhihu.com/question/30491221)

- 不同色卡同名的颜色都有差异，**因为中国传统色多是以一些近似颜色的物体来命名，基本都是一个范围，无法用RGB或者CMYK色值准确定义的**，
  - 比如桃红，同一棵树上的两朵桃花颜色都不一样，甚至同一朵花同一片花瓣还有渐变色。
  - 另外很多色名记载久远，传了几个朝代已经出现词义变更，更不用说传到现代了。

- 推荐的版本
  - 乾隆色谱，记载了已复原的这些颜色的复原步骤，书比较偏学术化
  - 金成熺《染作江南春水色》，对于《天工开物》和《多能鄙事》记录的染色方法有做还原实验
  - 国染馆馆长黄荣华 《中国传统天然染色色卡》
  - 微博洛梅笙自制的色卡

- 其他可参照的版本
  - 《中国传统色：故宫里的色彩美学》，当然这本书里真实有考据来源的颜色也是不少的，比如天水碧、流黄等，而且以节气的分类方式和搭配文物画色卡也真的是很吸引人，但是核心的色名部分真的存在大量可商榷空间
  - 王定理《中国の传统色》，选色比较偏，表示颜色的常用单字都没收录，而且对于传统色最广泛体现的染织领域占比偏小，大量收录了矿物色。
  - 鸿洋《中国传统色彩图鉴》，部分和国画颜料不符
  - 《中国国家地理》中国美色系列明信片

- 不同色卡同名的颜色都有差异，因为中国传统色多是以一些近似颜色的物体来命名，基本都是一个范围，无法用RGB或者CYMK色值准确定义的，比如桃红，同一棵树上的两朵桃花颜色都不一样，甚至同一朵花同一片花瓣还有渐变色。另外很多色名记载久远，传了几个朝代已经出现词义变更，更不用说传到现代了。

## [《色谱》与《中国の传统色》, 《中国色名综览》之色名比较研究(ZT)](https://www.douban.com/note/393997307/?_i=8942553XUA7MP0)

- 结语 
- 研究后发现, 
  - 《色谱》的色名大多来自於自然界中的动, 植物, 占总数的50%, 
  - 《中国の传统色》的色名选订或解释多采自织染, 服饰, 绘画领域, 
  - 《中国色名综览》是根据《色谱》编定的, 差异相同.
  - 但三研究对象在取样上均出现有偏颇不全的现象或取样过度集中的情形, 且未经客观且广泛且完整的搜集工作, 使得信赖度令人质疑
- 《中国の传统色》在汉字的使用上, 与《色谱》, 《中国色名综览》有所出入, 例如藕荷与藕合, 虽然只有一字之差, 但是却会造成色彩表10 达上的误解
  - 其中也发现单字的中国色名未被列入考虑, 却强加了许多近代外来的翻译性色名, 令人对「传统」两字的时间与区域定义产生困扰
- 也发现《中国色名综览》一书所列色名, 根据其所配合的曼塞尔(Munsell)色相表对照比较, 发现同属5R 6/12的大红, 珊瑚红及鱼腮红三色, 虽为色相相同, 却有著不同的命名.
# yaoo-color-palettes
- open-color with contrast
  - https://leonardocolor.io/theme.html?name=pgd-green&config=%7B%22baseScale%22%3A%22green-teal%22%2C%22colorScales%22%3A%5B%7B%22name%22%3A%22gray%22%2C%22colorKeys%22%3A%5B%22%23adb5bd%22%5D%2C%22colorspace%22%3A%22RGB%22%2C%22ratios%22%3A%5B%220%22%2C%2211%22%2C%2222%22%2C%2233%22%2C%2244%22%2C%2255%22%2C%2263%22%2C%2272%22%2C%2281%22%2C%2290%22%5D%2C%22smooth%22%3Atrue%7D%2C%7B%22name%22%3A%22red%22%2C%22colorKeys%22%3A%5B%22%23ff6b6b%22%5D%2C%22colorspace%22%3A%22RGB%22%2C%22ratios%22%3A%5B%220%22%2C%2211%22%2C%2222%22%2C%2233%22%2C%2244%22%2C%2255%22%2C%2263%22%2C%2272%22%2C%2281%22%2C%2290%22%5D%2C%22smooth%22%3Afalse%7D%2C%7B%22name%22%3A%22orange%22%2C%22colorKeys%22%3A%5B%22%23ff922b%22%5D%2C%22colorspace%22%3A%22RGB%22%2C%22ratios%22%3A%5B%220%22%2C%2211%22%2C%2222%22%2C%2233%22%2C%2244%22%2C%2255%22%2C%2263%22%2C%2272%22%2C%2281%22%2C%2290%22%5D%2C%22smooth%22%3Afalse%7D%2C%7B%22name%22%3A%22yellow%22%2C%22colorKeys%22%3A%5B%22%23fcc419%22%5D%2C%22colorspace%22%3A%22RGB%22%2C%22ratios%22%3A%5B%220%22%2C%2211%22%2C%2222%22%2C%2233%22%2C%2244%22%2C%2255%22%2C%2263%22%2C%2272%22%2C%2281%22%2C%2290%22%5D%2C%22smooth%22%3Afalse%7D%2C%7B%22name%22%3A%22green-sea%22%2C%22colorKeys%22%3A%5B%22%233cb371%22%5D%2C%22colorspace%22%3A%22RGB%22%2C%22ratios%22%3A%5B%220%22%2C%2211%22%2C%2222%22%2C%2233%22%2C%2244%22%2C%2255%22%2C%2263%22%2C%2272%22%2C%2281%22%2C%2290%22%5D%2C%22smooth%22%3Afalse%7D%2C%7B%22name%22%3A%22green-pine%22%2C%22colorKeys%22%3A%5B%22%2321a675%22%5D%2C%22colorspace%22%3A%22RGB%22%2C%22ratios%22%3A%5B%220%22%2C%2211%22%2C%2222%22%2C%2233%22%2C%2244%22%2C%2255%22%2C%2263%22%2C%2272%22%2C%2281%22%2C%2290%22%5D%2C%22smooth%22%3Afalse%7D%2C%7B%22name%22%3A%22green-teal%22%2C%22colorKeys%22%3A%5B%22%2320c997%22%5D%2C%22colorspace%22%3A%22RGB%22%2C%22ratios%22%3A%5B%220%22%2C%2211%22%2C%2222%22%2C%2233%22%2C%2244%22%2C%2255%22%2C%2263%22%2C%2272%22%2C%2281%22%2C%2290%22%5D%2C%22smooth%22%3Afalse%7D%2C%7B%22name%22%3A%22blue%22%2C%22colorKeys%22%3A%5B%22%23339af0%22%5D%2C%22colorspace%22%3A%22RGB%22%2C%22ratios%22%3A%5B%220%22%2C%2211%22%2C%2222%22%2C%2233%22%2C%2244%22%2C%2255%22%2C%2263%22%2C%2272%22%2C%2281%22%2C%2290%22%5D%2C%22smooth%22%3Afalse%7D%2C%7B%22name%22%3A%22blue-indigo%22%2C%22colorKeys%22%3A%5B%22%235c7cfa%22%5D%2C%22colorspace%22%3A%22RGB%22%2C%22ratios%22%3A%5B%220%22%2C%2211%22%2C%2222%22%2C%2233%22%2C%2244%22%2C%2255%22%2C%2263%22%2C%2272%22%2C%2281%22%2C%2290%22%5D%2C%22smooth%22%3Afalse%7D%5D%2C%22lightness%22%3A100%2C%22contrast%22%3A1%2C%22saturation%22%3A100%2C%22formula%22%3A%22wcag3%22%7D
