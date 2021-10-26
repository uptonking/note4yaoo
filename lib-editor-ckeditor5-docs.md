---
title: lib-editor-ckeditor5-docs
tags: [ckeditor, editor]
created: '2021-10-25T09:32:44.058Z'
modified: '2021-10-25T09:33:13.353Z'
---

# lib-editor-ckeditor5-docs

# guide

# builds overview
- Predefined CKEditor 5 builds are a set of ready-to-use rich text editors.
  - Every “build” provides a single type of editor with a set of features and a default configuration. 
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


# editing engine

- The editing engine implements an MVC architecture.
- There is one model document which is converted into separate views — the editing view and the data view.
  - These two views represent, respectively, the content that the user is editing (the DOM structure that you see in the browser) and the editor input and output data (in a format that the plugged data processor understands). 
  - Both views feature virtual DOM structures (custom, DOM-like structures) on which converters and features work and which are then rendered to the DOM.
- features control what changes are made to the model, how they are converted to the view and how the model needs to be changed based on fired events (the view’s and model’s ones).

## model
- The model is implemented by a DOM-like tree structure of elements and text nodes. 
  - Unlike in the actual DOM, in the model, both elements and text nodes can have attributes.
  - Like in the DOM, the model structure is contained within a document that contains root elements (the model, as well as the view, may have multiple roots). 
  - The document also holds its selection and the history of its changes.
- Finally, the document, its schema and document markers are properties of the Model. 
  - An instance of the Model class is available in the `editor.model` property. 
  - The model, besides holding the properties described above, provides the API for changing the document and its markers, too.
- All changes in the document structure, of the document’s selection and even the creation of elements, can only be done by using the model writer. 
  - Its instance is available in change() and enqueueChange() blocks.
- All changes done within a single change() block are combined into one undo step (they are added to a single batch). 
  - When nesting change() blocks, all changes are added to the outermost change() block’s batch.
- All changes made to the document structure are done by applying operations(from OT).
  - Since OT requires a system to be able to transform every operation by every other one (to figure out the result of concurrently applied operations), the set of operations needs to be small. 
  - CKEditor 5 features a non-linear model (normally, OT implementations use flat, array-like models while CKEditor 5 uses a tree structure), hence the set of potential semantic changes is more complex. 
  - Operations are grouped in batches. A batch may be understood as a single undo step.


- Text styles such as “bold” and “italic” are kept in the model not as elements but as text attributes (think — like element attributes). 
  - Such representation of inline text styling allows to significantly reduce the complexity of algorithms operating on the model. 


- The engine also defines three levels of classes that operate on offsets:
  - A Position instance contains an array of offsets (which is called a “path”)
- 



- 
- 
