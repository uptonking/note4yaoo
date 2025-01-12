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

# ext-Capabilities
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

## Restrictions

- No DOM Access
  - Extensions have no access to the DOM of VS Code UI. You cannot write an extension that applies custom CSS to VS Code or adds an HTML element to VS Code UI.
  - To ensure that extensions cannot interfere with the stability and performance of VS Code, and that we can continue to improve the DOM of VS Code without breaking existing extensions, we run extensions in an Extension Host process and prevent direct access to the DOM.

- No custom style sheets
  - A custom style sheet provided by users or extensions would work against the DOM structure and class names. These are not documented as we consider them internal.
  - Instead, VS Code aims to provide a well-designed extension API supporting UI customizations. The API is documented, comes with tooling and samples
# more
