---
title: lib-editor-slate-issues-stars
tags: [issues, slate-editor]
created: 2022-05-15T18:48:42.427Z
modified: 2023-02-05T19:03:12.723Z
---

# lib-editor-slate-issues-stars

# guide

# issues

## 

## [Editor crashes with redux](https://github.com/ianstormtaylor/slate/issues/3478)

- bug: The editor crashes if we connect the `onChange` function with redux action and our typing speed is just nominally fast, and wait for the state update. Given below in the codesandbox link just try to type nominally fast and the editor will crash.

- I am facing the same issue. I used debounce to solve this problem.
  - As a React developer, we like to put everything into the single source to manage state. However, if you need to update a big big big state like our SlateEditor, you have to bypass it by storing the latest value and skip unnecessary updates to Redux store. 
  - Our Redux store will be updated too frequently. It's costy becaues the state of SlateEditor is really huge. It's a JSON format, not just a pure text. What we can do is to use debounce. 
  - until we found user have finished their input, and then store a complete string "12345678999999999" into our Redux store.

- I think the reproducing example is slightly misleading. I believe the core of the issue is calling onChange asynchronously, and not necessarily taking a lot of time. As long as your redux update remains synchronous, I believe it should work fine.

- I understand the desire to keep state consistently in redux if possible, but unless you have a specific reason to have slate read from your redux store, it seems more performant to not subscribe to it.

- 💡 As I said: we had the same issue with Apollo Client. And we did exactly the same: we kept the state close to the editor. However, I suppose people will run into that issue again and again since it's pretty common to hold you state in a global data store like Redux. Maybe we could add a hint in the docs at least? 

- did you read the advice in the thread and make dispatch to the redux store a one way operation? Or are you also consuming the value updates asynchronously from the redux store? Doing the latter is going to cause a delay in slate receiving value updates and is going to make it not work correctly.

## [Introduce `editor.transaction()` to replace `without*` functions](https://github.com/ianstormtaylor/slate/issues/2658)

- But it seems to me like in the most recent version `Editor.withoutNormalizing` pretty much does what is suggested here and the withoutSaving and withoutMerging functions seem to not exist anymore.

## [Feature suggestion: isolated/atomic operation groups in HistoryEditor](https://github.com/ianstormtaylor/slate/issues/3874)

- My question here is how is this different than just using `Editor.withoutNormalizing`, which basically batches a set of Operations into an "atomic" unit anyways (and, as a consequence, makes the history state include that batch of operations)? I think `Editor.withoutNormalizing` could be renames to `Editor.transaction` really and it might be more descriptive.

- when you use `Editor.withoutNormalizing` and multiple Operations are submitted within the callback, then all those Operations are merged into a single array in the history stack.
  - When we want to ensure a given "user action" is 1 history event, we wrap it in Editor.withoutNormalizing. This works for wrapping/unwrapping links, etc. in our codebase as it stands now.
  - I am actually in favor of renaming `Editor.withoutNormalizing` to `Editor.transaction` as that is more descriptive of what it actually does.

- If you want to batch Operations, defer normalization and onChange and have those batched operations show up in the history stack in a single array, that is what Editor.withoutNormalizing is for.

- Operations are batched (per event tick) automatically; that's what the Promise.resolve in createEditor() does.
  -  I assume this exists so onChange doesn't fire for every single operation. 

- Your change to how onChange gets called is interesting (synchronously instead of like currently on next tick), do you think it could be a reasonable default?
  - Yes, we have been using it for 12 months at Aline and it works very well. Just wrap anything you don't want to synchronously normalize in withoutNormalizing and you're good.

## [Selection is null after editor loses focus](https://github.com/ianstormtaylor/slate/issues/3412)

- 思路1
  - 在编辑器失焦业务逻辑前如openDialog，手动保存editor.selection，然后在修改编辑器数据如setNodes前先设置选区
    - editor.selection = savedEditorSelection
    - If you want to show the selection, may be try `Transforms.setSelection` or `Transforms.select`.
