---
title: spec-design-theming-rfc
tags: [design, rfc, spec, styling, theming]
created: '2021-01-03T19:45:55.016Z'
modified: '2021-01-04T17:07:56.548Z'
---

# spec-design-theming-rfc

# guide

- theme-spec pros
  - 规范design tokens样式值属性名和属性值类型，为互操作的样式提供了可能性

- theme-spec cons
  - 没有提供具体平台相关样式的处理方式
    - 比如一个属性值引用另一个属性变量时，是该直接输出值，还是保留变量(css vars)

# theme-specification

- System UI Theme Specification
  - https://github.com/system-ui/theme-specification
  - https://system-ui.com/theme/
- ref
  - System UI is an open source organization that houses a Theme Specification for creating interoperable UI components.
  - https://mitchgavan.com/styleguide-driven-development/
  - https://github.com/primer/components/blob/master/src/theme.js

- who is using
  - theme-ui
    - styled-system, onno, xstyled
  - chakra-ui
    - blockstack-ui
  - github primer components
  - priceline design system
  - looker components
  - mineral-ui
  - pulse-boilerplate
  - more
    - cactus, flame, w-design

- 对样式主题的需求
  - If you’ve ever worked on a large application that has been worked on by many different people over time, you know that consistency can be hard to maintain. 
  - The amount of different colors, spacing, font-sizes and media queries can easily get out of control. 
  - Having a style guide combats that by providing a set of constraints that your application’s UI should adhere to, helping to maintain a consistent look and feel.
  - Having a style guide also leads to a more enjoyable developer experience. 
    - There’s less time spent worrying about the precision values, such as a specific padding value
  - common style such as UI Theme Spec makes themes portable between libraries

- 样式的写法
  - 采用类似内联样式的style对象更方便查看，但采用类似className性能更高
  - css属性名编写时的代码提示，可在样式库解决，也可在ide解决，也可借助ts
    - 只需要代码提示，没必要用typestyle库
    - csstype provides autocompletion and type checking for CSS properties and values
    - styled-system让组件上的css属性有提示且有限制，但要使用styled组件写法
    - typestyle书写样式对象返回className，和emotion类似，但写样式有提示，样式对象要作为参数传入style()，类似于emotion的css()
    - typestyle基于free-style，两者都存在一个问题，嵌套时内层逗号分隔的选择器只在最后一个选择器元素处生效

# theme-examples

- examples

## theme-ui-base

``` JSON
{
  "space": [
    0,
    4,
    8,
    16,
    32,
    64,
    128,
    256,
    512
  ],
  "fonts": {
    "body": "system-ui, -apple-system, BlinkMacSystemFont, \"Segoe UI\", Roboto, \"Helvetica Neue\", sans-serif",
    "heading": "inherit",
    "monospace": "Menlo, monospace"
  },
  "fontSizes": [
    12,
    14,
    16,
    20,
    24,
    32,
    48,
    64,
    96
  ],
  "fontWeights": {
    "body": 400,
    "heading": 700,
    "bold": 700
  },
  "lineHeights": {
    "body": 1.5,
    "heading": 1.125
  },
  "colors": {
    "text": "#000",
    "background": "#fff",
    "primary": "#07c",
    "secondary": "#30c",
    "muted": "#f6f6f6"
  },
  "styles": {
    "root": {
      "fontFamily": "body",
      "lineHeight": "body",
      "fontWeight": "body"
    },
    "h1": {
      "color": "text",
      "fontFamily": "heading",
      "lineHeight": "heading",
      "fontWeight": "heading",
      "fontSize": 5
    },
    "h2": {
      "color": "text",
      "fontFamily": "heading",
      "lineHeight": "heading",
      "fontWeight": "heading",
      "fontSize": 4
    },
    "h3": {
      "color": "text",
      "fontFamily": "heading",
      "lineHeight": "heading",
      "fontWeight": "heading",
      "fontSize": 3
    },
    "h4": {
      "color": "text",
      "fontFamily": "heading",
      "lineHeight": "heading",
      "fontWeight": "heading",
      "fontSize": 2
    },
    "h5": {
      "color": "text",
      "fontFamily": "heading",
      "lineHeight": "heading",
      "fontWeight": "heading",
      "fontSize": 1
    },
    "h6": {
      "color": "text",
      "fontFamily": "heading",
      "lineHeight": "heading",
      "fontWeight": "heading",
      "fontSize": 0
    },
    "p": {
      "color": "text",
      "fontFamily": "body",
      "fontWeight": "body",
      "lineHeight": "body"
    },
    "a": {
      "color": "primary"
    },
    "pre": {
      "fontFamily": "monospace",
      "overflowX": "auto",
      "code": {
        "color": "inherit"
      }
    },
    "code": {
      "fontFamily": "monospace",
      "fontSize": "inherit"
    },
    "table": {
      "width": "100%",
      "borderCollapse": "separate",
      "borderSpacing": 0
    },
    "th": {
      "textAlign": "left",
      "borderBottomStyle": "solid"
    },
    "td": {
      "textAlign": "left",
      "borderBottomStyle": "solid"
    },
    "img": {
      "maxWidth": "100%"
    }
  }
}
```

