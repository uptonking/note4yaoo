---
title: lib-utils-input-form
tags: [form, input, utils]
created: 2023-03-27T17:44:58.947Z
modified: 2023-03-27T17:45:27.440Z
---

# lib-utils-input-form

# guide

# forms-examples
- https://github.com/jaredpalmer/formik /ts/react/代码少
  - https://formik.org/
  - Build forms in React, without the tears.
  - forks
    - https://github.com/sagarrajak/formikplusplus
    - https://github.com/astonmartin07/formik
    - https://github.com/DemoChimpDev/formik-with-sync
- https://github.com/formium/formium
  - https://formium.io/
  - Formium is an API-first, headless online form builder and automation tool
  - In addition to hosting forms and surveys on formium.io, you can use your own React components to natively render your forms and surveys in your existing apps 
  - 依赖 formik

- https://github.com/react-hook-form/react-hook-form /代码高度模块化
  - https://react-hook-form.com/
  - React Hooks for form state management and validation (Web + React Native)
  - 只依赖react
- https://github.com/kodkafa/reform
  - React Hook Form + Yup + Tailwind
  - Tailwind is optional. And you can use Preline UI too.

- https://github.com/TanStack/form /代码少
  - https://tanstack.com/form
  - type-safe form state management for the web.
  - Designed with first-class TypeScript support, headless UI components, and a framework-agnostic design

- https://github.com/final-form/react-final-form /js/vanillajs
  - https://github.com/final-form/final-form
  - react binding 代码也挺多
  -  The author of Redux Form took all of the lessons he learned about form use cases from maintaining Redux Form and built React Final Form

- https://github.com/ivan-dalmet/formiz
  - https://formiz-react.com/
  - React forms with ease! Composable, headless & with built-in multi steps

- https://github.com/alibaba/formily /ts/多框架
  - https://formilyjs.org/
  - High Performance Normal Form/Dynamic(JSON Schema) Form/Form Builder 
  - Support React/React Native/Vue 2/Vue 3
  - 阿里巴巴统一前端表单解决方案
  - 代码量大，功能全
  - Formily2.x 在实现的过程中发现 Mobx 还是存在一些不兼容 Formily 核心思想的问题，最终，只能重新造了一个轮子，延续 Mobx 的核心思想的 @formily/reactive
- https://github.com/charlzyx/fireformily
  - 尽可能符合 AntD × formily 直觉习惯
  - Dict - 远程词典
  - QueryList - 查询表格
- https://github.com/charlzyx/da
  - https://charlzyx.github.io/da/

## utils

- https://github.com/fabian-hiller/decode-formdata /ts
  - When the values of your form are encoded to FormData, for example to send them to a server via HTTP, some information is lost. 
  - Using this library, you can decode FormData into a JavaScript object and supplement the information that was lost during encoding.
# form-builder/lowcode
- https://github.com/surveyjs/survey-library /MIT/ts
  - https://surveyjs.io/form-library
  - Free JavaScript form builder library with integration for React, Angular, Vue, jQuery, and Knockout.
# more

# discuss

- ## 

- ## 

- ## Unpopular opinion: Don't use http verbs PUT, PATCH, DELETE. Just use POST for everything. Reasons:
- https://twitter.com/matthewcp/status/1716549522015310116
  - `<form>` doesn't support the others. Frameworks that allow it do so through hacks.
  - URLs are free, you don't gain anything by overloading them.
  - Purity < practicality
- A bunch of infra-adjacent stuff is easier if you use proper verbs. Eg. PATCH is idempotent, POST is not.
  - *PUT is idempotent, PATCH is not necessarily. (According to MDN)
  - This is good in theory but broken in modern practice. E.g. Next.js caches POST requests, probably because GraphQL uses them even for reads without side-effects.
  - I used to make this argument, but now I think it's over-rated and I agree with the OP. It's just too hard to make every form do the right thing with respect to updates vs. creates. Also, it's rare that retrying an update is really what you want.
- Simplicity that works >>>> anything else.

- ## 使用fetch()上传formData数据时，千万不要在headers中设定content-type！
- https://twitter.com/ahshengchen/status/1687377120459378688

- multipart/form-data 如果修改了content type会覆盖解析数据需要的boundary。标准server就解析不到数据了，可以用postman or paw之类的查看一下和application/x-www-form-urlencoded的报文区别。

- 可以 postman 里测好了，用他的代码生成代码

- ## Wrote a guide about 11 popular HTML and JS mistakes in forms.
- https://twitter.com/sitnikcode/status/1661411602443247616
  - [11 HTML best practices for login & sign-up forms—Martian Chronicles, Evil Martians’ team blog](https://evilmartians.com/chronicles/html-best-practices-for-login-and-signup-forms)
