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

---

```JS
async function mockCmdkChat() {
  await new Promise((_) => setTimeout(_, 3000));
  return {
    status: 'success',
    message: '// ;;;\nCMD+K Error;\n// cmdkCodingRequest is not implemented;\n// please Reject and check your implementation;\n// ;;; ',
  }
  as
  const;
}

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

- strapi服务端返回csv的示例

```JS
{
  "data": "id,documentId,name,createdAt,updatedAt,publishedAt,locale\n1,hovfsfgtgnvroevstontx2h1,mystery,2024-03-22T15:59:30.658Z,2024-03-22T15:59:30.658Z,,"
}
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

# 刘邦致歉_202308
- 刘邦，非常抱歉，我没有实现自己的目标，找到比较满意的工作，所以暂时不能如期还款给你了😔。
- 我写了点想法，分析了一下自己职业生涯不顺利的原因。
- 再次感谢你对我的帮助，我也越来越理解你回老家和考公的选择，，我会降低自己的期望和要求，然后开始新的工作，大概十月或十一月把你的借款还了，希望我们都能调整好状态，做自己想做的事 🤔

## 想法变化

- 疫情期间互联网大厂扩招的人今年很多失业进入了市场，5月份左右，我只拿到了几家小公司和华为外包的offer，这些是往年我都不会考虑的工作，到了6月，招聘的职位和待遇大多面向应届生，所以我最终决定不去这些，然后继续做自己的代表作编辑器，这一拖就到了现在。
- 我分析了一下自己职业生涯不顺利的原因。

- 👉🏻 压力之下的厌恶情绪
  - 连续多轮的面试，感觉浪费了很多时间和精力，还对自己的工作能力没什么用，所以不想继续面试。
  - 随着年龄增大，面试与工作越来实际，最近的面试很多都是比较直白的问能给公司带来多少产出和收益，而我还是想纯粹一点写代码。
  - 就算拿到offer，入职工作，工作内容很可能与自己预想的有很大差距，技术也没什么提升，上份工作就是这样。
  - 程序员行业的工作时间整体都很长，工作后没什么时间做自己的技术与产品，在公司很少能积累技术，大多是不停的搬砖与沟通协调。
  - 我已经接受了工作就是拿时间换钱的逻辑，对工作内容不再抱有什么期待，希望趁年轻能做点前沿的技术。

- 👉🏻 技术积累不够深
  - 长期焦虑的一个重要原因，是自己的技术积累不够深，方向不够明确。
  - 技术开发有很多具体方向，大概从2021年开始，我决定 all in 编辑器，类似word、wps的富文本编辑器是一个需求广泛、需要技术积累、适合长期开发的技术方向。
  - 对于编辑器，无论是在公司的开发，还是自己尝试，仍然处于模仿和修改的阶段，目前原创技术不多。
  - 在公司的开发，更多是老板和产品经理定下开发需求，然后程序员这里抄一下、那里改一下，拼凑出一个勉强能用的网站或app，对于技术细节和整体架构很少关注，公司特别是创业公司更多的接项目搞钱，不太愿意投入资源去做偏底层的技术。
  - 也许将来我也会专注于搞钱，但精力一旦投入到业务和拉项目上，就很难深入技术了，年龄越大越难静下心来看技术原理和细节，所以近几年我一直把积累技术放在首位，希望尽快做出技术代表作，建立品牌和影响力。
  - 我不再挑剔去选自己喜欢的技术方向和公司，因为对公司而言只要产品结果和营销，还是需要在工作外挤时间，在个人项目中深入和完善技术细节。

- 👉🏻 产品盈利不明确
  - 近几年的开发工作，经常被问到商业模式和盈利计划，也许年龄大了后程序员不得不转管理。
  - 产品方向1: 面向大厂或投资人的创业或产品。这类产品并不需要有实际用户，模仿网红产品比如小红书、虾皮，在做出原型样板后，就卖给大厂或资本市场。以前我也鄙视，现在理解，并且认同，上家公司就是这类
  - 产品方向2: 以toB为主的产品。给企业定制编辑器或系统，侧重团队管理、权限控制，适合政府、企业合作
  - 产品方向3: 以toC为主的产品。类似wps、notion，侧重编辑体验和内容运营，适合个人创业
  - 以我对国内软件市场的了解，面向政企toB的市场已经被类似华为、金蝶、用友的头部公司占了大部分，偏向运营而不是技术，竞争很大，toC的产品需求大，可以尝试，面向大厂或投资人的产品也可以尝试，但需要最前沿的技术和快速开发。
  - 我一直侧重技术，但在产品方向上摇摆不定。暂时只能找份工作走产品2的方向，因为政企的需求是周期性且有预算的，在公司里面开发toB产品是大多数程序员的工作。

## 未来计划

- 四五月找工作时状态还行，最近状态不是很好，但我也深知不能再拖下去了，我会降低自己的期望和要求，然后开始新的工作，大概十月或十一月把你的借款还了。

- 👉🏻 积累技术，减少白干
  - 前些年写过很多代码和系统，但大多都是完成公司需求，然后一个做完了就下一个，没有注意积累
  - 我意识到以前很多工作都白干了，以后的技术和工作都会注意连续和可持续发展
  - 这也是我不急于工作而选择积累代表作的重要原因，就算通过面试入职了，然后呢，今天搬砖，明天继续搬砖，工作的时候很少能有喘息的机会

