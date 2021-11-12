---
title: draft-pastebin-pieces
tags: [draft, todo]
pinned: true
created: '2019-11-11T06:57:46.101Z'
modified: '2021-03-22T18:24:50.639Z'
---

# draft-pastebin-pieces

 

------  

- 图片base64编码示例

```
data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAOEAAADhCAMAAAAJbSJIAAAAhFBMVEX///+EMTGAJyeDLi6sfn5/JCR8GBiYV1fk1dW8l5d+ICDKsLB5DQ2CKyv9+vqcYGB6ExPYxMTw5+e3j4+OQ0N6EBB9HR2hamq/nZ3Su7umc3Pq39/cysp4BAS5kpJ7FxeIOTmRS0v38/PFpaWyiIjt5OSod3eINzeeZmaaXFyUUlKPSEjcOe1gAAAE6klEQVR4nO3dbVfaShSG4ZnEIAJRUAmgUKxw7LH9///v9GW51tHkCZM9k72Jfe7PBXIZCiHsIc6hbjfru146PMLH1Gz8Oq+KrJcm8/utNc+59a70/ZXv1ubAZY++X82NidtZz8CfxCtT4Y8+n6JvxC+GwHHfz9E/xDs74WGiIfT7o5nwIlMR+pEZUUvoRxefXegrI6Ke0FcPn11oRNQU2hBVhX6y+uxCC2JdmEfXSvzXXJjfR/fURiy0iTXhKP5T+bpoJb4m2OwO1YXj6Pu8ahVqEw2EvvieYMODsxDqEk2EPvt6nWDbw7IRahKNhD77oUW0Evrs/jnB5gdkJlQj2gl96VWIhkJfPmkQdYTgYLzMFYgqwvwVnLPUeKKqCCebKfjuoMxvEyBa0xFOHSSWfRO1hHZENaHbAGJe/BPPaElPiIlZr0RFISYmOK+A0xS6BfgqLy96JKoKMbHHvagrdNt58+FNXsU/LEhZiIn7vojaQrddAuK8J6K6UH0v6gvdGO3FWS/jUwZCN0Z7cd4H0ULoHkfgA+OuB6KJ0I0RcbmIfvSP2QjdY4X2YnKikRATl5vox3+fldA9ZoA4S0w0E7oNmjdLTLTbh/iU47LpDyLOSojeE//sxZREI+F43zrPkHIv2gi3s1bgzzeNQ/RWvGUi3J4e250nI1oI0Sf9dy1Tzb8bCBdhs/Op5t/1hZvQyfJERHUhOvfdREwy4q8t7AD0fp9ixF9ZeOi2+CEFUVeIgOUIDIEmGPFXFaIlVsXl9Qoch8cTNYUQ+GsIDBJjR/wVhV/mAHj5+1YPVT9EPSEEvg1jImLkQg014XF/AujcCyK+DEF4HDVv/eTmfzeExJhVDEqzGBcAWNy8uyX6Z1XEiL/OxNA38HZXm9xHxIhVDJZTX01LEyDxpuGBgrIUNu4Y9B+2kBINhWBxyd3pF91O2QnhC+SJI4OumQlb3gHSEq2Ere/iV4goWcVgJDxxmLIGxOx79/l3G+HJ47ADOBUgWMVgIgw4lj6gvdh5FYOFMOjz0HQHiPcdiQbCKuxj+xS89XddxVATVovb2I6tK2/L1XPQvTxfgbvpSKyvkq3msZ1YWlzG3k23VQzKK53TVH7rQByksNMqhmEKfRn+ijpQoZ8Ef6cxVKHfhT5PByusQr/qH6ywCH2aDlaYhZ5hHKywDD1vQ+HZRiGF5x+FLcL4H56tT+WVRWy1zZQLs5foHw9+/UgsH9ax1bZTLkxwnqb2K0qNU9Dd2n788tRUGDbn3a0FhTAKJVEoiUIchZIolEQhjkJJFEqiEEehJAolUYijUBKFkijEUSiJQkkU4iiURKEkCnEUSqJQEoU4CiVRKIlCHIWSKJREIY5CSRRKohBHoSQKJVGIo1AShZIoxFEoiUJJFOIolEShJApxFEqiUBKFOAolUSiJQhyFkiiURCGOQkkUSqIQR6EkCiVRiKNQEoWSKMRRKIlCSRTiKJREoSQKcRRKolAShTgKJVEoiUIchZLOXFiN3XVcjcLY+0wo9NUstvql8ybR91m7njWvjUDh+UchhecfhX+R8DhYYfO15+vVrgkzlLKwqwo7t91bb6qwahModL5+daZBVAVfanUKLvF95o0OoUDnHibWWytoEvpK+rvVfmhP1HzUCejcoaiyMh9KZVYV625A564Xx9XlUFodF/BF5j+Mt9zZWpXGVgAAAABJRU5ErkJggg==

```

- install app-ubuntu-calibre
 - sudo mkdir -p /opt/calibre && sudo rm -rf /opt/calibre/* && sudo tar xvf calibre-5.13.0-x86_64.txz -C /opt/calibre && sudo /opt/calibre/calibre_postinstall

- TO-DO: components、datable、chart

- 知乎禁止转载的回答测试
  - https://www.zhihu.com/question/25950466/answer/31731502
  - 只有复制内容较长时才会提示申请转载，比如复制超过150字

- webpack react fast refresh

```

"@pmmmwh/react-refresh-webpack-plugin": "^0.4.0-beta.7", 
"react-refresh": "^0.8.3", 

const ReactRefreshWebpackPlugin = require('@pmmmwh/react-refresh-webpack-plugin'); 

new ReactRefreshWebpackPlugin(), 

'react-refresh/babel', 
```

- webpack 5移除了node模块兼容

```

"crypto-browserify": "^3.12.0", 
"stream-browserify": "^3.0.0", 
"vm-browserify": "^1.1.2", 
```

- class extends

```js
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
