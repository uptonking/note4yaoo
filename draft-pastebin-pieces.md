---
title: draft-pastebin-pieces
tags: [draft, todo]
pinned: true
created: 2019-11-11T06:57:46.101Z
modified: 2021-03-22T18:24:50.639Z
---

# draft-pastebin-pieces

---

Yao King 邀请您参加预先安排的 Zoom 会议。

主题：Yao King's Personal Meeting Room

加入 Zoom 会议
https://us05web.zoom.us/j/7754416829?pwd=TUlMR3dMWEpaajdVR1VNdDR5N29NZz09

会议号：775 441 6829
密码：uZKAn9

- yaoo-accounts-social
  - cons
    - 用户的toots和retweet服务器不会保存，需要用户自己手动保存
  - pros
    - 用户可以自己搭建server
- mastodon
  - https://fosstodon.org/
    - open source software
  - https://mastodon.social/
    - twitter-like
  - https://vis.social/
    - data viz and d3
  - https://en.osm.town/
    - OpenStreetMap
  - https://mapstodon.space/
    - map
  - https://m.cmx.im/
    - 中文社区

- wechat-luckiikawayii
  - 技术积累
    - 前端基础html/css/js语法 👉🏻 笔记
    - 快速开发框架react/vue，状态管理 👉🏻 mvc-app
    - ajax前后端交互，对后端开发有基本了解 👉🏻 mock-api数据
  - 工作思路
    - 更重视解决问题的能力，而不是面试和做题
      - 分析现状，抓住重点，培养兴趣
    - 在某一方向的技术深度，长期积累
    - 长期维护的技术代表作

---

- 象牙客
  - 电费 50元
  - 包周 248
  - 包月 858

```JS
const unsubscribe2 = editor.selection.onSelectionChange(info => {
  console.log(';; sel-chge ', info.type);
});

const unsubscribe = editor.selection.onSelectEnd(info => {
      const { type, browserSelection, anchorNode } = info;

      const current_selection_in_text_block =
        editor.blockHelper.getCurrentSelection(anchorNode?.id);
      console.log(
        ';; sel-chge-end ',
        type,
        current_selection_in_text_block
      );
```

- js 产生定长字符串

```JS
Math.random()
  .toString(36)
  .replace(/[^a-z]+/g, '')
  .substring(0, 5);
```

- 图片 base64 编码示例

```
data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAOEAAADhCAMAAAAJbSJIAAAAhFBMVEX///+EMTGAJyeDLi6sfn5/JCR8GBiYV1fk1dW8l5d+ICDKsLB5DQ2CKyv9+vqcYGB6ExPYxMTw5+e3j4+OQ0N6EBB9HR2hamq/nZ3Su7umc3Pq39/cysp4BAS5kpJ7FxeIOTmRS0v38/PFpaWyiIjt5OSod3eINzeeZmaaXFyUUlKPSEjcOe1gAAAE6klEQVR4nO3dbVfaShSG4ZnEIAJRUAmgUKxw7LH9///v9GW51tHkCZM9k72Jfe7PBXIZCiHsIc6hbjfru146PMLH1Gz8Oq+KrJcm8/utNc+59a70/ZXv1ubAZY++X82NidtZz8CfxCtT4Y8+n6JvxC+GwHHfz9E/xDs74WGiIfT7o5nwIlMR+pEZUUvoRxefXegrI6Ke0FcPn11oRNQU2hBVhX6y+uxCC2JdmEfXSvzXXJjfR/fURiy0iTXhKP5T+bpoJb4m2OwO1YXj6Pu8ahVqEw2EvvieYMODsxDqEk2EPvt6nWDbw7IRahKNhD77oUW0Evrs/jnB5gdkJlQj2gl96VWIhkJfPmkQdYTgYLzMFYgqwvwVnLPUeKKqCCebKfjuoMxvEyBa0xFOHSSWfRO1hHZENaHbAGJe/BPPaElPiIlZr0RFISYmOK+A0xS6BfgqLy96JKoKMbHHvagrdNt58+FNXsU/LEhZiIn7vojaQrddAuK8J6K6UH0v6gvdGO3FWS/jUwZCN0Z7cd4H0ULoHkfgA+OuB6KJ0I0RcbmIfvSP2QjdY4X2YnKikRATl5vox3+fldA9ZoA4S0w0E7oNmjdLTLTbh/iU47LpDyLOSojeE//sxZREI+F43zrPkHIv2gi3s1bgzzeNQ/RWvGUi3J4e250nI1oI0Sf9dy1Tzb8bCBdhs/Op5t/1hZvQyfJERHUhOvfdREwy4q8t7AD0fp9ixF9ZeOi2+CEFUVeIgOUIDIEmGPFXFaIlVsXl9Qoch8cTNYUQ+GsIDBJjR/wVhV/mAHj5+1YPVT9EPSEEvg1jImLkQg014XF/AujcCyK+DEF4HDVv/eTmfzeExJhVDEqzGBcAWNy8uyX6Z1XEiL/OxNA38HZXm9xHxIhVDJZTX01LEyDxpuGBgrIUNu4Y9B+2kBINhWBxyd3pF91O2QnhC+SJI4OumQlb3gHSEq2Ere/iV4goWcVgJDxxmLIGxOx79/l3G+HJ47ADOBUgWMVgIgw4lj6gvdh5FYOFMOjz0HQHiPcdiQbCKuxj+xS89XddxVATVovb2I6tK2/L1XPQvTxfgbvpSKyvkq3msZ1YWlzG3k23VQzKK53TVH7rQByksNMqhmEKfRn+ijpQoZ8Ef6cxVKHfhT5PByusQr/qH6ywCH2aDlaYhZ5hHKywDD1vQ+HZRiGF5x+FLcL4H56tT+WVRWy1zZQLs5foHw9+/UgsH9ax1bZTLkxwnqb2K0qNU9Dd2n788tRUGDbn3a0FhTAKJVEoiUIchZIolEQhjkJJFEqiEEehJAolUYijUBKFkijEUSiJQkkU4iiURKEkCnEUSqJQEoU4CiVRKIlCHIWSKJREIY5CSRRKohBHoSQKJVGIo1AShZIoxFEoiUJJFOIolEShJApxFEqiUBKFOAolUSiJQhyFkiiURCGOQkkUSqIQR6EkCiVRiKNQEoWSKMRRKIlCSRTiKJREoSQKcRRKolAShTgKJVEoiUIchZLOXFiN3XVcjcLY+0wo9NUstvql8ybR91m7njWvjUDh+UchhecfhX+R8DhYYfO15+vVrgkzlLKwqwo7t91bb6qwahModL5+daZBVAVfanUKLvF95o0OoUDnHibWWytoEvpK+rvVfmhP1HzUCejcoaiyMh9KZVYV625A564Xx9XlUFodF/BF5j+Mt9zZWpXGVgAAAABJRU5ErkJggg==
```