- 思路2
  - 覆盖slate内部的方法，使得deselect逻辑不执行
- 思路3
  - 在Editable的onBlur方法中保存选区 editor.blurSelection = editor.selection
  - 不能在onFocus中设置选区，因为光标变化时，一直处于focus状态，就不会执行onFocus事件
  - 然后在修改编辑器数据如setNodes先设置选区
  - 没必要在onFocus中自动恢复选区，除非业务需要，利用onBlur和onFocus可自动保存和恢复选区，甚至可以在选区变空时给原选区位置addMark来显示蓝色状态
- 思路4
  - 不使用editor的active selection，在link业务组件里面所有操作都与link-path直接绑定

- 编辑器失焦时蓝色selection不可见的问题
  - 临时方案是在编辑器失焦时添加leaf属性，恢复焦点时移除leaf属性，可以在编辑器框架层实现这个逻辑
    - https://github.com/ianstormtaylor/slate/issues/3412#issuecomment-1147955840

- `Transforms.select(editor: Editor, target: Location)`; 
  - Set the selection to a new value specified by `target`. 
  - When a selection already exists, this method is just a proxy for `setSelection` and will update the existing value.
- `Transforms.setSelection(editor: Editor, props: Partial<Range>)`; 
  - Set new properties on an active selection. 
  - Since the value is a `Partial<Range>`, **this method can only handle updates to an existing selection**. 
  - If there is no active selection, the operation will be void. 
  - Use `select` if you'd like to create a selection when there is none.

- Found a work around for this issue thanks to a kind developer on slack channel. Writing here in case anybody needs it. 
  - Store the selection value just before the editor loses focus. 
  - In my case it was when I clicked on input field, so I stored it just when dialog box opens. 

- I know Notion does something very similar in its editor; 
  - when you highlight some text and try to insert a hyperlink, they insert a fake blue wrapper span styled to look like a regular selection, and then they delete it afterwards.

- a quick work around, is to not allow the editor to be unselected
  - You can either run your own logic, or you can just "monkey patch" Transforms.deselect to be a empty function in the begginging of your app, 
  - this worked like a charm, and I can seem where this is actually being used on the internals of Slate apart from Focus/UnFocus.
- Better scenario would be to actually change Editable to not call deselect via a prop or something, and you would manually call deselect ( in case for multiple editors on the same page)

- I don't know if this is a bug or expected behaviour. But here if you have value of selection with you (which is `editorSelection.current` ), you can pass it down to editor ( `editor.selection = editorSelection.current` ) before passing editor to `Transforms.insertNode` or anywhere else. 
  - If you want to show the selection, may be try Transforms.setSelection or Transforms.select.

- One alternative solution: When focus leaves the editor, wrap the current selection in a fake custom selection node. 
  - Then, instead of relying on `editor.selection` being non-null, perform all operations and checks relative to that unique selection node. 
  - And instead of using `editor.selection`, you can now define a custom `editor.getSelection` method that returns either the path/location of that fake selection or falls back to `editor.selection`. 
  - Then remove the fake selection when the editor is re-focused.
  - that's the basic idea: **Just like you have other inline nodes (hyperlinks and whatever else), you can also mock up a selection node that doesn't get serialized/deserialized and is only a run-time helper**.

- You can get around this issue by setting readOnly to true before opening the link input or focusing outside the editor, and then setting back to false when done.

- Here is my solution to this problem:
  - Add "onBlur" handler to the `<Editable>` tag. In that handler save selection to some property on the editor. E.g. blurSelection
  - Slate sets selection to null after blur, so before executing a command on the editor, you need to set selection to the saved one. Do it with Transforms.select(editor, editor.blurSelection); 
  - since we have selection we can use ReactEditor.focus(editor) to return focus, so users can just continue typing.
  - Make sure that your command doesn't modify selection under the hood. If you split nodes or change blocks that might be a case.

- Hey guys, what if you use onMouseDown instead of onClick? This doesn't reset focus for me.
  - I also added a preventDefault() at the end of the onMouseDown and it kept both selection and focus for me.

