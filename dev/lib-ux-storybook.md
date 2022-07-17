---
title: lib-ux-storybook
tags: [lib, storybook, utils]
created: 2021-01-18T06:23:43.506Z
modified: 2021-05-13T03:05:37.665Z
---

# lib-ux-storybook

# guide

- canvas中显示的部分是基于`iframe`实现

- 关于组件与文档设计
  - 复用文本过于灵活，需要各种解析器
  - 复用js函数则设计更清晰、复用更简单(特别是纯函数)

- alternatives to storybook
  - https://github.com/remorses/vitro
    - Vitro is a storybook alternative that builds 20x faster; built on top of esbuild (thanks to bundless)
  - https://github.com/ccontrols/component-controls
    - Using MDX or javascript to author documentation files, the sites can be generated with highly-optimized site generators as gatsby or nextjs, storybook

- ref
  - [storybook docs rfc](https://docs.google.com/document/d/1D4Ov4UvrB80Uy1CLGshbFEWQKWEpr8dL4FmOqRDwjwI/edit)
  - [storybook args rfc](https://docs.google.com/document/d/1Mhp1UFRCKCsN8pjlfPdz8ZdisgjNXeMXpXvGoALjxYM/edit)
    - Args is a proposed addition to Storybook’s CSF
  - [React Single File Components Are Here](https://www.swyx.io/react-sfcs-here/)
  - [Storybook Docs MDX usage example](https://github.com/storybookjs/storybook/blob/master/addons/docs/docs/mdx.md)
# pieces

# storybook-docs

- Component Story Format (CSF) with DocsPage
  - Storybook's Component Story Format (CSF) is a convenient, portable way to write stories. 
  - DocsPage is a convenient, zero-config way to get rich docs for CSF stories. 
  - Using these together is a primary use case for Storybook Docs.
- Pure MDX stories
  - MDX is an alternative syntax to CSF that allows you to co-locate your stories and your documentation. 
  - Everything you can do in CSF, you can do in MDX. 
  - And if you're consuming it in Webpack, it exposes an identical interface, so the two files are **interchangeable**. 
  - Some teams will choose to write all of their Storybook in MDX and never look back.

- ## CSF Stories with MDX Docs 在mdx中导入csf的stories
  - write your stories in CSF, but document them in MDX

```mdx
// Button.stories.js

import React from 'react';
import { Button } from './Button';

export const basic = () => <Button>Basic</Button>;
basic.parameters = {
  foo: 'bar',
};

// Button.stories.mdx

import { Meta, Story } from '@storybook/addon-docs/blocks';
import * as stories from './Button.stories.js';

<Meta title="Demo/Button" component={Button} />

# Button

I can define a story with the function imported from CSF:

<Story story={stories.basic} />

And I can also embed arbitrary markdown & JSX in this file.
```

- ## CSF Stories with arbitrary MDX 在csf中导入任意mdx

```

// Button.mdx 注意名称后缀不是.stories.mdx
// 本文件会被mdx loader处理，不要使用Meta定义标题了，挂载点不在这里

import { Story } from '@storybook/addon-docs/blocks';

# Button

I can embed a story (but not define one, since this file should not contain a `Meta`):

<Story id="some--id" />

And I can also embed arbitrary markdown & JSX in this file.

// Button.stories.js 主要提供在文档目录树中的挂载点

import React from 'react';
import { Button } from './Button';
import mdx from './Button.mdx';
export default {
  title: 'Demo/Button',
  parameters: {
    docs: {
      page: mdx,
    },
  },
  component: Button,
};
export const basic = () => <Button>Basic</Button>;
```

## [MDX-flavored Component Story Format (CSF)](https://storybook.js.org/docs/react/api/mdx)

- [Component Story Format (CSF)](https://storybook.js.org/docs/react/api/csf) is the recommended way to write stories. 
  - It's an open standard based on ES6 modules that is portable beyond Storybook.
  - CSF本身是基于es6 module的js文件，不是普通的文本格式
  - mdx可作为csf的完全替代，但mdx中需要显式import Story/Canvas/Meta
- In CSF, stories and component metadata are defined as ES Modules. 
  - Every component story file consists of a required default export and one or more named exports.
  - CSF is supported in all major frameworks except React Native

- MDX is a standard file format that combines Markdown with JSX. 
- MDX is the syntax Storybook Docs uses to capture long-form Markdown documentation and stories in one file.
- You can also write pure documentation pages in MDX and add them to Storybook alongside your stories.
- MDX-flavored Component Story Format (CSF in `*.stories.mdx`)  includes a collection of components called "Doc Blocks", that allow Storybook to translate MDX files into storybook stories. 
  - MDX-defined stories are identical to regular Storybook stories, so they can be used with Storybook's entire ecosystem of addons and view layers.
- There's a one-to-one mapping from the code in MDX to CSF, which in turn directly corresponds to Storybook's internal `storiesOf` API. 
  - As a user, this means your existing Storybook knowledge should translate between the three. 
  - And technically, this means that the transformations that happen under the hood are simple and predictable.
- Documentation-only MDX
  - Typically, when you use Storybook MDX, you define stories in the MDX documentation is automatically associated with those stories.
  - If you don't define stories in your MDX, you can write MDX documentation and associate it with an existing story, or embed that MDX as its own documentation node in your Storybook's navigation.
# storybook-web-components
- [Storybook for web components on steroids](https://dev.to/open-wc/storybook-for-web-components-on-steroids-4h29)
  - For demoing, documenting and showcasing different states of your Web Component, we recommend using storybook.
  - https://github.com/open-wc/open-wc/tree/master/packages/demoing-storybook
- [Demoing: Storybook](https://open-wc.org/docs/demoing/storybook/)

- examples
  - [html-kitchen-sink](https://github.com/storybookjs/storybook/tree/next/examples/html-kitchen-sink)
  - [web-components-kitchen-sink](https://github.com/storybookjs/storybook/tree/next/examples/web-components-kitchen-sink)
# ref
- [Build a Web Component library with Stencil and Storybook](https://dev.to/ofhouse/build-a-web-component-library-with-stencil-and-storybook-c27)
- [Storybook Controls w/ CRA & TypeScript](https://gist.github.com/shilman/69c1dd41a466bae137cc88bd2c6ef487)
