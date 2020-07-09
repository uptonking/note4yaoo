---
tags: [draft, todo]
title: draft-pieces
created: '2019-11-11T06:57:46.101Z'
modified: '2020-07-09T15:39:24.460Z'
---

# draft-pieces



进入存量市场后，技术大多用于维护现有用户，开拓新产品新市场价值高，难度也更高
 
------  

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

- bootstrap 4的breakpoints

``` 
$font-size-base:  1rem !default; // Assumes the browser default, `16px`
$font-size-lg: $font-size-base * 1.25 !default;
$font-size-sm: $font-size-base * .875 !default;

$grid-breakpoints: (
  xs: 0,
  sm: 576px,
  md: 768px,
  lg: 992px,
  xl: 1200px
) !default;
```

- react-data-grid使用的className
  - 不确定的类
      - row-selected， has-tooltip，has-error
  - 使用了的样式
      - pull-right
      - glyphicon-remove form-control-feedback
  - ChildRowDeleteButton组件使用了glyphicon glyphicon-remove-sign 
  - FilterableHeaderCell组件使用了form-group/control
