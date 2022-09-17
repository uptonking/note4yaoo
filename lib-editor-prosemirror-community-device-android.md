---
title: lib-editor-prosemirror-community-device-android
tags: [android, community, mobile, prosemirror]
created: 2022-08-30T18:17:24.603Z
modified: 2022-09-17T10:08:12.410Z
---

# lib-editor-prosemirror-community-device-android

# guide

# discuss-stars
- ## Contenteditable on Android is the Absolute Worst_202106
- https://discuss.prosemirror.net/t/contenteditable-on-android-is-the-absolute-worst/3810
- Our understanding based on digging into Android apps and staring at tons of logs is that the Android IME views the contenteditable block as one long plain text string. 
  - This is troubling when you have lots of HTML that you are editing as the IME may view your content very differently than how the user perceives it.
- ProseMirror has a lot of functionality to handle compositions/IMEs and has to walk a fine line between control and not interfering with native behavior. 
  - For one, it has to protect composition text nodes, while at the same time being willing to sync new changes from state updates. 
  - ProseMirror uses composition event handlers internally to help with composition issues and the various event types correspond to a composition lifecycle (compositionstart, compositionupdate, compositionend).
- We use input events all of the time to help workaround bugs as they provide crucial hints as to what the browser is trying to do.
- One important note is that Android has many types of keyboards with the most popular being GBoard.
  - These keyboards have their own unique quirks and bugs and unless you get native help via a mobile app, you can’t tell which type of keyboard is active.
- cursor parking
  - the short version is that we move the selection (and sometimes focus) out of the ProseMirror into a temporary input, let the browser trash that input as they see fit, then move the selection back.

- ### Issue 1: Lack of keydown keys
- This is one of the biggest and most annoying issues that we’ve ever had to deal with. 
  - The crux of the issue is that Android normally does not tell you which key is pressed on keypress events (keydown, keyup, etc.). 
- This means that most of your custom bindings will not work most of the time. 
  - This is especially annoying when you have custom backspace handling (like selecting a node first before deleting on backspace).
- ProseMirror has some workarounds internally to help with this by detect the changes in the mutation and looking to see if the mutation looks like a backspace or enter, but it doesn’t work 100% of the time.
- We can mostly detect if a backspace/delete is happening using a beforeinput event and looking for an inputType of either deleteContentBackward or deleteContentForward. We then fire a synthetic keydown that is either a Backspace or a Delete key (respectively) and use someProp(‘handleKeyDown’)
-  If the event is “handled” (if a handleKeyDown prop function returns true), then things get interesting.
   - According to the spec on beforeinput events, beforeinput is supposed to be cancelable for most inputTypes
   - Unfortunately, browsers often don’t care enough about the spec so we have to prevent the default behavior using a combination of cursor parking and suppressing selection updates. 

- ### Issue 2: The cursor wrapper
- The cursor wrapper has a few uses but one of the primary use cases is to take stored marks and make sure composition text is styled correctly. 
  - ProseMirror internally calls this use case “mark cursor.” 
  - This works because ProseMirror inserts a cursor wrapper decoration into the dom in the form an image element with no src and then selects that image element when the composition starts. 
  - The browser then overwrites that image element and keeps the styles. 
- However, this mark cursor can cause a few problems with the Android IME.
- One is that if it’s removed at just the right time, then the selection may end up jumping a single character. 
- Another issue is when you split inclusive marks. 
  - The mark cursor decoration is added to the middle and when issue 3 occurs (see next), Android loses track of where to re-insert the composition text. 
  - Update: This is actually a general Android contenteditable issue, it isn’t specific to ProseMirror and the cursor wrapper
- One last issue is that if you are tracking input states yourself in plugin state, you can unintentionally remove the cursor wrapper at the wrong time. 
  - We got around this by overwriting the view getter for the cursor wrapper and checking for meta only transaction. 
  - If the transaction was only a meta transaction, then we would lock the cursor wrapper for the next state update.

