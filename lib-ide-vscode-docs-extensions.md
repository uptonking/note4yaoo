---
title: lib-ide-vscode-docs-extensions
tags: [docs, extensions, vscode]
created: 2025-01-11T10:42:03.445Z
modified: 2025-01-11T10:42:21.734Z
---

# lib-ide-vscode-docs-extensions

# guide

# overview

# [docs-api](https://code.visualstudio.com/api)

- Here are some examples of what you can achieve with the Extension API:
  - Change the look of VS Code with a color or file icon theme - Theming
  - Add custom components & views in the UI - Extending the Workbench
  - Create a Webview to display a custom webpage built with HTML/CSS/JS - Webview Guide
  - Support a new programming language - Language Extensions Overview
  - Support debugging a specific runtime - Debugger Extension Guide

- The extension entry file exports two functions, activate and deactivate. 
  - activate is executed when your registered Activation Event happens. 
  - deactivate gives you a chance to clean up before your extension becomes deactivated. if an extension needs to perform an operation when VS Code is shutting down or the extension is disabled or uninstalled, this is the method to do so.

- There are five options for storing data:
  - `ExtensionContext.workspaceState`: A workspace storage where you can write key/value pairs. VS Code manages the storage and will restore it when the same workspace is opened again.
  - ` ExtensionContext.globalState` : A global storage where you can write key/value pairs. VS Code manages the storage and will restore it for each extension activation.
  - `ExtensionContext.storageUri`: A workspace specific storage URI pointing to a local directory where your extension has read/write access. This is a good option if you need to store large files that are accessible only from the current workspace.
  - `ExtensionContext.globalStorageUri`: A global storage URI pointing to a local directory where your extension has read/write access. This is a good option if you need to store large files that are accessible from all workspaces.
  - `ExtensionContext.secrets`: A global storage for secrets (or any information that is sensitive) that will be encrypted. These are not synced across machines. 
    - For VS Code desktop, this leverages Electron's `safeStorage` API. 
    - For VS Code for the Web, this uses a Double Key Encryption (DKE) implementation.

- "Workbench" refers to the overall Visual Studio Code UI that encompasses the following UI components:
  - Title Bar
  - Activity Bar
  - Side Bar
  - Editor Group
  - Panel
  - Status Bar

- 
- 
- 
- 
- 
- 

## api-Capabilities

- Common Capabilities are core pieces of functionality that you can use in any extension.
  - Registering commands, configurations, keybindings, or context menu items.
  - Storing workspace or global data.
  - Displaying notification messages.
  - Using Quick Pick to collect user input.
  - Open the system file picker to let users select files or folders.
  - Use the Progress API to indicate long-running operations.

- Theming
  - Change colors of your source code(editor).
  - Change colors of the VS Code UI.
  - Port an existing TextMate theme to VS Code.
  - Add custom file icons.

- Declarative Language Features adds basic text editing support for a programming language such as bracket matching, auto-indentation and syntax highlighting. 
  - Bundle common JavaScript snippets into an extension.
  - Tell VS Code about a new programming language.
  - Add or replace the grammar for a programming language.
  - Extend an existing grammar with grammar injections.
  - Port an existing TextMate grammar to VS Code.

- Programmatic Language Features
  - add rich programming language support such as Hovers, Go to Definition, diagnostic errors, IntelliSense and CodeLens
  - These language features are exposed through the `vscode.languages.*` API.
  - An extension can either use these API directly, or write a Language Server and adapt it to VS Code using the VS Code Language Server library.
  - Add hovers that show sample usage of an API.
  - Report spelling or linter errors in source code using diagnostics.
  - Register a new code formatter for HTML.
  - Provide rich, context-aware IntelliSense.
  - Add folding, breadcrumbs and outline support for a language.

- Workbench Extensions
  - Add custom context menu actions to the File Explorer.
  - Create a new, interactive TreeView in the Side Bar.
  - Define a new Activity Bar view.
  - Show new information in the Status Bar.
  - Render custom content using the WebView API.
  - Contribute Source Control providers.

- Debugging
  - writing Debugger Extensions that connect VS Code's debugging UI to a specific debugger or runtime.
  - Connect VS Code's debugging UI to a debugger or runtime by contributing a Debug Adapter implementation.
  - Specify the languages supported by a debugger extension.
  - Provide rich IntelliSense and hover information for the debug configuration attributes used by the debugger.
  - Provide debug configuration snippets.
  - Start debug sessions based on dynamically created debug configurations.
  - Track the lifecycle of debug sessions.
  - Create and manage breakpoints programmatically.

### Restrictions

