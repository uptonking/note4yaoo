---
title: lib-ux-style-dictionary-dev
tags: [devtools, engineering, lib, style-dictionary, utils]
created: 2021-01-02T18:05:21.074Z
modified: 2021-05-13T03:05:54.852Z
---

# lib-ux-style-dictionary-dev

# guide

- s-d pros
  - 方便将design tokens输出到各个平台
  - 支持输出scss，也支持输出css vars，所以可以针对ie浏览器build输出合适的格式

- s-d cons
  - ~~在输出css vars时，不支持一个变量值引用了多个其他变量的情况，如hsl, border~~
  - ~~不直接支持生成pseudo class的类名，可自己实现，分析有无此需求~~
  - ~~暂不支持输出文件的值中包含`var(--name)`形式的css变量~~

- s-d书写属性值时不够灵活
  - ~~书写颜色值时，没有提供改变颜色变量透明度alpha的方法~~
    - 现已支持hsl的方式
  - 没有提供拼接引用变量名的api，但已支持直接替换引用变量
  - 没有提供简单算术运算的方法，但可利用自定义transformer

- tips
  - 参考 w3c-design-tokens 规范，实现json解析与转换
  - 基于theme specification定义输出design tokens的类别和名称
    - 具体可参考theme-ui预置主题对应的(https://theme-ui.com/demo/)，可转换到w3c格式
  - 可以将每个组件的design tokens输出到单独的文件(利用自定义filter)
  - 可以输出扁平化无嵌套的样式变量，
    - 也可以输出时设置最外层的选择器名，如`:root{}` 或 `.dark-theme{}`
  - 输出的值也可以使用 css vars
  - 使用js对象书写color的value时，hsl不会自动计算

- style-dictionary不支持名为value的中间属性名，如`{ "color": { "font": { "value": "#111" , "secondary": { "value": "#333" }, } } }`
  - 若在中间设置了value属性，则同级和下级属性都不会输出了
  - 变通方案：对要输出的中间属性名，增加一个中间属性名 `.val`

- extensions
  - 可自定义输出的format，自动生成简单的单页文档，类似theo输出html

- 如何实现依次依赖的3套主题，如bs, bs-flat, bs-flat-dark
  - **对于在`include`或`source`设置的路径数组，后面路径中的同名属性值会覆盖前面路径中的值**，而不会抛出异常
  - 若source中存在token属性名相同，默认会使用s-d内部排序的最新值，不会抛出异常，可通过编译，但会在控制台输出冲突的token名
  - 对于bs和bs-flat，直接用 include 和 source
    - bs写值，bs-flat直接写新值去覆盖bs，只需要属性名相同
  - 对于bs-flat和bs-flat-dark，可直接将bs和bs-flat依次配置在include中
    - 还可参考 [multi-brand-with-defaults](https://github.com/dbanksdesign/style-dictionary-multi-brand-with-defaults)

- transformer
  - 在循环处理各转换项时，碰到包含引用的会跳过
  - [Custom value transforms skip values with aliases](https://github.com/amzn/style-dictionary/issues/451)
    - Notably the transform step skips doing any value transforms on values that reference other values.
    - The original intent was that the aliased token should already be properly transformed for the given format.

- formatter
  - 可以在自定义formatter中灵活生成各种输出

- 建议使用js书写tokens，计算工具库更丰富，
  - 适合以后生成gradient
  - polished提供的方法分类：mixins，color，shorthands，easing
  - 方便修改变量名前缀prefix

- 组件的样式不推荐使用style-dictionary书写
  - s-d虽然能提供sass的variables、functions、mixins、nested、import等功能，
    - 同名变量的覆盖可以用source覆盖include，但不能只在某一个文件中覆盖该文件中的所有变量，css属性名非常灵活且容错性高
    - 变量只能全部输出css variables，不能只输出某部分为css vars
  - 但s-d在以下几个方面不如sass
    - 通常输出的样式文件格式仍然是scss，此时若手动编辑scss以后更新tokens就会丢失
    - 书写多层嵌套nested的样式时实现自定义format就很复杂
    - 书写sass支持的placeholder自动转换成群组选择器，很难实现
    - sass在大公司的支持度很高
    - 基于自定义action可以输出component样式，后期可以考虑单独实现此方案，不冲突

- config
  - ~~source配置时，tokens文件的声明顺序不重要，可以先写依赖了其他tokens的目录，再写依赖所在的目录~~
    - include和source数组在配置时，后面路径中的同名属性值会覆盖前面路径中的值

- color变量的value值
  - 若包含outputAsItIs配置，则跳过颜色转换原样输出，适合作为通用变量
    - 对其他类型的值，会执行默认的color/css转换计算
- 不能直接修改css变量颜色值的alpha透明度
  - 但可以 `--color: 240, 240, 240;` `color: rgba(var(--color), 0.8);`
  - 问题是前者不是style-dictionary合法的颜色值
  - 无法动态修改css变量的颜色值，同时又让style-dictionary读取这个更改，因为s-d的应用场景是统一管理设计变量，值明确的变量，css vars过于灵活

- halfmoon的颜色变量
  - --blue-color-hsl:var(--c-h), var(--c-s), 10%
    - --blue-color:hsl(var(--blue-color-hsl))
    - 注意对于kv声明，只有后一个是合法的css样式值，所以用户只用后者，前者只被开发者内部使用
  - --dm-base-text-color: hsla(var(--white-color-hsl), 0.8); 
    - 此颜色由浏览器动态添加透明度，s-d难以实现，因为两个变量都要输出，而s-d需要输出的变量一般是合法的有效值(token)

- **书写hsl格式的color时要注意**
- 不支持带透明度的值如hsla，需要转换成rgba
- 对不包含变量引用的hsl裸数字值，s-d默认会自动转换，
  - 若hsl都为字符串，会正常输出
  - 若h为数字，则css vars获取引用时，要使用 `dictionary.getReference(p.original.value.h.toString())`
  - 对s, l用字符串即可，支持 `50%/50/0.5` 三种形式，但用自定义工具hslToHex时注意参数格式要求
- 对包含变量引用的hsl，
  - 若hsl属性值hslobjwithref包含引用，则必须用50%，不能用50或0.5

- roadmap
  - [Changelog](https://github.com/amzn/style-dictionary/blob/3.0/CHANGELOG.md)
# examples

## w3c-design-token

- https://github.com/drwpow/cobalt-ui
  - https://cobalt-ui.pages.dev/
  - Cobalt turns your W3C design tokens into code
  - The general approach is similar to Style Dictionary or Universal Design Tokens to solve the problem of creating a single source of truth for design tokens that is platform-agnostic and easy to build tooling for.

- https://github.com/lukasoppermann/style-dictionary-utils
  - a collection of parsers, filters, transformers and formats for Style Dictionary that make working with w3c design tokens a lot easier.
# faq
- ## style-dictionary vs theo
- Theo uses json, json5 or yaml and takes a file-in file-out strategy.
- Style Dictionary uses json or JS modules and merges all token files into 1 big object.
- ref
  - 工具要考虑实现或集成：theming, css in js
  - You can also create a custom tool (Adobe did this).
  - 甚至考虑用通用工具如google spreadsheet来存放tokens

- ## 是否该用工具生成design tokens外，还生成所有组件的样式？
- 若自动生成所有组件样式
  - 极大提高复用性，所有组件的样式都自动生成了，但对生成工具高依赖、高要求
  - 不支持 伪类
- 若手写各个组件的样式
  - 极大提高组件设计修改的灵活性，花费更多精力，针对某一平台进行优化更方便
- 用style-dictionary来写所有组件的样式，还是只书写通用变量
  - 若书写所有，则最大化跨平台的收益，但变量处理逻辑还有很多异常
  - 若只书写tokens，则需要再用sass来书写组件样式
- 折中方案
  - 用工具只生成各个变量，然后手写各组件样式时只用变量值

- ## referencing/alias transform vs transitive transform
- Before version 3.0, Style Dictionary did not have transitive transforms though. 
  - While you could reference non-token values, you would not be able to then transform the value if it had a reference in it.
- the current(v2) implementation only transforms and resolves once, and transformation on values containing references do not work.
  - it would iterate through the merged object and transform tokens it found, but only do value transforms on tokens that did not reference another token.
  - The original intent here was that a value of any reference should be the same for all references of it, so we only need to do a value transform once.
  - Then after all tokens are transformed, resolve all aliases/references.
- This 3.0 change enables this transitive dependencies, by executing "transform & resolve" until all transformations are executed.
- transitive
  - 支持引用非样式值，能获取json数组中某索引下标的值，如分开存放rgb/hsl
  - 支持添加自定义属性如modify，然后tranform引用值

- ## output css vars
- [feat(format): adding ability to have variables in output_202012](https://github.com/amzn/style-dictionary/pull/504)
  - Adding a `useVariables` configuration on SCSS, CSS, and Less variables formats to make use of this
- [Feature/css var deep_202008](https://github.com/amzn/style-dictionary/pull/428)
  - This one also currently supports CSS variables flat, split out dark tokens

- ## 是否要在输出样式的顶层，再加上一层`:root{}`或 `.dark-theme{}`
- tokens值一般要在具体组件的scss中使用，而不是具体某个组件的类
  - 若要生成具体组件的css，用主流css预处理器更好
- [I can't generate css variables to a specific class_202007](https://github.com/amzn/style-dictionary/issues/448)
  - You could write a custom format that does this too if you can't wait for that change to be made into the core library

- ## 不输出一个大文件，而输出各小文件
- [feat(examples): add matching build files example](https://github.com/amzn/style-dictionary/pull/481)
  - example of automatically generating 1:1 token files based on a custom filter.

- ## 如何生成tokens的简单说明文档，类似theo输出html format
- [Style guide? ](https://github.com/amzn/style-dictionary/issues/477)

- ## [Specifications for property values](https://github.com/amzn/style-dictionary/issues/461)
  - I am currently working on a figma plugin to extract and prepare design tokens to be converted using the style-dictionary. 
  - I feel it would be helpful to specify how certain properties should be defined
- How should units be specified?
  - Units can be specified in the value, like "2rem". 
  - As you noticed in the next question, some of the examples don't have units and you can't really tell what unit they are specifying. 
  - This is because the transforms used in the configuration like 'size/remToPx' are simplistic in that they just parse the value for a number and assume it is either pixels or rems.
- Are size values in pixel units always omitted?
  - Not necessarily, but because all the transforms right now make assumptions of what unit they are specifying by which transform you are using in your config, specifying a unit is not necessary. 
  - The size transforms right now are just parsing for a number, so technically you could have "12rem", "12px", or "12pixels" and the would all be parsed to the number 12, and then based on which transform is run could output "12px", "144px", or "0.75rem".
- Should colors always be specified as a hex value?
  - Colors can be specified as a hex or as any string or object that tinycolor can understand.
- How should gradient fills be specified?
  - We don't yet have a built-in way to deal with gradients right now. 
  - there is no built-in way doesn't mean we can't handle it
- How should shadows & effects be specified?
  - For shadows again, there is not a built-in way yet.
  - Defining the structure of a shadow that can be transformed to different platforms would be great to have built-in transforms for.
- How corner radii be specified?
  - Because radii are a size, under the CTI structure they would go under the "size" namespace.
- How borders/strokes be specified?
  - there aren't built-in transformers for borders yet, but that would be good to add.
- Specific categories
  - It seems there are expected categories to allow for transformation 
  - However I can not find any place in the documentation where they are specified. 

- ## [Adds prefix option for scss/map-deep format](https://github.com/amzn/style-dictionary/pull/372)
- We already do allow prefixes, but they are in the name transforms
- The only difference would be you need to add the "prefix" attribute to the platform object rather than the file object
# pieces
- ## component tokens
- [json to scss](https://github.com/amzn/style-dictionary/issues/492)
  - 方法1
    - The way I would do this is create a custom format and template.
  - 方法2
    - 使用action实现本质上是修改自动生成的样式文件，甚至可以提取为单独的项目来实现
    - I have done something similar in some projects, but instead used a custom action to build the files.
    - The action grabs parts of the dictionary under the component namespace and passes the entire component object to a formatter to generate the SCSS file. 
    - This way you can add more components without needing to add more files to the configuration.
- [Should we consider token organization a primary use case?](https://github.com/amzn/style-dictionary/issues/268)
  - people are using style dictionary both to create original design tokens AND to reference them into specific components. 
    - In this case it is clear that the file organization is representative of that "both" structure.
  - This is all fine until you need to output those tokens. 
  - So while we support the use case, we do so only in a round-about way and require technical knowledge.
  - It is my belief that if we want to enable simple design token control for people, we should probably make this a direct goal and engineer a simple solution.
  - We avoid being opinionated on how you want to organize your tokens, but try to help somewhat by providing value/functionality if you use the CTI model.

- ## s-d examples
- component-cti
  - All of the built-in transforms target tokens using the CTI attributes.
    - The built-in `attribute/cti` transform adds the CTI attributes to each token based on the object path of the token. 
  - In this example we override the default behavior of the `attribute/cti` transform to apply CTI attributes based on token's key, or last part of the object path to generate the equivalent category and type. 
    - This way we can correctly map a token with an object path of `component.button.background-color` to a category of `color` and type of `background`.
    - we monkey patch the `attribute/cti` transform to look at the top-level namespace of the token and if it is 'component', 
      - instead of running the default attribute/cti transform, it instead looks at the last part of the object path to generate the equivalent category and type.
    - This example uses CSS property names, but you could also change it to use similar React/CSS-in-JS names like 'backgroundColor' instead of 'background-color'.
  - Style Dictionary allows for extensibility through monkey patching. 
    - This allows you to override the default behavior of the Style Dictionary library, and any built-in transforms and formats.
    - You can override built-in transforms and formats by adding ones with the same name. 
    - Also, all of the built-in transforms, transformGroups, and formats are available by accessing them in the Style Dictionary library under the attributes transform, transformGroup, and format respectively. 
  - `propertiesToCTI`: A plain object where we map the CSS property name to the proper category and type.

- custom-formats-with-templates
  - This example shows how to generate design tokens files with custom formats using "custom" template files/engines. 
    - registerFormat API method is invoked, passing a custom name for the format (whatever string you like) and a formatting function that returns the content to be saved to file.
    - For the formatting function, it's possible to use any templating language (Lodash, Mustache, PUG, anything that can return a string). 
  - This is useful when you need to distribute your design tokens and integrate them with custom pipelines or scripts, that expect specific formats
  - web-scss.template: this is a template that uses Lodash`_.template`
  - android-xml_alt.hbs: this is an alternative example of custom XML format for Android, that uses Handlebar as templating language.

- custom-transforms
  - This example shows how to use custom transforms (and transformGroups) to apply custom "transformations" to the properties when converted to design tokens.
  - The reason for transforms is that in this way each platform can consume the property in different ways 
  - the transformation can be applied not only to the value of a property, but also to its name (and also to its attributes)

- matching-build-files
  - This example shows how you can manage what tokens are generated and how they are organized. 
  - This is useful when you want to generate a 1:1 relationship between build files and token categories.

- multi-brand-multi-platform
  - This example shows how to setup a multi-brand, multi-platform suite of design tokens, with values that may depend on the brand (eg. a brand color) or the platform (eg. a font family).
  - The properties are stored in three different folders:
  - brands
    - this folder contain properties that depend on the "brand", eg. the "primary" and "secondary" colors (generally these are called "brand colors", think of the blue of Facebook, the orange of Amazon).
  - platforms
    - this folder contain properties that depend on the "platform", eg. the font family used in the application or website (eg. a font stack like "Tahoma, Arial, 'Helvetica Neue', sans" on web, "San Francisco" in iOS, "Roboto" in Android).
  - global
    - this folder contain properties that are common, that don't depend on the specific "platform" or "brand", eg. the base grayscale colors, the font sizes, etc.
  - Leveraging the ability of Style Dictionary to reference other properties values as "aliases", we can have generic properties like `font.family.base` or `color.primary` whose values actually depend on the "platform" and "brand" and whose values are computed dynamically at build time depending on the specific "platform/brand" files, included dynamically by the `getStyleDictionaryConfig` function.
  - Depending on the file included at build time, the actual value of `color.primary` will depend on the "brand"

- node-modules-as-config-and-properties
  - tokens和config都用js书写，而不是用json
  - Style Dictionary understands node modules that export a simple object for both a config file as well as the property source files. 
  - Using node module exports allows you to do some pretty cool things like generating properties programmatically (design tokens).
  - The `.extend()` method on the Style Dictionary module can take an object or a path to a JSON or node module and it copies the object attributes onto a new copy of the Style Dictionary object. 
    - The Style Dictionary object stores the transforms, transformGroups, and formats as attributes on the SD object. 
    - You can override these defaults by directly adding these attributes to your config object. 
    - This allows you to add custom transforms and formats without calling `.registerTransform()`!

- referencing_aliasing
  - This example shows how to use referencing (or "aliasing") to reference a value -or an attribute– of a property and assign it to the value –or attribute– of another property.
  - You can also reference other attributes of a property, not only its value. 

- tokens-deprecation
  - the deprecated attributes have been converted to comments (and extra properties in the plist) in the output files.

- transitive-transforms
  - Before version 3.0, Style Dictionary did not have transitive transforms though. 
  - While you could reference non-token values, you would not be able to then transform the value if it had a reference in it.

- variables-in-outputs
  - This example shows how you keep aliases/references intact in certain types of formats as well as in custom formats.
  - Common use cases include: Vending theme-able output like CSS variables

- yaml-tokens
  - This example shows how to use a custom parser to define yaml token files.
  - A custom parser has a regular expression pattern to match against source filenames. 
    - The parse function is then run taking the text content of the file and returning an object. 
    - A custom parser is like a module rule in a webpack configuration.

- custom-parser
  - 支持design tokens用任意文件格式书写
# docs

## [Overview](https://amzn.github.io/style-dictionary/#/README)

- A Style Dictionary is a system that allows you to define styles once, in a way for any platform or language to consume. 
- A single place to create and edit your styles, 
  - and a single command exports these rules to all the places you need them - iOS, Android, CSS, JS, HTML, sketch files, style documentation, etc. 
- It is available as a CLI through npm, 
  -  but can also be used like any normal npm module if you want to extend its functionality.
- It can be quite challenging to keep styles consistent and synchronized across multiple development platforms and devices. 
- StyleDictionary solves this by automatically generating style definitions across all platforms from a single source
  - removing roadblocks(路障；障碍), errors, and inefficiencies across your workflow.

- A style dictionary consists of:
  - Style properties
    - organized in JSON files
  - Static assets 
    - e.g. fonts, icons, images, sounds, etc, organized into folders
  - Configuration
    - defining the transformation of the properties and assets for each output platform

- What a style dictionary does:
  - Transforms style properties and assets into platform specific deliverables
  - Creates human readable artifacts (e.g. documentation, design libraries, etc)
- Things you can build with a style dictionary:
  - Styling files for any platform
  - Images and graphics
  - Sketch files
  - Documentation website
  - Literally anything you want styles or style data in

- The value of using Style Dictionary to build all of these is that they are all consistent and up to date.
- The Style Dictionary framework is fully extensible and modular. 
  - You can create any type of file from a style dictionary. 
  - If there is a new language, platform, or file type you need, you can easily extend the style dictionary framework to create the necessary files.

## [Configuration](https://amzn.github.io/style-dictionary/#/config)

- Style dictionaries are configuration driven. 
- Your config file defines what executes and what to output when the style dictionary builds.
- By default, Style Dictionary looks for a `config.json`/`config.js` file in the root of your package. 

- include
  - An array of path globs to Style Dictionary property files that contain default styles.
  - The properties found using the `source` attribute will overwrite properties found using `include`.
- source
  - An array of path globs to JSON files that contain style properties.
  - The Style Dictionary will do a deep merge of all of the JSON files, allowing you to separate your properties into multiple files.
- platforms
  - An object containing platform config objects that describe how the Style Dictionary should build for that platform.
- platform.transforms
  - An array of transforms to be performed on the style properties object. 
- platform.transformGroup
  - A string that maps to an array of transforms.
- platform.buildPath
  - Base path to build the files, must end with a trailing slash.
- platform.files
  - Files to be generated for this platform.
- platform.file.destination
  - Location to build the file, will be appended to the buildPath.
- platform.file.format
  - Format used to generate the file.
  - Can be a built-in one, or you can create your own via `registerFormat`.
- platform.file.filter
  - A function, string or object used to filter the properties that will be included in the file. 
  - If a string is passed, is considered a custom filter registered via `registerFilter`
- platform.file.options
  - A set of extra options associated with the file. 
- platform.file.options.showFileHeader
  - If the generated file should have a "Do not edit + Timestamp" header.
  - By default is "true".
- platform.actions
  - Actions to be performed after the files are built for that platform.
  - Actions can be any arbitrary code you want to run like copying files, generating assets, etc.
  - Pre-defined Actions
    - copy_assets
      - Action that copies everything in the assets directory to a new assets directory in the build path of the platform.
    - android/copyImages
      - Action to copy images into appropriate android directories.

## [Style properties](https://amzn.github.io/style-dictionary/#/properties)

- Synonyms: design tokens, design variables, design constants, atoms

- Style properties are stored in a collection of JSON or JS module files. 
  - We usually keep them in a `properties` directory, 
  - but you can put them wherever you like, 
  - they need to be referenced in the `source` attribute on your `config.json` file.
- A property is a collection of attributes that describe any fundamental/atomic visual style. 
  - Each attribute is a `key:value` pair. 
  - A property name and its value are considered a design token (or design variable/constant/atom).
- A property is transformed for use in different platforms, languages, and contexts.
- A property file organizes properties in a structured way for quick access. 
  - Property files are organized as a deep object with the leaf nodes being the style `key:value` pairs.
- **Any object in the JSON that has a `value` attribute on it is a property**
  - For any properties you wish to output, the `value` attribute is required. 
  - This provides the data that will be used throughout the build process (and ultimately used for styling in your deliverables). 
  - You can optionally include any custom attributes you would like (e.g. `comment` with a string or `metadata` as an object with its own attributes).
    - the `comment` will appear in output files when the output format supports comments
- Multiple properties in a single file are simple to read and understand using the recommended Category/Type/Item (CTI) method
- You can reference (alias) existing values by using the dot-notation object path (the fully articulated property name) in brackets. 
  - Note that this only applies to values; 
- This CTI structure is not required.
  - However, we feel this classification structure makes the most sense semantically.
  - Structuring style properties in this manner gives us consistent naming and accessing of these properties. 
- You can organize and name your style properties however you want, there are no restrictions.
- there are a good amount of helpers if you do use CTI structure
- CTI structure provides a good mechanism to target transforms for specific kinds of properties.
  - All of the transforms provided by the framework use the CTI structure to know if it should be applied. 
  - For instance, the `color/hex` transform only applies to properties of the category 'color'.

## [API & Extending](https://amzn.github.io/style-dictionary/#/extending)

- buildAllPlatforms
- buildPlatform
  - Takes a platform and performs all transforms to the properties object (non-mutative) then builds all the files and performs any actions. 
  - This method is also used internally in buildAllPlatforms to build each platform defined in the config.
- cleanAllPlatforms
  - This removes all the files defined in the platform and calls the undo method on any actions.
- cleanPlatform
- exportPlatform
  - Exports a properties object with applied platform transforms.
  - useful if using a style dictionary in build tools like webpack.
- extend
  - Create a Style Dictionary

- registerTransform
  - Add a custom transform to the Style Dictionary 
  - Transforms can manipulate a property's name, value, or attributes
- registerTransformGroup
  - Add a custom transformGroup to the Style Dictionary, which is a group of transforms.
- registerFilter
  - Add a custom filter to the style dictionary
  - Matcher function, return boolean if the property should be included.
- registerFormat
  - Add a custom format to the style dictionary
  - Function to perform the format. Takes 2 arguments, dictionary and config
  - Format used to generate the file. Can be a built-in one or you can create your own via registerFormat
- registerAction
  - Adds a custom action to the style property builder. 
  - Custom actions can do whatever you need, such as: copying files, base64'ing files, running other build scripts, etc. 
  - After you register a custom action, you then use that action in a platform your `config.json`
  - You can perform operations on files generated by the style dictionary as actions run after these files are generated. 
  - Actions are run sequentially, 
    - if you write synchronous code then it will block other actions, 
    - or if you use asynchronous code like Promises it will not block.
- registerTemplate (deprecated)
  - Add a custom template to the Style Dictionary
  - Templates are deprecated in favor of Formats
  - Anything you could do in a Template you can do in a Format. 

## [Architecture](https://amzn.github.io/style-dictionary/#/architecture)

- Parse the config
  - Style Dictionary is a configuration based framework, you tell it what to do in a configuration file.
  - Style Dictionary first parses this configuration to know what to do.
- Find all token files
  - In your config file you define a `source`, which is an array of file paths. 
  - This tells Style Dictionary where to find your token files. 
  - You can have them anywhere and in any folder structure as long as you tell Style Dictionary where to find them.
- Deep merge token files
  - Style Dictionary takes all the files it found and performs a deep merge. 
  - This allows you to split your token files in any way you like, without worrying about accidentally overriding groups of tokens. 
  - This gives Style Dictionary a single, complete token object to work from.
- Iterate over the platforms
  - For each platform defined in your config, Style Dictionary will do a few steps to get it ready to be consumed on that platform. 
  - You don't need to worry about one platform affecting another because everything that happens in a platform is non-destructive
- Transform the tokens
  - Style Dictionary now traverses over the whole token object and looks for design tokens. 
  - It does this by looking for anything with a `value` key. 
  - When it comes across a design token, it then performs all the transforms defined in your config in order.
- Resolve aliases/references to other values
  - After all the tokens have been transformed, it then does another pass over the token object looking for aliases, which look like `{size.font.base.value}`. 
  - When it finds these, it then replaces the reference with the transformed value. 
  - As we have a single complete token object, aliases can be in any token file and still work.
- Format the tokens into files
  - Now all the design tokens are ready to be written to a file. 
  - Style Dictionary takes the whole transformed and resolved token object and for each file defined in the platform it formats the token object and write the output to a file. 
  - Internally, Style Dictionary creates a flat array of all the design tokens it finds in addition to the token object. 
  - This is how you can output a flat SCSS variables file.

- **Build Process**
- Here is what the build system is doing under the hood.
- The build system reads in a configuration
- If there is an `includes` attribute in the config, it will take those files and deep merge them into the `properties` object
- It takes all the JSON files in the `source` attribute in the config and performs a deep merge onto the `properties` object
- Then it iterates over the platforms in the config and:
  - Performs all transforms, in order, defined in the transforms attribute or transformGroup
  - Builds all files defined in the files array
  - Performs any actions defined in the actions attribute

## [Transforms & Transform Groups](https://amzn.github.io/style-dictionary/#/transforms)

- Transforms are functions that transform a property
  - this enables each platform to consume the property in different ways. 
  - A simple example is changing pixel values to point values for iOS and dp or sp for Android. 
  - Transforms are applied in a non-destructive way thus each platform can transform the properties. 
- Transforms are performed sequentially, therefore the order you use transforms matters. 
- Transforms are used in your configuration, 
  - and can be either pre-defined transforms supplied by Style Dictionary or custom transforms.

- A transform consists of 4 parts: type, name, matcher, and transformer. 
  - Transforms are run on all properties where the matcher returns true. 
  - NOTE: if you don't provide a matcher function, it will match all properties.
- There are 3 types of transforms: attribute, name, and value.
  - Attribute
    - An attribute transform adds to the attributes object on a property. 
    - This is for including any meta-data about a property such as it's CTI or other information.
  - Name
    - A name transform transform the name of a property. 
    - You should really only be apply one name transformer because they will override each other if you use more than one.
  - Value
    - The value transform is the most important as this is the one that changes the representation of the value. 
    - Colors can be turned into hex values, rgb, hsl, hsv, etc. 
    - Value transforms have a matcher function that filter which properties that transform runs on. 
    - This allows us to only run a color transform on only the colors and not every property.
- Pre-defined Transforms
  - attribute/cti
  - name/cti/camel
  - name/cti/constant
  - color/hex
  - size/px
    - Adds 'px' to the end of the number. Does not scale the number
  - time/seconds
- Transform Groups are a way to easily use multiple transforms at once. 
  - They are an array of transforms. 
- Pre-defined Transform groups
  - attribute/cti name/cti/kebab size/px color/css
  - attribute/cti name/cti/pascal size/rem color/hex

- the registration of custom transforms needs to be done before applying the configuration 
  - (the methods needs to be already declared and registered in Style Dictionary to be used when extending it with the configuration).
- the name of a custom "transform" can be the same as an existing pre-defined method; 
  - in that case, the pre-defined method is overwritten
- beyond the existing attributes, you can use custom attributes to create matcher functions, 
  - used to filter the properties and apply the transform only to those that match the filter condition.
- if you don't specify a matcher, the transformation will be applied to all the properties
- the transformation can be applied not only to the value of a property, but also to its name (and also to its attributes)

## [Formats & Filter](https://amzn.github.io/style-dictionary/#/formats)

- Formats define the output of your created files. 
  - For example, to use your styles in CSS you use the `css/variables` format. 
  - This will create a CSS file containing the variables from your style dictionary.
- Formats can take configuration to make them more flexible. 
- A special file configuration is `filter`, which will filter the tokens before they get to the format.
- Pre-defined Formats
  - css/variables
    - Creates a CSS file with variable definitions 
  - scss/variables
    - Creates a SCSS file with variable 
  - scss/map-flat
    - Creates a SCSS file with a flat map 
  - less/variables
  - javascript/module
    - Creates a CommonJS module with the whole style dictionary
  - json
  - json/flat
  - sketch/palette

## [Actions](https://amzn.github.io/style-dictionary/#/actions)

- Custom actions can do whatever you need, such as: copying files, base64'ing files, running other build scripts, etc. 
  - After you register a custom action, you then use that action in a platform your config.json
- You can perform operations on files generated by the style dictionary as actions run after these files are generated. 
  - Actions are run sequentially, if you write synchronous code then it will block other actions, or if you use asynchronous code like Promises it will not block.

- Actions provide a way to run custom build code such as generating binary assets like images.
- You use actions in your config file under `platforms > [platform] > actions`

## [Get ready for v3](https://amzn.github.io/style-dictionary/#/version_3)

- Transitive transforms is the big one that required a big re-architecture of how the Style Dictionary build process works.
  - The new build process is similar, except that it recursively transforms and resolves aliases, only deferring a transform to the next cycle if the token has an unresolved alias. 
  - **Use cases this change opens up**:
    - Having variable references in outputs
    - Combining values like using HSL for colors
    - Modifying aliases like making a color lighter or darker
- Custom parser support
  - The addition of custom parser support allows you to define your tokens in any language you like
- Adding filePath and isSource entries on tokens 
  - to help with debugging
- Typescript typings
- Formats
  - Adding `javascript/module-flat` format that's just like the `json/flat` format, but exported as a cjs module
  - Removing filters inside Android formats: WIP
- todo
  - Use ES6 where possible, Better log levels
# ref
- [[RFC] Plugin Architecture](https://github.com/amzn/style-dictionary/issues/311)
  - We don't want to try to build in so many transforms, formats, and actions into the core library that it becomes hard to maintain and bloated.
  - Technically, this ability exists today, but we don't document or promote this ability yet.

- [How to manage your Design Tokens with Style Dictionary](https://didoo.medium.com/how-to-manage-your-design-tokens-with-style-dictionary-98c795b938aa)
- https://github.com/didoo/style-dictionary-demo
- This, for example, is how we use some design tokens as Sass variables in the declaration of the styles for the `<Button/>` component
- These properties are also exposed in our style guide so that they can be part of our documentation
- Theo, a tool developed by the design system team at Salesforce 
  - Theo has evolved a lot (now we are at Theo8!) and the way you declare the token values has quite changed, 
  - but what remains a pain point (at least, for me) is the fact that in order to reference a value of a token in another token, you have to declare it before using a specific alias definition; 
  - and, if this declaration is in another file, you have to import the file where it’s used (which also means that, when declaring the files to import/process, the order of the declarations matters).
  - This way to define “aliases” leads to a lot of repetitions 
  - Besides, in this way, the resulting organisation of the design tokens, and the files where they are stored, tends to be very prescriptive (see for example here or here) and rigid when you need to refactor or re-arrange the design tokens.
  - Don’t get me wrong: Theo is a great tool, and the issues I have mentioned above are small details, just a matter of personal preferences. 
- First impact with Style Dictionary
  - This “deep merge” of different JSON files (plus, the different compilations for different platforms) was exactly what I had in mind.
- The ”Category > Type > Item” classification
  - This classification is simply based on the nesting of the properties inside the JSON files.
  - the order in the nesting of the source JSON is automatically interpreted as logical tree/structure, and it’s used to build the name of the properties 
  - While working with Style Dictionary, you will find this implicit CTI classification consistently across many helpers and functions
  - you can organize and name your style properties however you want, there are no restrictions
- My Cosmos design tokens organisation
  - built to support different “platforms” (Mobile Web, iOS and Android) and different “brands
  - Instead of following the suggested CTI — Category > Type > Item — organisation (e.g. color > background > button) 
  - I’ve preferred to follow a classification which is more “component-oriented”.
- Conclusions/Final thoughts
  - In the last days, weeks, I have used extensively Style Dictionary, and every time I find myself thinking “Wow. It just works!”. 
  - Everything in this project works as one would expect to, everything is so well-thought and clear
