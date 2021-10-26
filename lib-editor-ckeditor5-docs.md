---
title: lib-editor-ckeditor5-docs
tags: [ckeditor, editor]
created: '2021-10-25T09:32:44.058Z'
modified: '2021-10-25T09:33:13.353Z'
---

# lib-editor-ckeditor5-docs

# guide

- ckeditor架构亮点
  - view层包括editing view和data view

- ckeditor架构不足
  - 多套vdom，model和view的vdom有相似有差异

- 注意区分 @ckeditor/ckeditor5-editor-classic  @ckeditor/ckeditor5-build-classic
# ckeditor framework
- The framework was designed to be a highly flexible and universal platform for creating custom rich-text editing solutions.
- Plugin-based architecture. 
  - Everything is a plugin — even such crucial features as support for typing or `<p>` elements. 
  - You can remove plugins or replace them with your own implementations to achieve fully customized results.
- Schema-less core. 
  - The core makes minimal assumptions and can be controlled through the schema. 
  - This leaves all decisions to plugins and hence to you.
- Collaboration-ready.
  - The editor implements Operational Transformation for the tree-structured model as well as many other mechanisms. 
  - Additionally, we provide cloud infrastructure and plugins enabling real-time collaborative editing in your application!
- Custom data model. 
  - The editing engine implements a tree-structured custom data model, designed to fit multiple requirements such as enabling real-time collaboration and complex editing features (like tables or nested blocks).
- Virtual DOM. 
  - The editing engine features a custom, editing-oriented virtual DOM implementation that aims to hide browser quirks from your sight. 
- Extensibility. 
  - The entire editor architecture was designed for maximum flexibility. 
  - The code is event-based and highly decoupled, allowing you to plug in or replace selected pieces. 
  - Features do not directly depend on one another and communicate in standardized ways.
# core editor architecture
- The `Editor` class represents the base of the editor. 
  - It is the entry point of the application, gluing all other components.

- Plugins are a way to introduce editor features. 
  - Every feature is implemented or at least enabled by a plugin.
  - Plugins are highly granular. 可组合的
  - Plugins should know as little about other plugins as possible.
  - Plugins know everything about the editor.
  - These are the rules based on which the official plugins were implemented. When implementing your own plugins, if you do not plan to publish them, you can reduce this list to the first point.

- Another important aspect of how existing CKEditor 5 plugins are implemented is the split into engine and UI parts.

- A command is a combination of an action (a callback) and a state (a set of properties).
  - Basically, the default action of 'execute' (which is calling the execute() method) is registered as a listener to that event with a default priority. 

- CKEditor 5 has an event-based architecture so you can find `EmitterMixin` and `ObservableMixin` mixed all over the place. 
  - Both mechanisms allow for decoupling the code and make it extensible.
  - Most of the classes that have already been mentioned are either emitters or observables (observable is an emitter, too). 
  - An emitter can emit (fire) events as well as listen to them.
- Besides decorating methods with events, observables allow to observe their chosen properties.
  - Observables have one more feature which is widely used by the editor (especially in the UI library) — the ability to bind the value of one object’s property to the value of some other property or properties (of one or more objects). 
  - This, of course, can also be processed by callbacks.
# editing engine
- The editing engine implements an MVC architecture.
- There is one model document which is converted into separate views — the editing view and the data view.
  - These two views represent, respectively, the content that the user is editing (the DOM structure that you see in the browser) and the editor input and output data (in a format that the plugged data processor understands). 
  - Both views feature virtual DOM structures (custom, DOM-like structures) on which converters and features work and which are then rendered to the DOM.
- features control what changes are made to the model, how they are converted to the view and how the model needs to be changed based on fired events (the view’s and model’s ones).

## model

- The role of the model layer is to create an abstraction over the data. 
  - Its format was designed to allow storing and modifying the data in the most convenient way, while enabling implementation of complex features. 
  - Most features operate on the model (read from it and change it).

- The model is implemented by a DOM-like tree structure of elements and text nodes. 
  - Unlike in the actual DOM, in the model, both elements and text nodes can have attributes.
  - Like in the DOM, the model structure is contained within a document that contains root elements (the model, as well as the view, may have multiple roots). 
  - The document also holds its selection and the history of its changes.
- Finally, the document, its schema and document markers are properties of the Model. 
  - An instance of the Model class is available in the `editor.model` property. 
  - The model, besides holding the properties described above, provides the API for changing the document and its markers, too.

- **All changes in the document structure, of the document’s selection and even the creation of elements, can only be done by using the model writer**. 
  - Its instance is available in `change()` and `enqueueChange()` blocks.
