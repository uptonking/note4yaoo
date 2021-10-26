---
title: lib-office-remark-docs
tags: [docs, remark]
created: '2021-06-02T16:58:29.491Z'
modified: '2021-06-02T16:58:43.564Z'
---

# lib-office-remark-docs

# overview

- remark /4.1kStar/MIT/202105/js
  - https://github.com/remarkjs/remark
  - https://remark.js.org/
  - a Markdown processor built on micromark powered by plugins
  - It aims to do for Markdown what Esprima did for JavaScript and PostCSS for CSS: bring Markdown into the tooling age.

- micromark /835Star/MIT/202106/js
  - https://github.com/micromark/micromark
  - The smallest CommonMark compliant markdown parser
  - It uses a state machine to parse the entirety of markdown into concrete tokens.
  - It was made to replace the internals of remark-parse

- unified is an interface for processing text with syntax trees and transforming between them. 
- Three syntaxes are connected to unified, each coming with a syntax tree definition, and a parser and stringifier: 
  - mdast with remark for markdown, 
  - nlcst with retext for prose, 
  - hast with rehype for HTML.
- unified also bridges between syntaxes, such as between markdown and HTML
# remark-parse
- Parses Markdown to mdast syntax trees. 
- Built on micromark and mdast-util-from-markdown

- processor().use(parse)
  - Configure the processor to read Markdown as input and process mdast syntax trees.

- parser-extension
  - see remark-gfm

```JS 源码

var fromMarkdown = require('mdast-util-from-markdown'); 
function parse(options) {
  var self = this; 
  this. Parser = parse; 

  function parse(doc) {

    return fromMarkdown(
      doc,
      Object.assign({}, self.data('settings'), options, {
        extensions: self.data('micromarkExtensions') || [],
        mdastExtensions: self.data('fromMarkdownExtensions') || []
      })
    )

  }
}

module.exports = parse; 

// test
t.equal(
  unified().use(parse).parse('Alfred').children.length, 
  1, 
  'should accept a `string` '
)

```

# intro to unified
- unified is a friendly interface backed by an ecosystem of plugins built for creating and manipulating content.
  - It does this by taking Markdown, HTML, or plain text prose, turning it into structured data, and making it available to over 100 plugins. 
  - Plugins for example do tasks such as spellchecking, linting, or minifying.

- The ecosystems:
  - remark — Markdown
  - rehype — HTML
  - retext — Natural language
  - redot — Graphviz

- The specifications for syntax trees:
  - unist — Universal Syntax Tree
  - mdast — Markdown Abstract Syntax Tree format
  - hast — HTML Abstract Syntax Tree format
  - xast — XML Abstract Syntax Tree format
  - esast — ECMAScript Abstract Syntax Tree format
  - nlcst — Natural Language Concrete Syntax Tree format

- These processors, specifications, and tools come together in a three part act. 
- Parse
  - Whether your input is Markdown, HTML, or prose — it needs to be parsed to a workable format. 
  - Such a format is called a syntax tree. 
  - The specifications (for example mdast) define how such a syntax tree looks. 
  - The processors (such as remark for mdast) are responsible for creating them.
- Transform
  - Users compose plugins and the order they run in. 
  - Plugins plug into this phase and transform and inspect the format they get.
- Stringify
  - The final step is to take the (adjusted) format and stringify it to Markdown, HTML, or prose (which could be different from the input format!)

- `trough` is like `ware` with less sugar, and middleware functions can change the input of the next.
- `remark-rehype` doesn’t deal with HTML inside the Markdown. 
  - You’ll need `rehype-raw` if you’re planning on doing that.
# [Creating a plugin with unified](https://unifiedjs.com/learn/guide/create-a-plugin/)
- Plugins can contain two parts: 
  - an attacher, which is a function that is invoked when someone calls `.use`, 
  - a transformer, which is an optional function invoked each time a file is processed with a syntax tree and a virtual file.

# api
- processor()
  - Processor describing how to process text.

- processor.use(plugin[, options])
  - Configure the processor to use a plugin and optionally configure that plugin with options.
  - If the processor is already using this plugin, the previous plugin configuration is changed based on the options that are passed in. The plugin is **not added a second time**.

- **processor.parse(file)**
  - Parse text to a syntax tree.
  - file (VFile) — File, any value accepted by vfile()

- processor. Parser
  - A parser handles the parsing of text to a syntax tree. 
  - Used in the parse phase and called with a string and VFile representation of the text to parse.
  - Parser can be a function, in which case it must return a Node: the syntax tree representation of the given file.

- **processor.stringify(node[, file])**
  - Compile a syntax tree.

- processor. Compiler
  - A compiler handles the compiling of a syntax tree to text. 
  - Used in the stringify phase and called with a Node and VFile representation of syntax tree to compile.
  - Compiler can be a function, in which case it should return a string: the textual representation of the syntax tree.

- processor.run(node[, file][, done])
  - Run transformers on a syntax tree.
  - run performs the run phase, not other phases.
- processor.runSync(node[, file])