- install app-ubuntu-calibre
- sudo mkdir -p /opt/calibre && sudo rm -rf /opt/calibre/\* && sudo tar xvf calibre-5.13.0-x86_64.txz -C /opt/calibre && sudo /opt/calibre/calibre_postinstall

- TO-DO: components、datable、chart

- 知乎禁止转载的回答测试
  - https://www.zhihu.com/question/25950466/answer/31731502
  - 只有复制内容较长时才会提示申请转载，比如复制超过 150 字

- webpack react fast refresh

```

"@pmmmwh/react-refresh-webpack-plugin": "^0.4.0-beta.7",
"react-refresh": "^0.8.3",

const ReactRefreshWebpackPlugin = require('@pmmmwh/react-refresh-webpack-plugin');

new ReactRefreshWebpackPlugin(),

'react-refresh/babel',
```

- webpack 5 移除了 node 模块兼容

```

"crypto-browserify": "^3.12.0",
"stream-browserify": "^3.0.0",
"vm-browserify": "^1.1.2",
```

- class extends

```js
class B {
  print = () => {
    console.log("print b");
  };
}

class D extends B {
  print() {
    console.log("before-super-print");
    super.print();
    console.log("after-super-print");
    console.log("print d");
  }
}

const d = new D();
d.print();
d.__proto__.print();
// print b
// before-super-print
```

- musicbrainz-rename

```

$if2(%albumartist%,%artist%)/
$if(%albumartist%,%album%/,)
$if($gt(%totaldiscs%,1),%discnumber%-,)$if($and(%albumartist%,%tracknumber%),$num(%tracknumber%,2) ,)$if(%_multiartist%,%artist% - ,)%title%
```

- maven-aliyun: https://maven.aliyun.com/repository/central
- emotion 的 button

```
 const renderButton = (Root: React.ElementType<any> = 'button') => (
    <Root
      ref={forwardRef}
      type={Root === 'button' ? 'button' : undefined}
      {...(rest as HTMLElementProps<any>)}
      {...commonProps}
    >
      <span
        className={css`
          // Usually for this to take effect, you would need the element to be
          // "positioned". Due to an obscure part of CSS spec, flex children
          // respect z-index without the position property being set.
          //
          // https://www.w3.org/TR/css-flexbox-1/#painting
          z-index: 1;
        `}
      >
        {children}
      </span>
    </Root>
  );

  if (usesCustomElement(props)) {
    return renderButton(props.as);
  }

  if (usesLinkElement(props)) {
    return renderButton('a');
  }

  return renderButton();
```