- No DOM Access
  - Extensions have no access to the DOM of VS Code UI. You cannot write an extension that applies custom CSS to VS Code or adds an HTML element to VS Code UI.
  - To ensure that extensions cannot interfere with the stability and performance of VS Code, and that we can continue to improve the DOM of VS Code without breaking existing extensions, we run extensions in an Extension Host process and prevent direct access to the DOM.
- VS Code aims to deliver a stable and high performance editor to users, and misbehaving extensions should not impact the user experience. The Extension Host in VS Code prevents extensions from:
  - Impacting startup performance
  - Slowing down UI operations
  - Modifying the UI

- No custom style sheets
  - A custom style sheet provided by users or extensions would work against the DOM structure and class names. These are not documented as we consider them internal.
  - Instead, VS Code aims to provide a well-designed extension API supporting UI customizations. The API is documented, comes with tooling and samples

## api-webview

- A webview can render almost any HTML content, and it communicates with extensions using message passing. 
  - This freedom makes webviews incredibly powerful, and opens up a whole new range of extension possibilities.
- Webviews are used in several VS Code APIs:
  - With Webview Panels created using createWebviewPanel. In this case, Webview panels are shown in VS Code as distinct editors. 
  - As the view for a custom editor. Custom editors allow extensions to provide a custom UI for editing any file 
  - In Webview views that are rendered in the sidebar or panel areas.
- webview should be used sparingly and only when VS Code's native API is inadequate. 
  - Webviews are resource heavy and run in a separate context from normal extensions. 
- Webview panels are owned by the extension that creates them. The extension must hold onto the webview returned from `createWebviewPanel`. 
  - If your extension loses this reference, it cannot regain access to that webview again, even though the webview will continue to show in VS Code.
- Webviews run in isolated contexts that cannot directly access local resources. This is done for security reasons.
  - you must use the Webview.asWebviewUri function to convert a local file: URI into a special URI that VS Code can use to load a subset of local resources.

- Web Workers are supported inside of webviews but there are a few important restrictions to be aware of.
  - First off, workers can only be loaded using either a data: or blob: URI. You cannot directly load a worker from your extension's folder.
  - If you do need to load worker code from a JavaScript file in your extension, try using fetch
  - Worker scripts also do not support importing source code using importScripts or import(...). If your worker loads code dynamically, try using a bundler such as webpack to package the worker script into a single file.

- 
- 

## api-editor

- Custom editors allow extensions to create fully customizable read/write editors that are used in place of VS Code's standard text editor
- Custom editors build on a lot of VS Code concepts—such as webviews and text documents

- A custom editor is an alternative view that is shown in place of VS Code's standard text editor for specific resources. There are two parts to a custom editor: 
  - the view that users interact with 
  - and the document model that your extension uses to interact with the underlying resource.
- The view side of a custom editor is implemented using a webview. 
  - This lets you build the user interface of your custom editor using standard HTML, CSS, and JavaScript. 
  - Webviews cannot access the VS Code API directly but they can talk with extensions by passing messages back and forth
- The other part of a custom editor is the document model. 
  - This model is how your extension understands the resource (file) it is working with. 
  - A CustomTextEditorProvider uses VS Code's standard TextDocument as its document model and all changes to the file are expressed using VS Code's standard text editing APIs.
  - CustomReadonlyEditorProvider and CustomEditorProvider on the other hand let you provide your own document model, which lets them be used for non-text file formats.
- Custom editors have a single document model per resource but there may be multiple editor instances (views) of this document.
  - there is still just a single TextDocument since there is still just a single copy of the resource in the workspace, but there are now two webviews for that resource.

- if you are working with a text based file format use CustomTextEditorProvider, for binary file formats use CustomEditorProvider.

- 
- 
- 
- 
- 

## Virtual Documents

- The text document content provider API allows you to create readonly documents in Visual Studio Code from arbitrary sources.
- Note how the provider doesn't create uris for virtual documents - its role is to provide contents given such an uri. In return, content providers are wired into the open document logic so that providers are always considered.

- Depending on the scenario virtual documents might change. To support that, providers can implement a `onDidChange`-event.

- The event emitter has a fire method which can be used to notify VS Code when a change has happened in a document.

- If you need more flexibility and power take a look at the `FileSystemProvider` API. 
  - It allows to implement a full file system, having files, folders, binary data, file-deletion, creation and more.

- 
- 
- 
- 

## web-extension

- When VS Code is used in the Web, installed extensions are run in an extension host in the browser, called the 'web extension host'.
  - An extension that can run in a web extension host is called a 'web extension'.
- Web extensions still have access to the full VS Code API, but no longer to the Node.js APIs and module loading.
- The web extension runtime is supported on VS Code desktop too
# ext-

# more
