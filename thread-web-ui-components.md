---
title: thread-web-ui-components
tags: [components, thread, ui, web]
created: '2021-01-19T04:45:46.454Z'
modified: '2021-01-19T04:46:23.100Z'
---

# thread-web-ui-components

# guide

- [UI Components Handbook](https://www.uiguideline.com/components)
  - 可搜索各种组件，但部分组件需要付费才能查看详细内容
  - 列出了主流设计系统的组件，进行对比
  - https://www.uiguideline.com/reference-systems

- This is the biggest opportunity for new component libraries and design systems to differentiate: make mobile web a priority.
- https://twitter.com/rauchg/status/1406341624704102402
- The ideal approach is to use a platform-agnostic API like React Native (Web), which treats mobile as a first-class citizen. Design for screen size, not platform.
- Do you think Next would ever investigate pulling down different pages based on screen size? e.g. pages/pricing.sm.js
  - Yes, we are thinking about introducing something that would help with this pattern. 
  - I think fundamentally sometimes the page for a mobile and desktop site are quite divergent and deserve different entrypoints.
# discuss
- ## 

- ## 

- ## highlighted-code is a textarea builtin extend that's embarrassing how simple, a11y compliant, versatile and lightweight is, compared to most competitors
- https://twitter.com/WebReflection/status/1507814171211087875
  - it's literally a textarea that shows highlighted code, usable in forms too
  - https://github.com/WebReflection/highlighted-code
  - https://webreflection.github.io/highlighted-code/test/demo.html

- ## Do I understand correctly that "Custom Elements" (JavaScript classes extending HTMLElement) can not take constructor arguments and _have_ to be initialized in the god-awful imperative DOM way of setting attributes/properties one by one?
- https://twitter.com/MarijnJH/status/1428678081255022593
- If it’s useful, Object.assign(elements, attributes) can set multiple attributes at once.

- ## I wrote about my favorite HTML element `<dl>` . dl>dt/dd 注意dd会缩进
- https://twitter.com/BenDMyers/status/1423708549750956037
- Another benefit is the default styling in browsers.
- It is nice but its screen reader support is quite patchy compared to ul
- I know @thatrandybrown has used <dl> as his markup to debug objects' properties.

- ## TIL React-Native's Text comp does a bit too much and has a perf overhead 
- https://twitter.com/sebastienlorber/status/1419723047637037061
  - @wcandillon found out you could simplify it (ie just render text, no press etc...) and improve perfs
- it means removing features to only what you really need
- I wonder if a wrapper component could solve it magically 

```JS
if (type of props.children === string && noOtherExpensiveProps) {
  return <SlimText />
}
```

- ## Working on Excalidraw and Excalidraw+ we've been doing lots of modals. 
- https://twitter.com/dluzar/status/1418259104938795017
  - I thought I'd share some of the points from my experience.
- Let's start with accessibility: focus traps. 
  - Pressing Tab should never take you out of the modal. 
  - Instead, you should cycle back to the first focusable element.
  - (And make sure upon opening the modal you focus the first actionable element, usually the first input field.)
  - You can do this by listening on `keydown` , querying all focusable elements (inputs, buttons...) from the modal's root element, and manually focusing either the first or last element based on whether user pressed `shift` or not.
- Clicking outside the modal should close it, same as when pressing `escape` .
- What if the user just filled out the form and clicked away by mistake? Losing progress is annoying, so let's prevent that.
  - When the form is dirty, clicking outside (or Escape) won't close, and require you to explicitly hit `close` or `submit` button.
  - you can show the submit button only on a dirty form. This will give additional visual feedback.
- As a bonus, we can make pressing `escape` focus the close button as a courtesy to the user.
- Whenever your list exceeds a given number of items, you should provide a way to filter them for quick access.
  - Bonus points for adding a button to clear the filter for mobile users.
  - And you can set `min-height` to the list so that filtering doesn't result in layout shift.
- In large, scrollable modals, it's a good idea to make the header and the footer sticky so that the context and modal buttons are always visible.
- But how to deal with browser's back button ? Should it close the modal or go to previous page ? (Even more complex wizard steps inside modals)
  - I don't usually add modals to url
  - What I'm doing above is removing the modal url from history if we close it via UI, so we never get history like `page → modal → page → modal...`

- I don't think this is good UX, users shouldn't be constrained in any way. For me a better solution would be to persist the entries of the form.
  - I'm a big fan of keeping the state around and restoring later, but I don't think that applies to modals.
  - In this case we must ensure the user knows whether the operation was submitted or not.
- 

- ## Pouring over the details of other designers and doing some layout studies today. Grid is everything
- https://twitter.com/souporserious/status/1416884764691161089

- ## Forms tip!
- https://twitter.com/stackblitz/status/1412414470681415682
- Checkbox can be indeterminate, but you have to set that( `inputEl.intdeterminate = true` ) with JavaScript.
- `autocomplete="one-time-code"` can help users auto-fill the auth code they've just received - they won't need to copy it from the SMS by hand!
  - one-time-code requires an OS-level integration (eg works on Safari+Mac, but won't on Android)
- The `<fieldset>` element – used for grouping relevant inputs & buttons – allows you to provide the `disabled` attribute if you want to disable these enclosed controls all at once.
- Use `<datalist>` to enhance your forms with suggested values – not only for text inputs, but also numbers, ranges, emails, and even colors!
- You *can* customize these native html validation messages that browsers display. Just use the `setCustomValidity` method! Super useful for working with pattern validation, or even just to say "Name is required"
- Use the built-in `.validationMessage` property that allows you to get a native validation message (in your user's locale!), and display it in the UI the way you like it.
- Working with date inputs use the `valueAsDate` property so you don't have to manually convert between "YYYY-MM-DD" string and a `Date` object.
  - Useful for both getting, and settings the value!

- ## What is the correct way to include a blank line
- https://stackoverflow.com/questions/35315023
- I use a `<hr>` because is the semantic tag to represent that kind of break.
  - `<hr style="height:16px; border:none; " />` .
- `<br />` 设置height没有效果，除非强行修改display
  - 连续用2个 `<br />` 就有一个空行的效果了，但高度依旧是默认的，不如 `<hr />` 灵活

- ## Popover components in a Dark, Black and Light UI theme
- https://twitter.com/getdona/status/1390229858266062850

- ## does anyone have any knowledge around performance characteristics of "box" components? 
- https://twitter.com/itsmadou/status/1390120303343276033
  - considering the number of styles that could be applied (conditionally!) 
  - i'm curious if the before/after story affects performance if used at scale.
- Box components is too small to create an issue, but when you get more of those little bustards...
  - You will end with WAY more HTML elements than you ever wanted to have.
  - Boxes are good for DX, bad for users.
- The styles don't matter but having 2x the no of components actually makes React rendering (much?) slower. I don't remember where I have this test but try rendering 10000 divs as divs vs as a `<Box />` — back when I tried it was 2-4x slower
  - I had similar experience. For me swapping styles-components with just classes didn’t help much for the same tree. Reducing the depth is what helped. But it’s hard to do without breaking abstractions.
  - Had a bunch of styled components in a table, we were wondering why performance is so bad, tried changing and upgrading the table until we realised it was those little fuckers inside the cells making the overhead. Swapped with static and it's been great!

- ## Design System opinion: Don't make your `<Link>` and `<Button>` components support both link and button visuals 
- https://twitter.com/buildsghost/status/1389294014222934018
  - Do make your `<Link>` and `<Button>` components renders either `<a>` or `<button>` based on the props passed to it ("to" should render an anchor, "onClick" should render a button)
- When I tried that some years ago it was really hard to express the interface _properly_ in TypeScript. How about going one step further and call it `<Action/>` and forbid `<Link/>` and `<Button/>` components?
  - type BaseLinkProps = { to: string } 
  - type BaseButtonProps = { onClick(): void } 
  - type BaseLinkOrButtonProps = | BaseLinkProps | BaseButtonProps 
  - type ButtonProps = BaseLinkOrButtonProps & { other: boolean }
- From a HATEOAS/hypertext point of view, a link is a perfectly fine tag to use even for a button, as long as it has a href and expects the agent to follow the link to the new page. `<button>` is for submitting forms.
  - I don’t know what HATEOAS is but WAI-ARIA’s authoring practices don’t agree
  - HATEOAS/hypertext is the semantic underpinning of the web.
  - I realize my previous tweet as a bit vague, but I'm arguing for `<a>` for links, `<button>` for 'submitting forms', and to *not* use a `<button>` for navigating to another page
  - There are plots of use cases for buttons besides submitting forms. Ex: Showing/hiding a menu

- ##  `accent-color` will enable us to have style-matching checkboxes and radios.
- https://twitter.com/stefanjudis/status/1385294684977868802
  - https://codepen.io/stefanjudis/pen/abpPvYQ

- ## One step closer to moving away from abuse of history.pushState() to get back-button-closable sidebars and dialogs!
- https://twitter.com/domenic/status/1339675541083971586
- ModalCloseWatcher code, including Android back button support, is in Chrome Canary behind a flag! 
- All the excitement and engagement on appHistory has been really great. 
  - But I worry that if we don't solve the "Android back button" close signal problem, developers will be forced to abuse appHistory like they currently abuse window.history. Let's make sure both of these succeed!
- This is great. Modals are full of workarounds right now. Another related area I think you should consider are APIs to help restrict focus within a modal
- [Some ideas for to improve history state on the web](https://github.com/slightlyoff/history_api)

- ## You know the "segmented control" UI pattern used as an alternative to radio buttons? 
- https://twitter.com/fvsch/status/1380420535373475840
  - Designers always design it with 3 items, so you can see which one is selected by comparing with the other 2.
  - But when there are two items only, it breaks down. Which is selected here?
- I think adding an inset to the selected option helps

- ## You can use the `details` element to create native HTML accordion.
- https://twitter.com/denicmarko/status/1348523949014065153
- Only problem, so you've got to control your according(grouped), closed the previous on open of next
- Since there's no toggling of classes or pseudo-classes, you can't use CSS to add transitions to `<details>` .
  - `<details>` has one "toggle" event, but that's fired after the state change. 

- ## By nesting a `<dialog open>` inside a `<details>` you can create an infobox using only #CSS.
- https://twitter.com/bramus/status/1374090556566089738
  - https://codepen.io/bramus/pen/KKaPJdr
  - You might not want to use this "in production" though, as is most definitely has #compat, #a11y and #ux issues.
- That's clever and it's seems to work fine on iOs using VoiceOver!

- ##  If you have form fields where trailing/leading spaces don't matter, just trim the value instead of failing
- https://twitter.com/tomayac/status/1361972883468279808
- `HTMLInputElement.value.trim()` .
- interestingly regular text input fields are left as-is, whereas email input fields get trimmed: both name and email had a leading and a trailing space
- That's a bug, as spec says to trim
  - The value sanitization algorithm is as follows: Strip newlines from the value, then strip leading and trailing ASCII whitespace from the value.

- ## Thinking on ways to build Settings UI: layout, color, animation, a11y
- https://twitter.com/ChromiumDev/status/1372593649486233601
  - https://github.com/argyleink/gui-challenges/tree/main/settings
- There's the uncanny(异常的) valley of the grid gap being not clickable
  - It can be fixed too by not using `display: contents` .
- GUI Challenges are now built with Vite, I'm a huge fan. 
- Why have you chosen to rely on pseudo-element inside the `<input>` (checkbox example)? 
  - This doesn't work consistently across the browsers. For instance, this won't work in Firefox as of today.
  - Great write-up, nicely done as always. What bothers me a bit is the use of `<h3>` inside the `<label>` . As far as I know, `<label>` accepts only `Phrasing content` , and `<h3>` is a `Flow content` .
  - And by the way, the same goes for the `<small>` element. It's also a `Flow content`

- ## One of the common mistakes while building a UI is forgetting to add padding for long text elements.
- https://twitter.com/shadeed9/status/1371043578227650562
  - Make sure to have a good variety of text lengths while testing.
- [Handling Short And Long Content In CSS](https://ishadeed.com/article/css-short-long-content/)
- Long Content
  - overflow-wrap: break-word; 
  - hyphens: auto; 
  - text-overflow: ellipsis; 
  - -webkit-line-clamp: 3; 
  - Sometimes, it’s not always practical to break or hyphenate a word, allowing horizontal scrolling will make the reading experience better.
  - you might forget to add padding until you notice a visual issue. 
- Short Content
  - min-width
- Use cases and examples
  - Profile card
  - Navigation items
  - Article content
  - Shopping cart
  - Flexbox and long content

- ## Design systems folks, what would you call this component? 
- https://twitter.com/_alanbsmith/status/1370089747926851586
  - block of highlighted/accented text
  - inline with the rest of content (not floating)
  - might or might not be dismissable
  - usually offers details, notes, or additional info

- Notion refers to it as a "callout", which I think works well.
- I'd consider that a styled blockquote 
- callout card (polaris)
  - section message (atlastkit)
  - also seen - aside, inline-banner
- We've called them both Banners and Alerts, but Callout feels more natural
- Callout, Note or HighlightedNote?
- We call them “note”, sometimes called “annotation” or “alert”
- On the Luna design system at Northwestern Mutual, we call it an "Inline Notification"

- ## The most common layout found across my stylesheets: a gapped stack.
- https://twitter.com/argyleink/status/1369632881857990658
  - `display: grid; gap: var(--space-whatever);` .
- I think it’s actually my main use for grid… cannot wait for it to see wide support for flexbox gap!
  - https://caniuse.com/flexbox-gap
- I’ve done this in our WP theme then have been removing it from main containers because Google’s responsive ads don’t play nice and cause horizontal scroll on mobile.
- If we had margin-trim we could use all CSS layout properties and not just flex and grid.

- ## I've spent more time on this comparison table than I'm willing to admit.
- https://twitter.com/meijer_s/status/1368617079457386499
  - It's also honestly workable on mobile. Something many feature comparison tables lack. 

- ## Leva 0.5.1 introduces two little features: `hint` allows you to show a tooltip when hovering input labels, and `optional` lets you to toggle an input, setting its value to `undefined` when disabled.
- https://twitter.com/davidbismut/status/1368660111049302018
- tooltip uses @radix_ui under the hood

- ## The things we've seen built with @framer this year have already been so awesome. Smart Components are really bringing product design to the next level.
- https://twitter.com/AddisonSchultz/status/1367067007678578688
- Been playing around with the Variants & Variables Beta in @framer. 
  - Here’s a movie library UI with hover variants & simple overlays. It’s crazy how easy and fast it is to prototype this. 
- Variables really make components crazy customizable

- ## Anyone written about ways they work with design token in dark/light mode?
- https://twitter.com/SamKap/status/1367299104779489280
- [Building better products with a design token pipeline](https://uxdesign.cc/building-better-products-with-the-design-token-pipeline-faa86aa068e8)
- Here's a write-up of the color system from a DS I used to work on:
  - We had all the color schemes set up in Style Dictionary and exported them as SASS maps. 
  - In SASS we could then generate color scheme CSS classes 
  - and doing dark mode was done there by picking 2 color schemes (one for light and one for dark) and putting them behind the appropriate media query.
  - https://github.com/buildit/gravity-particles/tree/develop/src/tokens/color-schemes
- By design token do you mean the css prefers-color-scheme attribute?

- ## I feel every data fetch on application have this 5 different UI states: Initial, Fetching (Loading), Error, Empty and Result.
- https://twitter.com/renatorib_/status/1366481747882504194
  - Sometimes Refetching !== Fetching
  - And I feel that the right thing to do is somehow abstract/standardize this UI handling
  - It's about UI abstraction, not state itself.
- Also, data may be changed (localy), outdated (server has a new version), invalid (server rollback your version). Error may be intended (validation) or not (network fail).
  - Many reasons cause many options. We should generalize and name it, to be ready for each of them.
- For React, react-query or swr solve this beautifully

- ## Do you have any favorite designs of step-by-step UIs like on this screenshot?
- https://twitter.com/dan_abramov/status/1365723330825887750
  - I’m looking for examples where:
  - There are individual stops
  - There are descriptions of changes between them
  - Bonus points if it’s interactive in some way (e.g. you can click or hover an item and that does something).
- Good old wizard. It can be extended and used to solve complex UI flow
- [Step by step navigation](https://design-system.service.gov.uk/patterns/step-by-step-navigation/)

- ## Spacer component is a one-way ticket for handling CSS margins, there's simply no going back.
- https://twitter.com/bernam92/status/1365322784004571139
  - It's WAY faster than giving top/bottom margins to elements that don't belong in them!
  - Debug mode? Add background-color and :before content to visualize your spacings!
- Hmm doesn't it make the html too bloated and hard to read like it used to be when we used to use HoC in react?
  - This is the only downside of this approach, which I feel... ignorable?

- ## https://github.com/seek-oss/capsize
  - Capsize makes the sizing and layout of text as predictable as every other element on the screen.
  - Using font metadata, text can now be sized according to the height of its capital letters while trimming the space above capital letters and below the baseline.

- ## Do you guys still use 12-column grid system?
- https://twitter.com/renatorib_/status/1361688536500629507
  - Because of flexbox/cssgrid, I haven't used it in a while. 
  - But we are considering using it to create a better consistency with UI.
- With the gap property in CSS grid, it’s been a really long time since I used columns. What kind of inconsistencies do you see in your UI that you’d need a 12-column grid system to fix?
  - The auto-sizing in Grid is fantastic, but we give up some control by letting the browser make decisions for us. 
  - If that’s a no-go, columns could still make sense.

- ## Pulling Braid's layout components out to a standalone library, I had to switch to an array for configuring breakpoints
- https://twitter.com/markdalgleish/status/1361551281190412289
  - so TypeScript can extract the names of the first and last breakpoints—something I couldn't do when breakpoints are defined with an object.
- You can do something like this, but yeah, an array is probably the best solution

```JS
{
  one: "one",
  two: "two",
  get first() {
    return this.one;
  }
  get last() {
    return this.two;
  }
}
```

- ## Trying to build an accessible interactive tooltip in a React portal—the trick is simulating natural tab order
- https://twitter.com/markdalgleish/status/1356534519776432129
  - e.g. tabbing out of it should take you to the next focusable element on the page. 
  - There's no browser API for this, but luckily I found focus-trap/tabbable
- https://github.com/focus-trap/tabbable
  - Find descendants of a DOM node that are in the tab order
  - If you think a node should be included in your array of tabbables but it's not, all you need to do is add tabindex="0" to deliberately include it.(-1 to exclude it)

- ## Thinking on ways to solve a SIDENAV
- https://twitter.com/argyleink/status/1352343431914299393
  - No position absolute anywhere, and the JS is only ux enhancements
- [Building a sidenav component](https://web.dev/building-a-sidenav-component/)
  - how I prototyped a Sidenav component for the web that is responsive, stateful, supports keyboard navigation, works with and without Javascript, and works across browsers. 
  - Try the [demo](https://gui-challenges.web.app/sidenav/dist/).

- ## Intent to Prototype: HTMLPopupElement - <popup>
- https://twitter.com/intenttoship/status/1352410513876119554
- https://groups.google.com/a/chromium.org/g/blink-dev/c/9y-Thg9UCxY/m/_4gShWjQAAAJ?pli=1
- [Enabling Popups](https://github.com/MicrosoftEdge/MSEdgeExplainers/blob/main/Popup/explainer.md)

- ## I've been experimenting a lot with "pure CSS theming" and composition with CSS variables
- https://twitter.com/MaximeHeckel/status/1352289351024181250
- One of the cool things I did [here](https://twitter.com/MaximeHeckel/status/1343589258859319298) was to base this system solely on CSS variables: bye-bye ThemeProvider!

- ## High compatability and longevity pattern libraries shouldn’t include JavaScript, just document the states JavaScript can affect. 
- https://twitter.com/heydonworks/status/1351478317183074304
  - Document the toggle button pressed and unpressed, and what HTML/CSS these states need.
- I’ve been a big fan of this for large orgs.
  - It's (kinda) what I did with my last client (my bad jQuery with a big - "write your own JS" caveat) and with my current client where we’re trying to show/document those things rather than code examples up.
  - This is what happened with one design pattern from a previous clients design system that had (essentially) an HTML, CSS and minimal Javascript based component library
  - when you have the coded components of your design system written in HTML, CSS, and (vanilla) JavaScript it lets your pattern filter into products that use: asp, php, ruby on rails, angular, vue
- I (gut reaction!) strongly disagree with this, especially as more and more CSS features arrive with accompanying JS APIs.
  - I have no idea if React will be more or less prevalent in 10 years, but I definitely think many declarative UI patterns from it will.
  - The costs of describing complex patterns and states with them decoupled from JS seem too high to me?
  - It feels like an ends justify the means approach—implementation doesn’t matter, just the result. 
  - I’m biased as I work primarily with a DS built in React.
  - I’ve wanted to extract everything generic from it for a long time, to find what is expressed such that it can also be expressed as just HTML/CSS and what cannot. But it’s a staggering undertaking.
  - Personally, I think front end would benefit immensely from standardizing how we do UI in JS more, and that’s where most of the chaos/confusion comes from, rather than promoting even greater agnosticism.
- Cannot agree more. Too often is a pattern lib of high quality but intertwined to a JS lib that could change within months.
- I've been pondering this myself as I build our design system. 
  - My inclination was the same but then I had to build a JS templated modal gallery and it made sense to me to include the JS. 
  - As the audience is PHP CMS developers I couldn't expect them to do the JS. Not ideal but...
- Hard agree, each time the patterns are implemented as components in a framework that can be shared for reuse, but you the look & feel shouldn't be tightly coupled to the scripts

- ## I like to make my design systems two tiered. 
- https://twitter.com/stubbornella/status/1351600378849103874
  - Tier 1: html and CSS only. 
  - Tier 2: HTML, CSS, and JS flavor. 
  - Teams can choose 1 and get flexibility with more breaking changes. 
  - Or 2, and get more guardrails and fewer breaking changes. Both are valid.
- Cool! Presumably, for (2), you take the extant HTML+CSS stuff and compile it with a separate JS repo or something?
- @neal4d did a talk about "Trap Doors" in architecture/designs a while back, IIRC, too, so maybe I either channeled him or adapted it. 
  - His slides/videos might be on the Interwebs somewhere, too.

- ## With so many website designs being updated to feature large border radiuses, I'm finding them much more well rounded.
- https://twitter.com/markdalgleish/status/1351642575908732928
- We really have come full border-radius: 50% back to the trends of "web 2.0"

- ## Lots of designers try to avoid modals, but I don't think they should be so quick to dismiss them.
- https://twitter.com/markdalgleish/status/1351300138233282561
- Implementation wise, you often want the URL to represent the UI State. 
  - If the user refreshes the page, or accidentally closes the browser, or duplicates the tab, or shares the URL to another computer, when that URL finishes loading, the state of the UI should be identical.
  - You end up needing to either:
  1. totally break the contract of URL with UI State
  2. invent your own bespoke convention for representing Modal state consistently on the URL for each URL path.
  - Every app will end up implementing #2 a little differently
  - just the open/close state. 
  - if the modal is a form, it'd be a bit much to shove the form into the URL -- that sort of data instead goes in local storage if at all.
  - Nested modals make this even more complex/stupid.
- Idea: an app where every new page is a modal stacked on top of one another so users have ~ u l t i m a t e   c o n t e x t ~
- It's just really hard to dialog with them.
- So true. When discussing usage of modals with the rest of team it’s important to keep an open dialog
- They have good reason to! 
  - Modals are not inherently bad but in many cases they end disrupting the user flow and limiting the user experience.
  - They have been used for bad more than for good, that's for sure. 
  - Exit modals when the user heads for the back button, are some of the worst UX yet stats show they work.
- You’re gonna have to try harder if you are to keep my focus.
  - I guess it's tough to stay on top of things and maintain focus.