- All changes done within a single `change()` block are combined into one undo step (they are added to a single batch). 
  - When nesting `change()` blocks, all changes are added to the outermost `change()` block’s batch.
- All changes made to the document structure are done by applying operations(from OT).
  - Since OT requires a system to be able to transform every operation by every other one (to figure out the result of concurrently applied operations), the set of operations needs to be small. 
  - CKEditor 5 features a non-linear model (normally, OT implementations use flat, array-like models while CKEditor 5 uses a tree structure), hence the set of potential semantic changes is more complex. 
  - Operations are grouped in batches. A batch may be understood as a single undo step.

- Text styles such as “bold” and “italic” are kept in the model not as elements but as text attributes (think — like element attributes). 
  - Such representation of inline text styling allows to significantly reduce the complexity of algorithms operating on the model. 
  - 将文字格式类样式放在attribute而不是element，可以减少确定selection位置的复杂度

- selection also has attributes

- if the selection is at the boundary of two text nodes, is it anchored in the left one, the right one, or in the containing element?
  - This is, indeed, another problem with DOM APIs. Not only can positions outside and inside some element be identical visually but also they can be anchored inside or outside a text node (if the position is at a text node boundary). This all creates extreme complications when implementing editing algorithms.
  - To avoid such troubles, and to make collaborative editing possible for real, CKEditor 5 uses the concepts of indexes and offsets. 
  - **Indexes relate to nodes (elements and text nodes) while offsets relate to positions**. 

- The engine also defines three levels of classes that operate on offsets:
  - A `Position` instance contains an array of offsets (which is called a “path”)
  - A `Range` contains two positions: start and end ones.
  - there is a `Selection` which contains one or more ranges, attributes, and has a direction (ltr/rtl). 
    - You can make as many instances of it as you need and you can freely modify it whenever you want. 
    - Additionally, there is a single `DocumentSelection`. It represents the document’s selection and can only be changed through the model writer. It is automatically updated when the document’s structure is changed.

- Markers are a special type of ranges.
- They can only be created and changed through the model writer.
- They can be synchronized over the network with other collaborating clients.
- They are automatically updated when the document’s structure is changed.
- **Markers are perfect for storing and maintaining additional data related to portions of the document such as comments or selections of other users**.

- The model’s schema defines several aspects of how the model should look
  - Where a node is allowed or disallowed
  - What attributes are allowed for a certain node
  - Additional semantics of model nodes
- This information is then used by the features and the engine to make decisions on how to process the model.
- The schema is, by default, configured by editor plugins. 
  - **It is recommended that every editor feature comes with rules that enable and preconfigure it in the editor**. 
  - This will make sure that the plugin user can enable it without worrying to re-configure their schema.
- Currently, there is no straightforward way to override the schema preconfigured by features. 
  - If you want to override the default settings when initializing the editor, the best solution is to replace `editor.model.schema` with a new instance of it. 
  - This, however, requires rebuilding the editor.

## view

- The view is an abstract representation of the DOM structure 
  - which should be presented to the user (for editing) 
  - and which should (in most cases) represent the editor’s input and output (i.e. the data returned by `editor.getData()`, the data set by `editor.setData()`, pasted content, etc.).
- The view is yet another custom structure.
  - It resembles the DOM. While the model’s tree structure only slightly resembled the DOM (e.g. by introducing text attributes), the view is much closer to the DOM. In other words, it is a virtual DOM.
- There are two “pipelines”: the editing pipeline (also called the “editing view”) and the data pipeline (the “data view”).
  - Treat them as two separate views of one model. 
  - The editing pipeline renders and handles the DOM that the user sees and can edit. 
  - The data pipeline is used when you call `editor.getData()`,  `editor.setData()` or paste content into the editor.
- The views are rendered to the DOM by the `Renderer` which handles all the quirks required to tame(驯化；驯服；使易于控制) the `contentEditable` used in the editing pipeline.

- Technically, the data pipeline does not have a document and a view controller. 
  - It operates on detached view structures, created for the purposes of processing data.
  - It is much simpler than the editing pipeline
- The structure of the view resembles the structure in the DOM very closely. 
- The view structure comes “DTD-free”, 
  - so in order to provide additional information and to better express the semantics of the content, the view structure implements 6 element types (ContainerElement, AttributeElement, EmptyElement, RawElement, UIElement, and EditableElement) and so called “custom properties” (i.e. custom element properties which are not rendered)

- Container element
  - The elements that build the structure of the content. Used for block elements such as `<p>, <h1>, <blockQuote>, <li>`, etc.