- processor.process(file[, done])
  - Process the given file as configured on the processor.
  - process performs the parse, run, and stringify phases.
  - unified typically compiles by serializing: most compilers return string (or Buffer). 
  - Some compilers, such as the one configured with rehype-react, return other values (in this case, a React tree). 
  - If you’re using a compiler that serializes, the result is available at file.contents. 
  - Otherwise, the result is available at file.result.
- processor.processSync(file|value)

- processor.data([key[, value]])
  - Configure the processor with information available to all plugins. 
  - Information is stored in an in-memory key-value store.

- processor.freeze()
  - Freeze a processor. 
  - Frozen processors are meant to be extended and not to be configured directly.
  - Once a processor is frozen it cannot be unfrozen. New processors working the same way can be created by calling the processor.

- Plugin
  - Plugins configure the processors they are applied on in the following ways:
    - They change the processor: such as the parser, the compiler, or configuring data
    - They specify how to handle syntax trees and files
  - **Plugins are a concept. They materialize as attachers**.
- Presets are sharable configuration. 
  - They can contain plugins and settings.

- function attacher([options])
  - Attachers are materialized plugins. 
  - An attacher is a function that can receive options and configures the processor.
  - Attachers change the processor, such as the parser, the compiler, configuring data, or by specifying how the syntax tree or file are handled.
  - Attachers are called when the processor is frozen, not when they are applied.

- function transformer(node, file[, next])
  - Transformers handle syntax trees and files. 
  - A transformer is a function that is called each time a syntax tree and file are passed through the run phase. 
  - If an error occurs (either because it’s thrown, returned, rejected, or passed to next), the process stops.
  - The run phase is handled by `trough`.

- function next(err[, tree[, file]])
  - If the signature of a transformer includes next (the third argument), the transformer may perform asynchronous operations, and must call next().

# unist syntax tree
- unified is an interface for processing text using syntax trees. 
  - Syntax trees are a representation of text understandable to programs. 
  - Those programs, called plugins, take these trees and inspect and modify them. 
  - To get to the syntax tree from text, there is a parser. 
  - To get from that back to text, there is a compiler. 
  - This is the process of a processor.

- Every processor implements another processor. 
  - To create a processor, call another processor. 

- The syntax trees used in unified are `unist` nodes. 
  - A node is a plain JavaScript objects with a `type` field. 
  - The semantics of nodes and format of syntax trees is defined by other projects.

- vfile
  - When processing a document, metadata is often gathered about that document. 
  - vfile is a virtual file format that stores data, metadata, and messages about files for unified and its plugins.

- Processors can be combined in two modes.
- Bridge mode transforms the syntax tree from one format (origin) to another (destination). 
  - Another processor runs on the destination tree. 
  - Finally, the original processor continues transforming the origin tree.
- Mutate mode also transforms the syntax tree from one format to another. 
  - But the original processor continues transforming the destination tree.

- unist is a specification for syntax trees. 
  - It’s implemented by several other specifications.
- Syntax trees are representations of source code or even natural language. 
  - These trees are abstractions that make it possible to analyze, transform, and generate code.

- Syntax trees come in two flavors:
- concrete syntax trees: 
  - structures that represent every detail (such as white-space in white-space insensitive languages)
- abstract syntax trees: 
  - structures that only represent details relating to the syntactic structure of code (such as ignoring whether a double or single quote was used in languages that support both, such as JavaScript).

- Syntactic units in unist syntax trees are called nodes, and implement the Node interface.

``` typescript

interface Node {
  type: string
  data?: Data
  position?: Position
}

interface Data { }

interface Position {
  start: Point
  end: Point
  indent?: [number >= 1]
}

interface Point {
  line: number >= 1
  column: number >= 1
  offset?: number >= 0
}

interface Parent <: Node {
  children: [Node]
}

// Nodes containing a value extend the abstract interface Literal (Node).
interface Literal <: Node {
  value: any // The value field can contain any value.
}
```

- The `type` field is a non-empty string representing the variant of a node. 
  - This field can be used to determine the type a node implements.
- The `data` field represents information from the ecosystem. 
  - The value of the data field implements the Data interface.
- The `position` field represents the location of a node in a source document. 
  - The value of the position field implements the Position interface. 
  - The position field must not be present if a node is generated.

- `Data` represents information associated by the ecosystem with the node.
  - This space is guaranteed to never be specified by unist or specifications implementing unist.

- Specifications implementing unist are encouraged to define more fields. 
  - Ecosystems can define fields on `Data`.

- The value of the `start` and `end` fields implement the Point interface.
- The `indent` field of Position represents the start column at each index (plus start line) in the source region, for elements that span multiple lines.

- The `line` field (1-indexed integer) represents a line in a source file. 
- The `column` field (1-indexed integer) represents a column in a source file. 
- The `offset` field (0-indexed integer) represents a character in a source file.

- Any value in unist must be expressible in JSON values: string, number, object, array, true, false, or null. 
  - This means that the syntax tree should be able to be converted to and from JSON and produce the same tree.

- A file is a source document that represents the original file that was parsed to produce the syntax tree. 
  - Positional information represents the place of a node in this file. 
  - Files are provided by the host environment and not defined by unist.
