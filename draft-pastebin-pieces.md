---
title: draft-pastebin-pieces
tags: [draft, todo]
pinned: true
created: '2019-11-11T06:57:46.101Z'
modified: '2020-07-30T13:52:49.242Z'
---

# draft-pastebin-pieces

 
- todo 测试ag-grid行中行嵌套的rowModel
- import ag-grid的ts源码进行开发出现的error
  - babel class decorator  Cannot access  before initialization

``` 
Uncaught ReferenceError: Cannot access 'Component' before initialization
at Module.Component (component.ts:3)
at eval (agAbstractLabel.ts?deaf:14)
at Module .../widgets/agAbstractInputField.ts
```

- babel编译ag-grid源码中的types出现warning
  - 这些warning相关的导出内容都是type类型定义，可忽略

``` 
WARNING in ../../community-modules/core/src/ts/main.ts 13:0-84
export 'ColumnState' (reexported as 'ColumnState') was not found in './columnController/columnController' (possible exports: ColumnController)
```

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