- Attribute element
  - The elements that cannot hold container elements inside them. 
  - Most model text attributes are converted to view attribute elements. 
  - They are used mostly for inline styling elements such as `<strong>, <i>, <a>, <code>`. 
  - Similar attribute elements are flattened by the view writer.
- Empty element
  - The elements that must not have any child nodes, for example `<img>`.
- UI element
  - The elements that are not a part of the “data” but need to be “inlined” in the content. 
  - They are ignored by the selection (it jumps over them) and the view writer in general. 
  - The contents of these elements and events coming from them are filtered out, too.
- Raw element
  - The elements that work as data containers (“wrappers”, “sandboxes”) but their children are transparent to the editor. 
  - Useful when non-standard data must be rendered but the editor should not be concerned what it is and how it works. 
  - Users cannot put the selection inside a raw element, split it into smaller chunks or directly modify its content.
- Editable element
  - The elements used as “nested editables” of non-editable fragments of the content
  - 比如图片不可编辑、图片描述可编辑

- Not all view trees need to (and can) be build with semantic element types. 
  - View structures generated straight from input data (e.g. pasted HTML or with editor.setData()) consists only of base element instances. 
  - Those view structures are (usually) converted to model structures and then converted back to view structures for editing or data retrieval purposes, at which point they become semantic views again.
  - The additional information conveyed in the semantic views and special types of operations that feature developers want to perform on those tree (compared to simple tree operations on non-semantic views) means that both structures need to be modified by different tools.
- there are semantic views for rendering and data retrieval purposes and non-semantic views for data input.

- **Do not change the view manually, unless you really know what you are doing**. 
  - If the view needs to be changed, in most cases, it means that the model should be changed first. 
  - Then the changes you apply to the model are converted (conversion is covered below) to the view by specific converters.
- The view may need to be changed manually if the cause of such change is not represented in the model. 
  - For example, the model does not store information about the focus, which is a property of the view. 
  - When the focus changes, and you want to represent that in some element’s class, you need to change that class manually.

- There are two view writers:
- `DowncastWriter` is available in the` change()` blocks, used during downcasting the model to the view. 
  - It operates on a “semantic view” so a view structure which differentiates between different types of elements (see Element types and custom data).
- `UpcastWriter` is a writer to be used when pre-processing the “input” data (e.g. pasted content) which happens usually before the conversion (upcasting) to the model
  - It operates on “non-semantic views”.

- Just like in the model, there are 3 levels of classes in the view that describe points in the view structure: positions, ranges and selections.
  - A position is a single point in the document. 
  - A range consists of two positions (start and end). 
  - A selection consists of one or more ranges and has a direction (ltr/rtl).
- A view range is very similar to its DOM counterpart as view positions are represented by a parent and an offset in that parent. 
- unlike model offsets, view offsets describe:
  - points between child nodes of the position’s parent if it is an element, 
  - or points between the character of a text node if position’s parent is a text node.
- you can say that view offsets work more like model indexes than model offsets.
  - view中的一个位置可以有前面元素的末尾offset和后面元素的开头offset(一般是1)这2种表示方法

- Sometimes you may find in the documentation that positions are marked in HTML with the `{}` and `[]` characters. 
  - The difference between them is that the former indicates positions anchored in text nodes and the latter in elements.

- In order to create a safer and more useful abstraction over native DOM events, the view implements the concept of observers. 
  - It improves the testability of the editor as well as simplifies the listeners added by editor features by transforming the native events into a more useful form.
- An observer listens to one or more DOM events, does preliminary processing of this event and then fires a custom event on the view document. 
  - An observer not only creates an abstraction on the event itself but also on its data. 
  - **Ideally, an event’s consumer should not have any access to the native DOM**.
- By default, the view adds the following observers:
  - MutationObserver
  - SelectionObserver
  - FakeSelectionObserver
  - FocusObserver
  - KeyObserver
  - ArrowKeysObserver
  - CompositionObserver
- Additionally, some features add their own observers. 
  - For instance, the clipboard feature adds ClipboardObserver.

- Since all events are by default fired on `@ckeditor/ckeditor5-engine/src/view/document. Document`, it is recommended that third party packages prefix their events with an identifier of the project to avoid name collisions.

## conversion

- The three main situations in which model and view layers meet are:
- Data upcasting 将数据处理后保存到model
  - Loading/Set the data to the editor.
  - First, the data (e.g. an HTML string) is processed by a `DataProcessor` to a view `DocumentFragment`. 
  - Then, this `view document fragment` is converted to a `model document fragment`. 
  - Finally, the model document’s `root` is filled with this content.