- 👉🏻 all in 表格编辑器
  - 从工作经历和市场产品上看，以编辑器为核心的产品层出不穷，我相信自己对技术和市场的判断
  - 普通文本编辑器亮点不够，我最近专注于打磨编辑器中的表格，尝试分离出去作为一个可独立的产品
  - 做得越深入就越能意识到需要技术的深度和广度，我模仿了很多表格类产品，但理解还不够深入
  - 我意识到不可能等自己都做好了再去工作，一是需要的时间精力是无底洞，二是我需要开始工作换个状态，不能一直这样下去

- 👉🏻 专注一个产品
  - 我本对产品和商务没那么大兴趣，但年龄到了后就不得不考虑甚至主导这些
  - 比较容易的状态是能够接几个toB企业定制化需求，然后通过产品2的思路和其他企业合作，养活自己和产品，在国内很可能就是接大厂的二层、三层、四层外包
  - 比较理想的状态是能够用前沿技术做出有特色的toC产品，这需要深厚的技术积累和敏锐的市场判断，在能比较稳定的养活自己后，我会更专注这个方向

- 再次感谢你对我的帮助，我也越来越理解你回老家和考公的选择，希望我们都能调整好状态，做自己想做的事 🤔
# 范新月致歉_202306
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
# yaoo-debt
- debt
  - 母亲三周年 20250825 - 南华叔-800多餐厅/2桌客
  - [x] 金敏小姐(2017) - 30000
  - [x] 大丫(2016) - 17000 + 2000
  - [x] 小姨(2016) - 20000 + 1500
  - mom
    - 6212 2518 0900 0758 487
    - 6212251809000758487

- debt-还款事项
  - 我是他大妈，我可以代表金瑶，一切事情都可以做主，欠钱的事件你可以处理
  - 📌 哪个平台，欠了多少钱
    - 确认双方有还款意愿
    - 明确诉求，只还本金
  - 📌 利息太多就去找他本人等到猴年马月他有钱了再还吧
    - 他总债务说是有二三十万，
    - 最近几年都没正经工作，一直在玩
    - 银行卡、微信、支付宝都被冻结了
    - 毕竟不是父母，多的债务处理不了，
  - 📌借钱清单、还款信息 发个短信: 本金、利息、时间
  - 结清证明怎么开，什么时候开

- 百度有钱花
  - 本金: 37910
  - 本金+利息: 66233
  - 95055
  - 记录
    - 金额: 4023, 对公账户已专注
  - 投诉处理 400 100 9891
  - ⏳ 处理进度

- 360借条 /本金在减少
  - 本金: 12900
  - 本金+利息: 37500
  - 官方 400-603-0360
  - 贷后 400 052 6663
    - 没有减免政策
  - 投诉处理 021-6151-5143
  - 国瑞金资
  - 金城银行 4006161888
  - 剩下的债务360处理
  - ⏳ 处理进度
    - 1118: 需要自己去找银行处理

- 头条放心借
  - 本金: 8476
  - 本金+利息: 17487
  - 95766
  - 投诉处理 4001098067
  - ⏳ 处理进度

- 美团借钱
  - 本金: 5404
  - 本金+利息: 5704
  - 95172
  - 5132.36
  - 天津银行 总客服 956056, 济南美团借钱客服 0531 67609560
  - ⏳ 处理进度
    - 只能app还款本金+利息

- ~~招商银行信用卡~~
  - 本金: 9249
  - 本金+利息: 10766
  - 400-820-5555
- ~~招联金融~~
  - 本金: 4360
  - 本金+利息: 7814
  - 95786
  - 400-001-2222

- ~~翼支付~~
  - 本金: 7956
  - 本金+利息: 10727

- 12378是国家金融监管总局的投诉电话，主要用于协调持卡人与银行之间的纠纷。
  - 12378并不直接干预银行的协商方案，但可以促进银行与持卡人之间的沟通。
 
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

- 银行卡冻结， 荆门市中级人民法院
  - 北海仲裁 冻结
  - 解冻的方法，都是协商+还款
  - [荆门市中级人民法院](http://jmzy.hbfy.gov.cn/)
  - [广西 北海仲裁委员会 北海国际仲裁院](https://www.beihaizhongcai.com/)

- 租房-象牙客
  - 15302974687 五妈
  - 13886920127 五爷
  - 电费 50元, 包周 248, 包月 858

- 王安迪
  - andywangkingluckii@outlook.com
  - AnDy.20080313

- 唐银生
  - 农业银行 6228 4804 7850 9920 979

- 日用品采购20250329
  - 衣: 运动袜
  - 食: ~~花生、豌豆~~ 瓜子
  - 住: 牙刷，马桶刷，毛巾，洗发水，电蚊香
  - 行: 运动鞋
  - 其他: 香水

## 结清证明

- 20251027-4900-中原消费金融-360借条
  - 中原消费金融官方客服热线：400-111-2233 (早9：00——晚21：00，全国热线)
  - 400-603-0360
  - 结清证明发送到 jinyaoo@qq.com, 密码是145597

- 20251029-20790-支付宝借呗-辽宁振兴银行
  - 956185
# yaoo-job-leave-20250711
- 缺点
  - 技术上，对编辑器表格协作类技术仍比较执着，对cicd/k8s运维不太熟练
  - 业务上，编辑器、IDE都是技术挑战大且难以商业化的方向
  - 性格上，不太会来事，表现自己的工作成果、写文档PPT

- 优点
  - 技术上，对编辑器表格协作类技术仍比较执着，专注于版本、协作、自动化
  - 业务上，目标比较专注，对熟悉业务能快速给出准确方案
  - 性格上，能快速融入团队

- 
- 
- 
