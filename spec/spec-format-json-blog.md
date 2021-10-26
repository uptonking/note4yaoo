---
title: spec-format-json-blog
tags: [blog, json, format]
created: '2021-02-27T15:08:43.563Z'
modified: '2021-02-27T15:09:07.825Z'
---

# spec-format-json-blog

# json config

## [Why JSON isn’t a Good Configuration Language_201807](https://www.lucidchart.com/techblog/2018/07/16/why-json-isnt-a-good-configuration-language/)

- Don’t get me wrong — I like JSON. 
  - It is a flexible format that is relatively easy for both machines and humans to read, and it’s a pretty good data interchange and storage format. 
  - But as a configuration language, it falls short.
- Many projects use JSON for configuration files. Perhaps the most obvious example is the package.json file used by npm and yarn, 
  - but there are many others, including CloudFormation (originally JSON only, but now supports YAML as well) and composer (PHP).

- ### Why is JSON popular as a config language?
  - The biggest reason is probably that it is easy to implement. 
    - Many languages have JSON support in the standard library, and those that don’t almost certainly have an easy-to-use JSON package readily available.
  - Then there is the fact that developers and users are probably already familiar with JSON and don’t need to learn a new configuration format
  - And that’s not to mention all the existing tooling for JSON, including syntax highlighting, auto-formatting, validation tools, etc.

- ### Lack of comments
  - Comments are necessary to annotate what different options are for and why a particular value was chosen and—perhaps most importantly—to temporarily comment out parts of the config while using a different configuration for testing and debugging. 
    - If you think of JSON as a data interchange format, then it doesn’t really make sense to have comments.
  - Some JSON libraries do allow comments as input. 
    - For example, Ruby’s JSON module and the Java Jackson library with the JsonParser.Feature.ALLOW_COMMENTS feature enabled will handle JavaScript-style comments just fine in JSON input. 
    - However, this is non-standard, and many editors don’t properly handle comments in JSON files, which makes editing them a little harder.

- ### Overly strict
  - The JSON specification is pretty restrictive. 
  - Its restrictiveness is part of what makes it easy to implement a JSON parser, 
  - but in my opinion, it also hurts the readability and, to a lesser extent, writability by humans.

- ### Low Signal to Noise
  - Compared to many other configuration languages, JSON is pretty noisy.
    - There is a lot of punctuation(标点符号) that doesn’t aid human readability, although it does make it easier to write implementations for machines. 
    - In particular, for configuration files, the keys in objects are almost always identifiers, so the quotation marks around the keys are redundant.
  - JSON requires curly braces around the entire document, which is part of what makes it an (almost) subset of JavaScript and helps delimit(界定，限定) different objects when multiple objects are sent over a stream. 
    - But, for a configuration file, the outermost braces are just useless clutter. 
    - The commas between key-value pairs are also mostly unnecessary in config files. 
    - Generally, you will have a single key-value pair per line, so it would make sense to accept a newline as a delimiter.
    - JSON doesn’t accept trailing commas.

- ### Long Strings
  - it doesn’t have any support for multi-line strings
  - If you want newlines in the string, you have to escape them with “\n”, and what’s worse, if you want a string that carries over onto another line of the file, you are just out of luck. 
  - if your configuration includes long strings, such as the description of a project or a GPG key, you probably don’t want to put it on a single line with “\n” escapes instead of actual newlines.

- ### Numbers
  - As defined in the JSON spec, numbers are arbitrary precision finite floating point numbers in decimal notation.
  - But if you need to use hexadecimal notation or represent values like infinity or NaN, then TOML or YAML would be able to handle the input better.

- ### What you should use instead
- Each language has different pros and cons, but here are some choices to consider. 
- TOML 适合简单配置，不适合嵌套过深的配置
  - TOML is an increasingly popular configuration language. 
  - It is used by Cargo (Rust build tool), pip (Python package manager), and dep (golang dependency manager). 
  - TOML is somewhat similar to the INI format, but unlike INI, it has a standard specification and well-defined syntax for nested structures. 
  - It is substantially simpler than YAML, which is attractive if your configuration is fairly simple. 
  - But if your configuration has a significant amount of nested structure, TOML can be a little verbose, and another format, such as YAML or HOCON, may be a better choice.
- HJSON 类似json5扩展了json
  - HJSON is a format based on JSON but with greater flexibility to make it more readable. 
  - It adds support for comments, multi-line strings, unquoted keys and strings, and optional commas. 
  - If you want the simple structure of JSON but something more friendly for configuration files, HJSON is probably the way to go. 
  - There is also a command line tool that can convert HJSON to JSON, so if you are using a tool that requires plain JSON, you can write your configuration in HJSON and convert it to JSON as a build step. 
  - JSON5 is another option that is pretty similar to HJSON.
