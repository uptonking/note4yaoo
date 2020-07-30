---
title: draft-pastebin-pieces
tags: [draft, todo]
pinned: true
created: '2019-11-11T06:57:46.101Z'
modified: '2020-07-30T13:52:49.242Z'
---

# draft-pastebin-pieces

- 贫血主要是指单位容积血液中红细胞计数或血红蛋白（Hb）浓度低于同龄或同性别健康人的正常值下限
  - 成人男子的血红蛋白低于 120 g/L，成人女子的血红蛋白低于 110 g/L 即为贫血。
  - 血红蛋白低于 30 g/L 为极重度贫血，30～60 g/L 为重度贫血，60～90 g/L 为中度贫血，90~110 g/L 为轻度贫血
- 糖尿病患者出现贫血的原因有很多，与糖尿病本身或糖尿病治疗直接相关的病因主要有饮食不当所致、降糖药物所致、慢性肾病所致
  - 糖尿病由于过度节食及偏食，特别是富含叶酸、维生素B12及铁质的瘦肉、鸡蛋、牛奶及新鲜果蔬摄入不足，导致营养不良或是贫血。
  - 长期服用某些降糖药物，也可引发贫血。如糖尿病患者服用双胍类药物，可以影响自身维生素B12和叶酸在肠道的吸收，导致DNA合成障碍，引起巨幼细胞性贫血。α-糖苷酶抑制剂也会导致患者发生体重下降、缺铁性贫血，可能与该药影响铁在肠道的吸收有关。
  - 慢性肾病也会所致糖友出现贫血，由于肾脏病变导致体内无法生成足够的促红细胞生成素，致使红细胞缺少，引发贫血。
  - 糖友首先要积极治疗引起贫血的原发疾病，如抗感染、抗结核、治疗消化性溃疡及月经不调等等。第二，糖友需要调整饮食结构及降糖药物，适当增加蛋白质及新鲜蔬菜的摄入，如能确定贫血与服用某种降糖药物有关，则应及时换用其他降糖药物或胰岛素。
  - 如果发现指甲、手掌皮肤皱纹处以及口唇黏膜和眼睑等处皮肤黏膜苍白，且有疲倦、乏力、头晕、耳鸣、记忆力衰退、思想不集中等症状，糖尿病患者应到医院做相关检测，确认自己是否已经处于贫血早期状态。
  - 在饮食方面，糖尿病人的饮食应该有规律，在平衡膳食结构的基础上，适量的食用含铁丰富的食物，如猪肝、猪血、瘦肉、奶制品、豆类、大米、苹果、绿叶蔬菜等。忌暴饮暴食，忌食辛辣、生冷不易消化的食物。
- ref
  - [糖尿病与贫血的那些事儿](http://endo.dxy.cn/article/511665)

------  

- 知乎禁止转载的回答测试
  - https://www.zhihu.com/question/25950466/answer/31731502
  - 只有复制内容较长时才会提示申请转载，比如复制超过150字

- webpack react fast refresh

"@pmmmwh/react-refresh-webpack-plugin": "^0.4.0-beta.7", 
"react-refresh": "^0.8.3", 

const ReactRefreshWebpackPlugin = require('@pmmmwh/react-refresh-webpack-plugin'); 

new ReactRefreshWebpackPlugin(), 

'react-refresh/babel', 

- webpack 5移除了node模块兼容

"crypto-browserify": "^3.12.0", 
"stream-browserify": "^3.0.0", 
"vm-browserify": "^1.1.2", 

- class extends

``` js
class B {
  print = () => {
    console.log('print b');
  }
}

class D extends B {
  print() {
    console.log('before-super-print');
    super.print();
    console.log('after-super-print');
    console.log('print d');
  }
}

const d = new D();
d.print();
d.__proto__.print()
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
- emotion的button

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
