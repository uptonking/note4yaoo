---
title: lib-tool-style-dictionary-dev
tags: [devtools, engineering, lib, style-dictionary]
created: '2021-01-02T18:05:21.074Z'
modified: '2021-01-02T18:08:07.806Z'
---

# lib-tool-style-dictionary-dev

# guide

- s-d pros
  - 方便将design tokens输出到各个平台
  - 支持输出scss，也支持输出css vars，所以可以针对ie浏览器build适合的格式

- s-d cons
  - 不直接支持pseudo class的类，需要自己实现，分析有无此需求
  - ~~暂不支持输出文件的值中包含`var(--name)`形式的css变量~~

- extensions
  - 可自定义输出的format，自动生成简单的单页文档，类似theo输出html

- tips
  - 先基于theme specification定义输出design tokens的类别和名称
    - 具体可参考theme-ui预置主题对应的[raw json](https://theme-ui.com/demo/)
  - 可以将每个组件的design tokens输出到单独的文件，利用自定义filter
  - 可以输出扁平化无嵌套的样式变量，
    - 也可以输出时设置最外层的选择器名，如`:root{}` 或 `.dark-theme{}`
  - 输出的值也可以使用 css vars

- roadmap
  - [Changelog](https://github.com/amzn/style-dictionary/blob/3.0/CHANGELOG.md)

# faq

- style-dictionary vs theo
  - Theo uses json, json5 or yaml and takes a file-in file-out strategy.
  - Style Dictionary uses json or JS modules and merges all token files into 1 big object.
  - ref
    - 工具要考虑实现或集成：theming, css in js
    - You can also create a custom tool (Adobe did this). 
    - 甚至考虑用通用工具如google spreadsheet来存放tokens

- 是否该用工具生成design tokens外，还生成所有组件的样式？
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

- referencing/alias transform vs transitive transform
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

- output css vars
  - [feat(format): adding ability to have variables in output_202012](https://github.com/amzn/style-dictionary/pull/504)
    - Adding a `useVariables` configuration on SCSS, CSS, and Less variables formats to make use of this
  - [Feature/css var deep_202008](https://github.com/amzn/style-dictionary/pull/428)
    - This one also currently supports CSS variables flat, split out dark tokens

- 是否要在输出样式的顶层，再加上一层`:root{}`或 `.dark-theme{}`
  - tokens一般要在具体组件的scss中使用
  - [I can't generate css variables to a specific class_202007](https://github.com/amzn/style-dictionary/issues/448)
    - You could write a custom format that does this too if you can't wait for that change to be made into the core library

- 不输出一个大文件，而输出各小文件
  - [feat(examples): add matching build files example](https://github.com/amzn/style-dictionary/pull/481)
    - example of automatically generating 1:1 token files based on a custom filter.

- 如何生成tokens的简单说明文档，类似theo输出html format
  - [Style guide? ](https://github.com/amzn/style-dictionary/issues/477)

- [Specifications for property values](https://github.com/amzn/style-dictionary/issues/461)

# pieces

- ## component tokens
- [json to scss](https://github.com/amzn/style-dictionary/issues/492)
  - The way I would do this is create a custom format and template.
  - I have done something similar in some projects, but instead used a custom action to build the files.
    - The action grabs parts of the dictionary under the component namespace and passes the entire component object to a formatter to generate the SCSS file. 
    - This way you can add more components without needing to add more files to the configuration.

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
