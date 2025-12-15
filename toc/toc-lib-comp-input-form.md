---
title: toc-lib-comp-input-form
tags: [components, form, input, toc, ui]
created: 2023-03-27T17:44:58.947Z
modified: 2023-11-23T18:01:59.304Z
---

# toc-lib-comp-input-form

# guide

# popular
- https://github.com/open-circle/formisch /519Star/MIT/202512/ts
  - https://github.com/fabian-hiller/formisch
  - https://formisch.dev/
  - https://stackblitz.com/edit/formisch-playground-solid
  - The modular and type-safe form library for any framework
  - Supported frameworks: React, Preact, Qwik, SolidJS, and Vue. Svelte will follow soon.
  - a schema-based, headless form library for JS frameworks. It manages form state and validation. 
  - its bundle size is small due to its modular design
  - Schema-based validation with Valibot
  - What makes Formisch unique is its framework-agnostic core, which is fully native to the framework you are using. It works by inserting framework-specific reactivity blocks when the core package is built
  - https://x.com/FabianHiller/status/1998402978697425084
    - how is it different from Tanstack form
    - It’s much smaller (~2.5 kB vs. >10 kB), but it also has less functionality than TanStack Form in its current state. One of the biggest differences is our modular design. So only what you use ends up in your final bundle. When you choose Preact, Qwik, SolidJS, Svelte, or Vue as the framework, we use the native reactivity system (signals), which should result in better performance
  - 🐛 [Support other schema libraries through Standard Schema _202507](https://github.com/open-circle/formisch/issues/2)
    - Yes, I can replace the Valibot-specific code with the Standard Schema interface for v1. I am a Standard Schema co-creator by the way. However, I must point out that Formisch initializes the form store (each state of the form is a signal) based on the schema structure, but Standard Schema does not provide this information because each schema library is implemented differently. Supporting multiple schema libraries would therefore require us to use adapters for each one, which would decrease DX. 
    - Until the library is more popular it is probably not worth investing time into supporting Zod or other schema libraries as I should probably focus on providing docs and support for meta frameworks first.
  - https://x.com/FabianHiller/status/1952545041341100173
    - What makes Formisch unique is its framework-agnostic core, It works by inserting framework-specific reactivity blocks when the core package is built. 
    - TanStack Form is implemented with a framework-agnostic core that has its own reactivity system. This system is then connected to the framework you are using via framework-specific adapters. This differs from how Formisch works under the hood.
  - https://github.com/fabian-hiller/modular-forms /同作者旧框架
    - The modular and type-safe form library for SolidJS, Qwik and Preact
    - [Support for Zod 4 _202509](https://github.com/fabian-hiller/modular-forms/issues/297)
      - 👷 the zodForm function is a really simple function. Here is the code. I recommend copy it to your project and upgrade it as I am more focused on Formisch right now

- https://github.com/jaredpalmer/formik /ts/react/代码少
  - https://formik.org/
  - Build forms in React, without the tears.
  - 🍴 forks
  - https://github.com/sagarrajak/formikplusplus
  - https://github.com/astonmartin07/formik
  - https://github.com/DemoChimpDev/formik-with-sync
  - https://github.com/formium/formium /BSL/202107/ts/inactive
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
  - The author of Redux Form took all of the lessons he learned about form use cases from maintaining Redux Form and built React Final Form

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

- https://github.com/formkit/formkit /4.6kStar/MIT/202411/ts/inactive
  - https://formkit.com/
  - FormKit is a form-authoring framework for Vue
  - supports its whole feature set for native HTML inputs (like select, checkbox, and textarea) 

- https://github.com/heyform/heyform /AGPLv3/202407/ts
  - https://heyform.net/
  - an open-source form builder that allows anyone to create engaging conversational forms for surveys, questionnaires, quizzes, and polls.
  - Smart Logic: Conditional logic and URL redirections for dynamic, adaptable forms.
  - powerful Integrations: Connect with webhooks, analytics, marketing platforms, and tools like Zapier and Make.com.
  - [Show HN: I just made my profitable online form builder open-sourced | Hacker News _202404](https://news.ycombinator.com/item?id=39895960)
    - Grist has the ability to create forms that are automatically connected to their spreadsheets. Though it doesn't seem like you can create sophisticated forms (with some logic in them for example) just yet.
    - As someone that built a 20m ARR survey product... The only difference between this and something making millions is a sales team.
    - I really like that you are using nestjs, idk why some devs hate it
    - Best makes JavaScript look like Java, it’s needlessly complex and just encourages vast amounts of boilerplate. Awful stuff.
# form-elements
- tom-select /947Star/apache2/202212/ts/vanillajs
  - https://github.com/orchidjs/tom-select
  - https://tom-select.js.org/examples/remote/
  - Tom Select is a dynamic, framework agnostic, and lightweight (~16kb gzipped) `<select>` UI control.
  - Tom Select was forked from `selectize.js` with the goal of modernizing the code base, decoupling from jQuery, and expanding functionality.
  - Options are efficiently scored and sorted on-the-fly (using sifter). 
  - https://github.com/orchidjs/sifter.js
    - A library for textually searching arrays and hashes of objects by property (or multiple properties). 
    - Designed specifically for autocomplete.
# utils
- https://github.com/fabian-hiller/decode-formdata /ts
  - When the values of your form are encoded to FormData, for example to send them to a server via HTTP, some information is lost. 
  - Using this library, you can decode FormData into a JavaScript object and supplement the information that was lost during encoding.
# form-builder/lowcode
- https://github.com/surveyjs/survey-library /MIT/ts
  - https://surveyjs.io/form-library
  - Free JavaScript form builder library with integration for React, Angular, Vue, jQuery, and Knockout.

- https://github.com/getodk/central-backend /apache2/202312/js
  - https://docs.getodk.org/central-intro/
  - the API server for ODK. It's built with Node.js and Postgres.
  - https://github.com/getodk/central-frontend /js/vue
# form/survey-SaaS
- https://github.com/didi/xiaoju-survey /3.3kStar/apache2/202502/ts/vue
  - https://xiaojusurvey.didi.cn/
  - 一套轻量、安全的调研系统，提供面向个人和企业的一站式产品级解决方案，用于构建各类问卷、考试、测评和复杂表单，快速满足各类线上调研场景。
  - Web   端：Vue3 + ElementPlus
  - Server端：NestJS + MongoDB
  - 内部系统已沉淀 40+种题型，累积精选模板 100+，适用于市场调研、客户满意度调研、在线考试、投票、报道、测评等众多场景。数据能力上，经过上亿量级打磨，沉淀了分题统计、交叉分析、多渠道分析等在线报表能力，快速满足专业化分析。
  - 多类型数据采集，轻松创建调研表单：文本输入、数据选择、评分、投票、文件上传等。
  - ⚖️ 制定了问卷标准化协议规范
    - 业务描述：问卷协议、题型协议
    - 物料描述：题型物料协议，包含题型和设置器
# more