## theme-ui-bulma

``` json
{
  "colors": {
    "black": "hsl(0, 0%, 4%)",
    "blackBis": "hsl(0, 0%, 7%)",
    "blackTer": "hsl(0, 0%, 14%)",
    "greyDarker": "hsl(0, 0%, 21%)",
    "greyDark": "hsl(0, 0%, 29%)",
    "grey": "hsl(0, 0%, 48%)",
    "greyLight": "hsl(0, 0%, 71%)",
    "greyLighter": "hsl(0, 0%, 86%)",
    "whiteTer": "hsl(0, 0%, 96%)",
    "whiteBis": "hsl(0, 0%, 98%)",
    "white": "hsl(0, 0%, 100%)",
    "orange": "hsl(14,  100%, 53%)",
    "yellow": "hsl(48,  100%, 67%)",
    "green": "hsl(141, 71%,  48%)",
    "turquoise": "hsl(171, 100%, 41%)",
    "cyan": "hsl(204, 86%,  53%)",
    "blue": "hsl(217, 71%,  53%)",
    "purple": "hsl(271, 100%, 71%)",
    "red": "hsl(348, 100%, 61%)",
    "text": "hsl(0, 0%, 29%)",
    "background": "hsl(0, 0%, 100%)",
    "primary": "hsl(217, 71%,  53%)",
    "muted": "hsl(0, 0%, 96%)",
    "info": "hsl(204, 86%,  53%)",
    "success": "hsl(141, 71%,  48%)",
    "warning": "hsl(48,  100%, 67%)",
    "danger": "hsl(348, 100%, 61%)",
    "light": "hsl(0, 0%, 96%)",
    "dark": "hsl(0, 0%, 21%)",
    "modes": {
      "invert": {}
    }
  },
  "fonts": {
    "body": "BlinkMacSystemFont, -apple-system, \"Segoe UI\", \"Roboto\", \"Oxygen\", \"Ubuntu\", \"Cantarell\", \"Fira Sans\", \"Droid Sans\", \"Helvetica Neue\", \"Helvetica\", \"Arial\", sans-serif",
    "heading": "inherit",
    "monospace": "monospace"
  },
  "fontSizes": [
    "0.75rem",
    "0.875rem",
    "1rem",
    "1.25rem",
    "1.5rem",
    "1.75rem",
    "2rem",
    "2.5rem",
    "3rem"
  ],
  "fontWeights": {
    "body": 400,
    "heading": 700,
    "bold": 700,
    "light": 300,
    "medium": 500,
    "semibold": 500
  },
  "space": [
    "0rem",
    "0.5rem",
    "1rem",
    "1.5rem",
    "2rem",
    "2.5rem",
    "3rem"
  ],
  "styles": {
    "root": {
      "fontFamily": "body",
      "lineHeight": "body",
      "fontWeight": "body"
    },
    "a": {
      "color": "primary",
      "textDecoration": "none",
      ":hover": {
        "textDecoration": "underline"
      }
    },
    "h1": {
      "fontFamily": "heading",
      "fontWeight": "heading",
      "lineHeight": "heading",
      "m": 0,
      "mb": 1,
      "fontSize": 6,
      "mt": 2
    },
    "h2": {
      "fontFamily": "heading",
      "fontWeight": "heading",
      "lineHeight": "heading",
      "m": 0,
      "mb": 1,
      "fontSize": 5,
      "mt": 2
    },
    "h3": {
      "fontFamily": "heading",
      "fontWeight": "heading",
      "lineHeight": "heading",
      "m": 0,
      "mb": 1,
      "fontSize": 4,
      "mt": 3
    },
    "h4": {
      "fontFamily": "heading",
      "fontWeight": "heading",
      "lineHeight": "heading",
      "m": 0,
      "mb": 1,
      "fontSize": 3
    },
    "h5": {
      "fontFamily": "heading",
      "fontWeight": "heading",
      "lineHeight": "heading",
      "m": 0,
      "mb": 1,
      "fontSize": 2
    },
    "h6": {
      "fontFamily": "heading",
      "fontWeight": "heading",
      "lineHeight": "heading",
      "m": 0,
      "mb": 2,
      "fontSize": 1
    },
    "code": {},
    "pre": {},
    "hr": {
      "bg": "muted",
      "border": 0,
      "height": "1px",
      "m": 3
    }
  }
}
```
