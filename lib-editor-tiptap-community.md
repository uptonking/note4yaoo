---
title: lib-editor-tiptap-community
tags: [community, editor, prosemirror, tiptap-editor]
created: 2022-08-19T23:08:02.074Z
modified: 2023-02-05T19:03:27.730Z
---

# lib-editor-tiptap-community

# guide

- resources
  - https://discuss.prosemirror.net/search?q=tiptap
# discuss-stars
- ## [Markdown input and output_201810](https://github.com/ueberdosis/tiptap/issues/66)
- [prosemirror official Friendly Markdown example](https://prosemirror.net/examples/markdown/)
  - 支持在markdown和wysiwyg间切换，无外部依赖
- At the moment it's not possible to add this functionality with extensions. That's something I have to add to the core.
- I don’t see us adding this to the core, it’s just too different. So I’m closing this here for now. Consider using CodeMirror, if you really want to work with Markdown.

- ## Comparison to raw ProseMirror, esp. regarding collaboration. 
- https://github.com/ueberdosis/tiptap/discussions/1507
- Everything you can do with ProseMirror, you can also do with tiptap. 
  - The goal of tiptap is to bundle some related logic into extensions (e.g. schema, commands, input rules), and to make some complex APIs more accessible (e.g. chained commands). 
  - We also provide a documentation with many examples and extensions so it’s way easier to start than with plain ProseMirror.
- y.js builds on top of CRDT instead of OT. 
- Anyway, we’re doing a big bet on Y.js. 
  - CRDT are the future, and Y.js is the most performant implementation. 
  - It has a huge ecosystem, and new community projects pop up every week. 
  - If you want to go the OT-way, you can do that with tiptap as you would do it with ProseMirror. 
  - All parts and APIs of ProseMirror are accessible through tiptap.

- ## Tiptap 2 beta is here_202104
- https://discuss.prosemirror.net/t/tiptap-2-beta-is-here/3710
  - Commands are chainable. 
  - Support for text align. 
  - Render nodes as react components or vue components
  - Show suggestions for things like mentions 2 or slash commands 
- I’ve been taking a sneak peak at your new API and decided to use a similar approach myself. 
  - Basically just turning PM plugins into React components that have their own props instead of one massive EditorProps object.
- So having dabbled myself mostly with React+PM integration, I’ll ask the basic ones that are on my mind - how do components subscribe to the global editor state? Observables? Also, do you intend to allow the use of some central event message bus, a la Redux?
- by looking into your ReactNodeView - it seems you have avoided the use of ReactDOM completely? No portals nothing?
  - I’m using portals! You can see it in react/src/EditorContent.tsx 
- One thing I’ve been thinking about is how to manage the state fetched from the API. For example collaboration participants
  - We provide first class support with Y.js collab.
  - It’s definitely a PITA to implement with the bare collab module. Yet I’m still a bit ambivalent about Yjs, like is it easy to switch between single and multiplayer editing and how much memory it actually consumes in the server.
  - But what I was getting at that do you implement the API providers as extensions or as separate services. Not a huge difference but something I myself am pondering. I guess having one entity for everything makes things simple.
- Also, I have a tricky question that’s been on my mind. What’s your approach for rolling out breaking schema changes?
  - We do not currently provide anything for this. However, I find it best to migrate the JSON data manually on the server side.
- One thing I’d like to see, for Tiptap and PM in general, is good testing support with jsdom. Seems pretty important considering how complicated the editors can get.
  - I haven’t had good experiences with JSDOM, so we run all tests with Cypress. Works great! 
- What do you mean by global editor state? State from the editor or from your react app?
  - Yeah I meant the whole app: editor plugin state, extension state, UI state, API state and so forth. It seems that to manage the whole thing you need message passing of some sorts, which you seem to provide as well with editor pub/sub events, but I was wondering if you had some interesting new angle to it.
- Well in theory that’s all you need and useContext does work for providing state but. React doesn’t have as nice built-in state management as Vue and useContext can get quite tedious to work with. Moreover, the nature of PM’s event loop combined with the handling collaboration events and whatnot does seem the steer the whole architecture towards more event-based state management.
  - As one example let’s consider updating a component based on a plugin state change. So the simplest way is to make one context that has the editorState which you can replace in the dispatchTransaction call. 
  - Yet the component would update on every transaction and you’d have to check inside the component to see if the plugin state has changed. 
  - So you want to slice the state to make the updates as minimal as possible but it’s not very convenient with pure useContext. 
  - I myself made some hacky pub/sub pattern where I trigger a provider in the plugin’s apply function whenever plugin state changes but I definitely have to refactor it when I have the time. 
  - Curvenote put everything into Redux which seems nice but I don’t want to deal with its boilerplate.
  - To be frank it may be even impossible to add in a similar state management into an editor framework versus making your custom editor. So it’s a bit tricky.
- Why would the component update on every transaction. I was able to create a very simple hook for https://bangle.dev that reads a plugin state, it is working great for me and doesn’t utilize the event pub sub pattern.
  - Because EditorState is recreated on every transaction thus it would always update if the component was subscribed to changes to it. 
  - From what I can tell from your code, you are doing precisely what I said you have to do which is to slice the state somehow to the components. 
  - And sure, you’re not using pub/sub per say although one could think of editor transactions that change the plugin state as published events. 
  - But any state that would not be inside plugin state and still be relevant, eg API/UI stuff, you would have to engineer your own method of triggering changes somehow and relaying them forward.
  - Using React context for that purpose sucks.
# discuss-news
- ## 

- ## 

- ## 

- ## 

- ## Released “Snapshot Compare” for Tiptap to make tracking changes between document versions simple and visual _202411
- https://x.com/tiptap_editor/status/1852018294682767647
  - right within the editor like you know from Google Docs or MS Word. 

- ## we're working on something... What should we call it? Track changes? _202407
- https://x.com/tiptap_editor/status/181537635366484  7993
  - The first version is just tracking changes, laying the basis for suggestions like you described coming in the next version.

- Will change diffing work with pure TipTap/ProseMirror documents as well? or is it tied to the live documents in your cloud offering?
  - It is stored in Y.doc, so it does not run on pure Tiptap/PM.

- Any ideas yet on what a "version" would be. In Yjs it's sometimes difficult to properly group changes and not end up with loads of versions
  - Actually, ours is mostly based on Yjs snapshots.
# discuss-not-yet 🐛
- ## 

- ## 

- ## [Github like `diff` extension to compare two versions _202401](https://github.com/ueberdosis/tiptap/discussions/4800)
- the diff view is on our Q1 roadmap and we're working on a POC. Things escalated a bit because a diff view in combination with version history was more complex to solve than we thought 

# discuss
- ## 

- ## 

- ## [Append text to current editor's content · Issue #230 · ueberdosis/tiptap](https://github.com/ueberdosis/tiptap/issues/230)

```JS
editor.chain().focus().insertContent('some content').run();

editor.chain().focus('end').createParagraphNear().insertContent('some content').run()
```

- [Append text/info to the end of the document · Issue #696 · ueberdosis/tiptap](https://github.com/ueberdosis/tiptap/issues/696)

- ## [[Bug]: `generateJSON` is stripping trailing whitespace · Issue #4432 · ueberdosis/tiptap](https://github.com/ueberdosis/tiptap/issues/4432)
- `editor.commands.setContent("<p>Example Text </p> ", false, { preserveWhitespace: true });`

- ## Just in case anyone tries to use Hocuspocus with NestJS in the future, this code allows me to run hocuspocus (although a bit hacky) without issues_20221005
- https://discord.com/channels/818568566479257641/818569767149371444/1027216475179712692

```JS
import { WebSocket, Server } from 'ws';
import { OnGatewayInit, WebSocketGateway, WebSocketServer } from '@nestjs/websockets';
import { hocuspocus } from '@/hocuspocus';
import { Request } from 'express';
import url from 'url';

const extractString = (x: (string | string[]) | undefined) => (x && Array.isArray(x) ? x[0] : x) as string | undefined;

@WebSocketGateway({ path: `/collaboration` })
export class CollaborationGateway implements OnGatewayInit {
  @WebSocketServer()
  server: Server;

  afterInit(server: Server) {
    server.on(`connection`, (socket: WebSocket, request: Request) => {
      const query = url.parse(request.url, true).query;

      const documentId = extractString(query?.documentId);

      if (documentId) {
        hocuspocus.handleConnection(socket, request, documentId);
      }
    });
  }
}

new HocuspocusProvider({
  url: `${protocol}//${providerUrl.host}/collaboration?documentId=${documentId}&ignore=`,
  name: documentId,
  document: new Y.Doc({ guid: documentId }),
})
```
