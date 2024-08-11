---
title: lib-editor-codemirror-community-lang-lsp
tags: [codemirror, community, lsp]
created: 2024-08-11T07:59:46.588Z
modified: 2024-08-11T08:00:00.211Z
---

# lib-editor-codemirror-community-lang-lsp

# guide

# discuss-stars
- ## 

- ## 

- ## 
# discuss-lsp-worker
- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## [TypeScript integration · codesandbox/sandpack _202112](https://github.com/codesandbox/sandpack/discussions/237)
- Vocs is solving this elegantly with Twoslash

- 
- 

- ## ✏️🆚️ [Codemirror 6 and Typescript LSP - v6 - discuss. CodeMirror _202107](https://discuss.codemirror.net/t/codemirror-6-and-typescript-lsp/3398)
  - If anyone is still having problems with this, I was able to create a small demo based on @madebysid comment, you can find it here: https://github.com/okikio/codemirror 197, Demo Link: https://okikio-codemirror.netlify.app/

- For the @codesanbox/sandpack-react package there was a discussion on how to integrate the language server with codemirror.
- I’d like to share the progress I made on integrating the TypeScript LSP into Sandpack, which uses CodeMirror in the editor component. Fortunately, I could implement most of the features I had planned thanks to the amazing examples from @okikio and @madebysid.
- Here’s the full list of feature:
  IntelliSense; 
  Tooltip error; 
  Multiple files; 
  Support tsconfig.json; 
  Automatically dependency-types fetching (CodeSandbox CDN); 
  In-browser dependency cache; 
- TBH, I’m not an expert on CodeMirror even less on LSP, so I’m curious to know how I can improve this implementation and make it even better
  - https://codesandbox.io/p/sandbox/github/danilowoz/sandpack-tsserver/tree/main/

- Did https://codesandbox.io/ switch away from CodeMirror to Monaco for it’s TypeScript/LSP editor? If so, is there a discussion somewhere of why? _202212
  - 💡 Actually, CodeSandbox has always used Monaco as the default editor, except for a specific mobile version where we defaulted it to CodeMirror.
- Not to be pedantic, but it’s worth noting that tsserver / the typescript standalone worker is not LSP compatible.
  - Replit is working on open sourcing our LSP Client (we didn’t the microsoft packages) and a follow up to open source the LSP client + codemirror extension. Timeline TBD but should happen in 2023

- We were able to leverage much of the learning discussed here to implement Typescript completions for our open source multiplayer code editor VZCode
- It’s a more bit complex than the examples here because:
  - The system supports editing multiple files
  - The system supports remote collaborators (so their changes need to be accounted on the LSP side for in addition to local changes)
  - There are multiple instances of the CodeMirror extension that talk to a singleton language server
  - The singleton language server lives in a Web worker