- HOCON
  - HOCON is a configuration designed for the Play framework but is fairly popular among Scala projects. 
  - It is a superset of JSON, so existing JSON files can be used
  - Besides the standard features of comments, optional commas, and multi-line strings, HOCON supports importing from other files, referencing other keys of other values to avoid duplicate code, and using dot-delimited keys to specify paths to a value, so users do not have to put all values directly in a curly-brace object.
- YAML
  - a very flexible format
  - Libraries for YAML are almost as ubiquitous as JSON.
  - In addition to support of comments, newline delimiting, multi-line strings, bare strings, and a more flexible type system, YAML also allows you to reference earlier structures in the file to avoid code duplication.
  - The main downside to YAML is that the specification is pretty complicated, which results in inconsistencies between different implementations.
  - It also treats indentation levels as syntactically significant (similar to Python), which some people like and others don’t.
    - It can also make copy and pasting tricky. 
- Scripting language
  - If your application is written in a scripting language such as Python or Ruby, and you know the configuration comes from a trusted source, the best option may be to simply use a file written in that language for your configuration. 
  - Doing so gives you the full flexibility of the scripting language and can be simpler to implement than using a different configuration language
  - The downside to using a scripting language is it may be too powerful, and of course, if the source of the configuration is untrusted, it introduces serious security problems.

## [Stop Using JSON Config Files_202006](https://medium.com/trabe/stop-using-json-config-files-ab9bc55d82fa)

- Every major tool in the JavaScript world allows custom configuration using either JSON or JavaScript files (Babel or ESLint are good examples). 
  - Whatever the reason you may have to choose JSON, please don’t. 
  - Use JavaScript instead.
- Learning from my own mistakes
  - Once upon a time I was setting up a complex monorepo.
  - It contained several packages that shared common transpilation, linting and testing configuration.
  - Unfortunately, not every tool implements this `extends` mechanism.
- Why you should also prefer JavaScript configuration
  - Easy overrides
  - Dynamic configuration
  - Shareable configuration via npm
  - Comments
  - Testable configuration

## [The state of config file formats: XML vs. YAML vs. JSON vs. HCL_202011](https://octopus.com/blog/state-of-config-file-formats)

- When should you use XML?
  - XML is a generalized language that easily allows different formats to be realized from a common syntax.
  - Schemas exist for validation and creation of custom types, while namespaces avoid collisions between elements.
  - XPath and XQuery facilitate complex queries into XML documents.
- When should you not use XML?
  - The XML language is verbose and often contains redundant syntax.
  - With the higher verbosity comes increased storage capacity and bandwidth needs.
  - Not considered easily human-readable due to the descriptive nature of elements.

- When should you use JSON?
- In contrast to XML, far more human-readable due to a more compact syntax.
  - Simpler syntax with limited markup.
  - Quick for systems and languages to parse.
  - JSONPath, similar to XPath, is available for complex queries.
- When should you not use JSON?
  - Limited data type support containing only strings, numbers, JSON object, array, boolean, and null.
  - No namespace, comment, or attribute support.
  - Simple structures may not support complex configurations.

- When should you use YAML?
  - Exceptionally human-readable syntax.
  - Compact syntax, which uses Python-style indentation to denote structure.
  - Supports language-independent object types. Scalers such as int, binary, str, and bool or collections such as map, set, pairs, and seq.
- When should you not use YAML?
  - Indentation format is prone to syntax and validation errors.
  - Portability with certain types may not exist due to a lack of features across all languages.
  - Due to the declarative nature of YAML, debugging is difficult. - Breakpoints and similar functionality does not exist.

- HCL is a tool-specific language intended for use with the Terraform toolset. 
  - HCL looks visually similar to JSON, with unique data structures added.
- When should you use HCL?
  - Using Terraform is far easier when using HCL.
  - Visually and functionality similar to JSON in addition to being compatible.
  - With features such as attributes and templates, HCL is more full-featured than competing languages, such as JSON.
- When should you not use HCL?
  - As evidenced by Hashicorp being in the name, HCL was developed primarily for its products, and development is geared towards those ends.
  - Despite stated compatibility with JSON, a strict conversion between the two languages is not straightforward due to ambiguity in mapping certain language constructs.
  - As a relatively new language, many features are still being developed and toolkit maturity is still growing.