- ### Issue 3: The composition text node swap
- When performing custom mutations (like a custom enter handling when splitting a paragraph), Android has this really strange behavior where it seems to want to swap out text notes with a composition text node. 
- I think some ProseMirror internals may have problems with this text node swap because selectionchange events are asynchronous
- we don’t have a great workaround for this and I think the cursor jumping would need to be fixed inside of ProseMirror by syncing the selection during the deleteContentBackward beforeinput event. 
- we may want to hold off on flushing the mutations until Android finished everything.

- ### Issue 4: Android Chrome is afraid of unselectable atoms
- What Android often does is that when you backspace onto that atom/unselectable node, Android will just give up and dismiss the keyboard. 
- We have also used some CSS class trickery to force user-select: all on unselectable items when your cursor is getting close to unselectable atoms.
- For the NodeSelection issue, we have gotten around this using cursor parking.

- ### Issue 5: Input bugs are unique across different webview versions, keyboards, keyboard versions, types of devices, and OS versions.
- there are still some nasty and stupid bugs that come up that are specific to a combination of certain webview versions on specific devices with specific keyboards. 
- We are actually using our native app to tell our editor which keyboard types (e.g. Gboard, Samsung, LG, etc.) are enabled at any given time so we can have workarounds for specific keyboards if absolutely necessary. 
- Many of our fixes in these scenarios end up using cursor parking but this is still an area where we are all bound to have blind spots.

- ### Where to go next?
- Honestly unless there are serious efforts on the Chrome front to improve contenteditable on Chrome Android and how the IME views contenteditable, there isn’t much we can do fundamentally that ProseMirror isn’t already doing. 
- I’m sure there are a few additional fixes that could be made but issues like the mark cursor seem to be unfixable without breaking the mark cursor feature at least some of the time.
- 💡 The best approach may be to just have less functionality on mobile, especially around key handling and advanced node views, but I’d love to hear what others think

- It should also be noted that Mobile Safari on iOS isn’t much better here. 
  - It doesn’t use composition for most languages, so many users don’t run into the bizarre things it does during composition, 
  - but Chinese or Japanese users run into about as many bugs on that platform as on Chrome Android.

- /// discussion

- `beforeinput` events weren’t really supported yet at the time of the initial implementation of ProseMirror — it is possible that we could be leaning more onto that (but as you mentioned, it’s not ideal).
- It should also be noted that Mobile Safari on iOS isn’t much better here. 
  - It doesn’t use composition for most languages, so many users don’t run into the bizarre things it does during composition, but Chinese or Japanese users run into about as many bugs on that platform as on Chrome Android.
- Yea I was thinking of writing a sequel to this about iOS as it’s almost just as bad. However, the lack of keydown keys made Android take the cake for me.
- The only proposals I would have for ProseMirror (and I can file tickets and potential PRs for this if you agree) are
  - Not to remove the cursor wrapper if the state update is not changing the doc or selection. However, this problem may just be unique to us and we already have a workaround so maybe we can just ignore it.
  - The enter jumping bug that seems to be due to the text node swap (Issue #3)
  - Experiments with new mark cursor workarounds to prevent issues where inclusive marks get split
- I think the most pressing issue is a generalized fix for issue #3 and I think it’s due to the selection being out of sync with ProseMirror on `deleteContentBackward`.

- Just to be clear, if you use an actual hardware keyboard, then Android behaves much more similarly to Chrome on desktop and compositions are not the default unless you are using a composition based language (Chinese, Japanese, etc.). 
  - You could try this on mobile by hooking up a bluetooth keyboard and looking at the keyboard event viewer. It’s only when you type with an onscreen keyboard where compositions and a lack of key events happen. 
  - If you were using the emulator with 12L, it’s possible that it pretended as if you were typing with a hardware keyboard and not an onscreen keyboard (considering 12L is for larger devices).
# discuss
- ## 

- ## 

- ## 