- 🤝🏻 老范，一晃10个月过去了，我竟然还没出去工作。
  - 这期间一直在杭州，做了很多想做的事，包括数据库、多人协作编辑、编辑器、表格
  - 我最有代表性的作品是类似WPS/Word的编辑器，完成度中等 https://windrunnermax.github.io/DocEditor/
  - 年后我意识到这个编辑器的亮点不够大，所以近期在做多维表格，业务场景是任务管理、内容管理，目标效果类似飞书多维表格 https://www.feishu.cn/product/base
  - 你可能不理解我为什么对技术这么执着，今天我30岁，没有技术代表作和产品代表作我就感觉这些年白干了
  - 💡 对工作和公司的想法我有了变化，上份工作我对编辑器非常执着才加入了投光编辑器，离职原因是工作忙且不想写没有积累的代码；可是，很遗憾我错过了一个亿的机会，投光改名Affine在2022年底Pre-A轮融资1000万美元，原来创业独角兽曾经就在我身边可是我没把握住
  - 又积累了10个月后，我坚定自己做编辑器和内容管理的方向是没错的。产品亮点是自研在编辑器中支持多维表格，初步效果可以在这里体验下(我在模仿这个) https://demo.undb.xyz/
  - 不得不承认，在工作中代码并没有我想的那么重要，融资前的代码乱七八糟，但演示demo效果还行，老板很能吹，所以能融1000万；在我的技术代表作稳定后，我就会花更多时间在产品和业务项目上
  - 我准备最后打磨下作品，然后就面试工作了，代码问题不是一时能改完的
  - [衰]这次找你是因为钱用完了，去年处理完老家事情手里大概3万多，现在手里只剩2000，我也是催自己赶紧做出代表作然后面试工作，火烧眉毛了
  - 希望你能再次帮我，我挺无颜面对老同学的，但自己几乎无社交，事不过三。这次打算借6000开始新工作，主要用于房租日用。因为前些年债务的原因，最近我的微信钱包被冻结了，所以银行卡转账可能被冻结也可能正常，所以希望你能先转3000，等我确定工作地点入职时再转3000。没想到有什么能回报你，如果有一天我创业了，可以找你做市场顾问。
  - 我还是太任性了，但年轻时没有代表作，估计以后也不会有了。现在我很能理解你考公的选择了，普通工作几乎都不轻松，有没有润的动力，希望我们都能做到自己想做的。
  - [抱拳]

- debt
  - 金敏小姐(2017) - 30000
  - 大丫(2016) - 17000 + 2000
  - [x] 小姨(2016) - 20000 + 1500
  - mom
    - 6212 2518 0900 0758 487
    - 6212251809000758487
  - debt-五妈 
    - 20230519: 5000新工作启动资金
    - 20230521: 1500 = 房租1510
    - 20230605: 200 = 电费181
    - 20230630: 1100搬家 = 新房租958 + 邮政ems111
    - 20230702: 200生活费 = 50(饺子)+60(面条)+母亲银行卡20
    - 总计 8000
    - 新城市预计 1500

- debt-投诉
  - 翼支付 冻结
  - 普惠金融 
  - 招联金融 北海仲裁
    - http://www.beihaizhongcai.com/app/zc_filelist?type=3&caseno=202210897_368
    - http://www.beihaiaccloud.com/template.html?filetype=3&caseid=1899552
  - 众安
  - 衢州 仲裁
  - 庆阳 仲裁

- debt-freeze
  - 现金发放
  - 借用亲友银行卡
    - 工资发亲人卡上，一般公司都不太愿意，怕以后跟你扯皮，有风险有麻烦。
    - 而且证明你和亲人的关系也比较麻烦。
  - 办新卡，可能被再次冻结

- debt-payback
  - 微信钱包被强制扣除 1934_202305

- 银行卡冻结，荆门市中级人民法院
  - 北海仲裁 冻结
  - 解冻的方法，都是协商+还款
  - [荆门市中级人民法院](http://jmzy.hbfy.gov.cn/)
  - [广西 北海仲裁委员会 北海国际仲裁院](https://www.beihaizhongcai.com/)

- 五爷五妈的支持(日期: 金额)
  - 20230519: 5000 = 新工作启动资金(已冻结)
  - 20230521: 1500 = 房租1510
  - 20230605: 200 = 电费181
  - 20230630: 1100搬家 = 新房租958 + 邮政ems111
  - 20230702: 130生活费 = 50(饺子)+60(面条)+母亲银行卡20
  - 20230715: 1070 =  房租898+生活费166
  - 总计 9000 - 950 = 8050
  - > 新工作新城市预计 1500
# 刘邦致歉
- 没有实现自己的工作计划
- 原因
  - 厌恶情绪
  - 技术目标差距大
  - 产品盈利不明确
- 计划
  - 技术工作，减少白干
  - 专注技术
  - 专注产品