- It's not easy to keep the selection visually because it's the same document. 
  - You could have a custom "Selection" plugin which draws a background behind the selection to have a visual effect maybe?
- I think the safest solution is what you suggested, and draw a background explicitly when the focus is not there.

## [Only use Slate Provider's value prop as initial state__202109.v0.70.0](https://github.com/ianstormtaylor/slate/pull/4540)

- [`value` should be renamed to `initialValue`](https://github.com/ianstormtaylor/slate/issues/4992)

> `slate-react` 中Slate组件经历了 非受控  > 受控  >  非受控 的过程

- the `value` prop that must be passed to the `Slate` provider is kind of a hoax because in reality this prop has to be exactly what has been passed to `onChange`. This changes the `Slate` provider to relax this requirement. 
- The `value` prop is now only used on the initial render to initialize the value prop. On subsequent changes it is ignored.

- 👀️ onChange should not be the only way of changing the Component's value. If you rely on a database to render your content, you'll also want to pass the new value using the value prop. In that case you don't want to rely on a local state that is changed with onChange.
  - An example would be when you need to display someone else changes to the value.

- slate used to offer an API similar to any generic input, whereby it exposed props such as value and onChange. This enabled users to interact and maintain the value of the input with a `useState` hook

- 👉🏻️ I definitely see how, since slate uses operations to mutate its state, using a controlled value pattern would be inconsistent. Specially considering that onChange is triggered for all operations including `set_position`

### [Delayed setState(value) results in Cannot resolve a DOM point from Slate point ](https://github.com/ianstormtaylor/slate/issues/3575)

- In my case, I'm using Apollo to keep some text in sync with the server
  - I also encountered the same issue while trying to sync with some quite large (and badly written) Redux store

- As far as I can tell, the `value` prop is really only meant to be used as an initial value. 
  - When applying a different `value` prop (one that was not returned from onChange) later on this can cause all kinds of problems because `editor.selection`, and the history stack from `slate-history` (if you use that) can still contain values related to the old slate value. Perhaps it's a good idea to rename the value prop to initialValue instead?

- As pointed out by @phamstack, this state mismatch can happen even on seemingly synchronous operations.
  - **React state updates are by nature asynchronous, so there's isn't any guarantee that they will run quickly enough to satisfy Slate's requirements**.
- The possible solutions I can think of are:
  - Make Slate keep an internal `value` state, that gets kept in sync with what's passed in by props (difficult); 
  - Make Slate wait to run selection operations until the content is updated (may introduce lag); 
  - Make Slate silently fail - gracefully handle these errors; 

- While you are correct that React updates are by nature asynchronous, Slate uses the ReactDOM.unstable_batchedUpdates helper to mitigate that

- This is a problem when doing collaborative editing. Say user A has focus on line 2. User B removes the line above (line 1). 
  - As far as I can tell there is no way I can adjust the selection for user A before Editable in slate-react tries to update the selection itself and fails because now line 2 no longer exists.
  - So far I have forked slate-react and just fail silently, and then adjust the selection myself

- I have the same problem described by @skogsmaskin. My application already has collaboration built-in, which powers other widgets (slate is just one of them). I am opting out of slate's collaborative handling and instead piggybacking on my own app's infrastructure to make things more uniform
  - This error bites me constantly - when collaborating and also when using undo/redo (which, again, works through my own app code for consistency rather than using slate's system).
  - User types paragraph A, then types paragraph B, then clicks undo. Paragraph A no longer exists, the selection is invalid, slate crashes.
  - I also cannot store/reset the selection as part of the undo/redo mechanism, unless I use slate's system.

- Slate core has a couple of ways to deal with this:
  - both document contents (editor.children) and selection (editor.selection) are simple properties and can be changed at the same time.
  - in collaboration, when an operation is applied to the editor, it will automatically update the selection (along with all other Ref instances).
- **So perhaps the React editor should expose the ability to include selection in the state, as the core does**, but I also wonder if we need some documentation around getting started with collaboration. 
  - The Slate design goal is (as far as I can tell) to synchronise based on operations, not state, for the best user experience.

- Same issue here with remote updates as @skogsmaskin & @gabriel-peracio described, as current workaround I'm removing selection during the remote update (collaboration mode or history updates), and set it back once value updated

- I'm doing something like notion when the user types '/' then a popup appears to select a block type and after selecting a block I want to remove that slash so I'm taking a backup when user types '/' and then resetting the value with backup after selecting a block, So how can I achieve this without passing a value to slate?
  - You could use the Transforms interface to remove the current line.

### [Bug: Cannot update slate state externally](https://github.com/ianstormtaylor/slate/issues/4612)

- It works, but I agree, it's a hack. Setting `editor.children` directly also requires manual fixing of `selection`, because selected range remains the same even if some new nodes are added above the selection.

- It does not seem like a hack based on the PR discussion. It's just not a React way, and not necessary to be a React way.

- It took me several days to find out that changes in #3216(201912, Slate改为受控组件) were silently reversed in #4540(202109, Slate改为非受控组件).

- I think you got it right in the controlled component vs uncontrolled component part. I originally argued in an issue that **it should be explicitly an uncontrolled component because some people were getting problems with the selection not updating as a result of setting the "controlled" value state**, see #3575 (comment).
  - The problem is that whenever editor.children gets changed outside of slate's knowledge it has the potential to cause different inconsistencies to happen including the Cannot resolve a DOM point from Slate point error
  - I find people generally get confused by the "passing value" API as it seems to indicate that's how you propagate changes, the "reacty" way. 
  - But in reality slate operates on operations and keeps its internal state consistent using them. An API that reflects this behavior is therefore desirable was my reasoning.
- Note that an Editor.reset method was proposed there which would then also handle the selection resetting and the history resetting (which wasn't handled by passing a different `value` prop). 
  - As mentioned above setting editor.children explicitly to an initial value is the recommended way for now. 

- For now, I've done as described above in this thread and added a `key` based on `initialValue` to a `div` containing the `Slate` editor.

- [State is uncontrolled in slate-react@0.70.0](https://github.com/ianstormtaylor/slate/issues/4646)
  - what is the best way right now for changing state as a whole?
  - it can be changed directly by `editor.children = value`

- [Delayed setState(value) results in Cannot resolve a DOM point from Slate point](https://github.com/ianstormtaylor/slate/issues/3575)
  

## [Triple-click selection and Selection API issue](https://github.com/ianstormtaylor/slate/issues/4329)

- The basic issue as I understand it is that the DOM selection API supports two kinds of selection endpoint:
  - text node + character offset (I'll call it a "text endpoint")
  - element node + child offset (I'll call it an "element endpoint"), used to signify that entire elements are in the selection, not just the text inside them
- **but Slate selections support only text endpoints**.
- When a DOM selection has an element endpoint, Slate looks for a corresponding text endpoint (ReactEditor.toSlatePoint). 
  - In most cases, this text endpoint is after the original element endpoint; 
  - so when the focus of a forward selection is an element endpoint, the Slate selection is "hanging": 
  - its focus is at the beginning of the following block.
- Browsers vary on exactly what actions produce element endpoints, but they are generally actions that sensibly mean "select the whole element":
  - triple-click on a paragraph
  - place the cursor at the beginning of a paragraph, shift-arrow-down past the end of the paragraph
  - place the cursor at the beginning of a paragraph, shift-arrow-right to the end of the paragraph (selects the text within the paragraph), then shift-arrow-right again (selects the whole paragraph)
  - drag the cursor from the beginning of a paragraph to the end (selects the text within the paragraph), then drag a little further / down (selects the whole paragraph)
- All of these generate element endpoints (in most cases) in the browsers I've tested (Chrome, Firefox, Safari, all on a Mac), and in most cases the element endpoints turn into a hanging selection in Slate.
  - It's good to have hanging selections! There's no other way in Slate to represent the selection of a whole block, and there are lots of actions that sensibly work on a whole block

- 👉🏻 But hanging selections have some bugs:
- First, browsers differ in exactly how they generate selection endpoints for the actions above:
  - Chrome always generates an element endpoint for the selection focus, which points to an element preceding the next editable text location, so Slate generates a hanging selection.
  - Safari behaves like Chrome, except when there is an image before the next editable location; then it generates a text endpoint in the original paragraph (so Slate generates a non-hanging selection).
  - I feel like these differences are not really a problem—applications should do something sensible with both hanging and non-hanging selections; so inconsistencies in when hanging / non-hanging selections are generated don't really matter. Just my opinion!
- Second, applications don't always handle hanging selections correctly:
  - I've been working on a branch that addresses these bugs by always looking for the text endpoint inside the DOM selection, never outside. 
  - This works without browser-specific fixups, but it also gets rid of hanging selections (as above I think this is a mistake). 

## [What is the purpose of onDOMBeforeInput?](https://github.com/ianstormtaylor/slate/issues/3302)

- It's an event handler for the native DOM `beforeinput` event, because sadly React's synthetic events don't properly expose it. 
  - In this case it's listening for specific inputTypes that browsers fire for context menus, etc.

## [onDocumentChange and onSelectionChange](https://github.com/ianstormtaylor/slate/issues/4687)

- Currently the onChange event of slate is fired for changes on the document structure but also for changes on the selection. 
- you can distinguish in the onChange event like:
  - `if (editor.operations.every(op => op.type === "set_selection"))`

## [Why is content pasted as plain text?](https://docs.slatejs.org/general/faq)

- One of Slate's core principles is that, unlike most other editors, it does not prescribe a specific "schema" to the content you are editing.
  - For the most part, this leads to increased flexibility without many downsides, but there are certain cases where you have to do a bit more work. Pasting is one of those cases.
  - Since Slate knows nothing about your domain, it can't know how to parse pasted HTML content (or other content). So, by default whenever a user pastes content into a Slate editor, it will parse it as plain text. 
  - If you want it to be smarter about pasted content, you need to override the insert_data command and deserialize the `DataTransfer` object's `text/html` data as you wish.

## [onKeyDown not fired for editable elements nested inside non-editables](https://github.com/ianstormtaylor/slate/issues/468)

- [Keydown event on contenteditable div and child span](https://stackoverflow.com/questions/22895124)
  - I have a contenteditable div containing a span and would like to trace the keydown events when typing in both the div itself and the span within the div.
  - Everything seems to work fine so far in firefox but in webkit browsers the div keydown event seems to override the span event. 
- it seems to happen because it is the div element that catches the keydown events, not the inner span elements. To make them catch the keydown events, you would need to set contenteditable=true for each of them while setting contenteditable=false for the div container.
  - To make both the div container AND the inner span catch the keydown events, you can wrap your span in a non-editable span

- [Focusing on nested contenteditable element](https://stackoverflow.com/questions/40907091)
  - I have two contenteditable divs nested inside of another. When it is focused, nested should be focused but using console.log(document.activeElement); it shows that the top is focused and it doesn't recognize the nested div.
- 💡 The way [contenteditable] elements are handled by browser made **any nested [contenteditable] not handling any event, the editing host is the former editable parent**. See spec:
  - If an element is editable and its parent element is not, or if an element is editable and it has no parent element, then the element is an editing host. 
  - Editable elements can be nested. User agents must make editing hosts focusable (which typically means they enter the tab order). An editing host can contain non-editable sections, these are handled as described below. An editing host can contain non-editable sections that contain further editing hosts.
- Now as a workaround, you could make focused nested editable element the hosting host by setting any of its editable parent temporarily not editable
- Give `tabindex=-1` to the nested div, than can be focused
  - 👀 `contenteditable` is inherited, so there is no need to specify it again.
  - it only works with mouse focus. Moving the caret (cursor left/right) over the nested div, will not focus the nested div. Similarly, leaving a focused nested div with the caret, will not does not give the focus back to the parent div. Handling might need workarounds with keydown listener, range and selection.