- Data downcasting 获取model中的数据并转换到目标格式
  - Retrieving/Get the data from the editor.
  - First, the content of the model’s root is converted to a view document fragment. 
  - Then this view document fragment is processed by a data processor to the target data format.
- Editing downcasting 
  - Rendering the editor content to the user for editing.
  - This process takes place for the entire time when the editor is initialized. 
  - First, the model’s root is converted to the view’s root once data upcasting finishes. 
  - After that this view root is rendered to the user in the editor’s contentEditable DOM element (also called “the editable element”). 
  - Then, every time the model changes, those changes are converted to changes in the view. 
  - Finally, the view can be re-rendered to the DOM if needed (if the DOM differs from the view).

- Data pipeline
- Data upcasting is a process which starts in the view layer, passes from the data view, through a converter (green box) in the controller layer to the model document. 
  - Note: Data upcasting is also used to process pasted content (which is similar to loading data).
- Data downcasting is the opposite process to data upcasting.

- Editing pipeline / Editing downcasting
- there is no editing upcasting 
  - because all user actions are handled by editor features by listening to view events, analyzing what happened and applying necessary changes to the model. 
  - Unlike `DataController` (which handles the data pipeline),  `EditingController` maintains a single instance of the Document view document’s for its entire life. 
  - Every change in the model is converted to changes in that view so changes in that view can then be rendered to the DOM (if needed — i.e. if the DOM actually differs from the view at this stage).
# ui library
- Views use templates to build the UI. 
  - They also provide observable interfaces that other features (e.g. plugins, commands, etc.) can use to change the DOM without any actual interaction with the native API.

- Note that views encapsulate the DOM they render. 
  - Because the UI is organized according to the view-per-tree rule, it is clear which view is responsible for which part of the UI so it is unlikely that a collision occurs between two features writing to the same DOM node.
- Features can interact with the state of the DOM via the observable properties of the view

- Best practices
  - A complete view should provide an interface for the features, encapsulating DOM nodes and attributes. 
  - Features should not touch the DOM of the view using the native API. 
  - Any kind of interaction must be handled by the view that owns an element to avoid collisions

- Templates render DOM elements and text nodes in the UI library. 
  - Used primarily by views, they are the lowest layer of the UI connecting the application to the web page.

- Views are organized into collections which manage their elements and propagate DOM events even further. 
  - Adding or removing a view in a collection moves the view’s element in the DOM to reflect the position.
- It is advised that for the best user experience the editing view gets focused upon any user action (e.g. executing a command) to make sure the editor retains focus
- The framework offers built–in classes that help manage keystrokes and focus in the UI. 
  - They are particularly useful when it comes to bringing accessibility features to the application.
- The `FocusTracker` class can observe a number of HTML elements and determine if one of them is focused either by the user (clicking, typing) or using the `HTMLElement.focus()` DOM method.
- The `KeystrokeHandler` listens to the keystroke events fired by an HTML element or any of its descendants and executes pre–defined actions when the keystroke is pressed. 
  - Usually, each view creates its own keystroke handler instance which takes care of the keystrokes fired by the elements the view has rendered.
- 

# builds overview
- Predefined CKEditor 5 builds are a set of ready-to-use rich text editors.
  - **Every “build” provides a single type of editor with a set of features and a default configuration**. 
  - They provide convenient solutions that can be installed with no effort and that satisfy the most common editing use cases.

- Available builds
  - Classic editor
  - Inline editor
  - Balloon editor
  - Balloon block editor
  - Document editor

- In CKEditor 5 the concept of the “boxed” editor was reinvented:
  - The toolbar is now always visible when the user scrolls the page down.
  - By default the editor now grows automatically with the content.

- Inline editor comes with a floating toolbar that becomes visible when the editor is focused (e.g. by clicking it). 
  - Unlike classic editor, inline editor does not render instead of the given element, it simply makes it editable. 

- Balloon editor is very similar to inline editor. 
  - The difference between them is that the toolbar appears in a balloon next to the selection (when the selection is not empty)

- Balloon block editor is essentially the balloon editor with an extra block toolbar which can be accessed using the button attached to the editable content area and following the selection in the document. 
  - The toolbar gives an access to additional, block–level editing features.

- Document editor is focused on rich text editing experience similar to the native word processors. 
  - It works best for creating documents which are usually later printed or exported to PDF files.

- CKEditor 5 Framework should be used, instead of builds, in the following cases:
  - When you want to create your own text editor and have full control over its every aspect, from UI to features.
  - When the solution proposed by the builds does not fit your specific use case.
