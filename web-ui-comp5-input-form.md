---
title: web-ui-comp5-input-form
tags: [components, form, ui, web]
created: 2021-04-23T15:20:03.201Z
modified: 2021-07-28T20:11:24.350Z
---

# web-ui-comp5-input-form

> 数据输入类组件，表单组件

# guide
- form设计
  - form提交后，若请求处理失败，应该保持旧的输入记录方便用户直接修改，而不是展示空白form让用户重新输入
# switch

## [Switch Pattern | APG | WAI | W3C](https://www.w3.org/WAI/ARIA/apg/patterns/switch/)

- switches can only be used for binary input while checkboxes and toggle buttons allow implementations the option of supporting a third middle state. 

- it is critical the label on a switch does not change when its state changes.

- If the switch element is an HTML `input[type="checkbox"]`, it uses the HTML `checked` attribute instead of the `aria-checked` property.

- ## [Building a switch component](https://web.dev/building-a-switch-component/)
- This demo uses `<input type="checkbox" role="switch">` for the majority of its functionality, which has the advantage of not needing CSS or JavaScript to be fully functional and accessible.

- https://github.com/argyleink/gui-challenges/blob/main/switch/style.css

- ## [Build an accessible Switch Component with React and Typescript.](https://levelup.gitconnected.com/build-an-accessible-switch-component-with-react-and-typescript-d455a405aaa)
- HTML unfortunately does not support native switch elements. 
  - We can opt for a simple `<input type="checkbox" role="switch" />`, remove all default browser styles using the CSS declaration `appearance: none;` and apply our own custom styles

- ## [The good, the bad and the toggle.](https://uxdesign.cc/the-good-the-bad-and-the-toggle-2abc0fbbd099)
- Do not use toggles in forms. Use checkboxes or radio buttons instead.
- Do not use toggles in filters or multiple selections of elements.
- Use toggles for settings and changes that have an immediate effect on the UI (same applies for the segmented control).
- Avoid mixing toggle button groups and segmented controls.
- Avoid using switches with multiple options.

- ### [Checkbox or switch?](https://bootcamp.uxdesign.cc/checkbox-or-switch-97dd932b01c0)
- If the actions rely on each other, for instance, choosing one will choose the others as well, then use checkbox
- Switch takes more space, and this big space provides more design possibilities.
- There are gaps between guidelines and actual practices

- ### [checkboxes - Checkbox vs toggle](https://ux.stackexchange.com/questions/63884/checkbox-vs-toggle)
# discuss-form-solutions
- ## 

- ## 

- ## 

- ## 

- ## 🆚 React Hook Form, TanStack Form, or Formisch — which one should you actually pick in 2026?
- https://x.com/FabianHiller/status/2042251006612844819
  - We compared all three across TypeScript inference, validation architecture, and performance as forms grow
  - [Choosing a React Form Library in 2026: React Hook Form, TanStack Form, and Formisch Compared | Formisch _202604](https://formisch.dev/blog/react-form-library-comparison/)
- RHF attaches validation rules at the point of field registration. Alternatively, you can pass a schema resolver at the form level using Zod, Valibot, Yup, or similar. Either way, the mental model is field-centric. Each field is responsible for its own validation, and the form is an aggregation of those field-level concerns.
  - RHF's core design decision is that field values do not live in React state. They live in RHF's internal object. RHF updates the native HTML input directly through refs, bypassing React's re-render system entirely. 
  - This is what makes RHF fast. It is a deliberate architectural choice.
  - In small forms, this is not a problem, but in larger forms with many watched fields, the re-render problem returns, but scoped to the components subscribed to those fields.
- The most significant architectural change in TanStack Form is that validators are first-class objects. Each validator you define specifies its own trigger: onChange, onBlur, onSubmit, or onMount and these triggers are independent of each other. Async validation is also treated as a first-class concern. Form-level validators are also part of the core design. These validators run against the entire form state and can assign errors to specific fields.
  - TanStack Form stores field values in a reactive store, and components subscribe only to the specific slice of state they use. When a field changes, only components subscribed to that field update.
  - TanStack Form's store-based reactivity manages re-render scope automatically, so performance remains stable as forms grow without additional architectural work.
- Formisch centralizes everything in the Valibot schema. Validation runs when the form is submitted by default, rather than on individual field events like onChange, giving users silent-until-submit behaviour on first interaction, then live feedback as they correct mistakes. 
  - Formisch uses signals as its reactive model internally
  - A signal represents a single value and tracks exactly which components depend on it. When a signal changes, only those components update, allowing updates to be scoped very precisely with minimal overhead compared to store-based approaches.
  - The dependency graph is more direct than a store-based model. 

- For most applications, the difference between TanStack Form and Formisch comes down to this: both scope re-renders automatically without requiring deliberate component structure. Formisch does it at the signal level, which can reduce overhead as form size and update frequency increase.

- Tanstack Form hands down. When they implement multi step functionality then i wont even consider other options

- Great framing. Form choices should be made on failure modes (async validation, nested state, dynamic schemas), not DX first impressions. Tradeoff-first comparisons are rare and useful.
# discuss
- ## 

- ## 

- ## 

- ##  `<input name="username">` 在 iOS 中会锁定用户的主键盘，不能切换输入法。如果用户系统语言使用英文，他就不能用输入法输入中文。
- https://x.com/TooooooBug/status/2011088778014965878
  - 非常震惊，name 居然还能有这种副作用， 感觉这么多年前端白做了。
  - 目前我测出来只影响iOS Edge浏览器，它更像是浏览器自作主张，Safari我测了一下没影响
  - 一些无效解决方案：改name值无效，加inputmode无效，设置autocomplete值无效
  - 有效的解决方案：在密码框前面加上一个输入框，这个输入框会被认为是用户名，原来的用户名的输入框恢复正常。但这个输入框不能被隐藏掉，type="hidden"或者display:none都不行。最后如图，设置absolute不影响原有布局，设置透明度为0视觉隐藏，设置pointer-events不影响其它元素交互。
- 其实我是在 edge 中碰到的，改了 name 值以后，Safari 好了，edge 还是坏的，有待进一步研究。

- 这种w3c标准里面没有定义的行为, 如何实现都是宿主环境说了算的, 要是实现全部统一的话, 也没有浏览器兼容性这种恶心事了
  - w3c在移动端确实缺失非常多东西。

- 有很多類似保留字的規範，之前被 copilot 教育的

- 聚焦密码输入框的时候还不能触发罗技的手势操作

- ## TIL ElementInternals doesn't listen call `reportValidity()` when you submit a form, instead it just checks that you already have `setValidity()` called with an anchor attached. 
- https://twitter.com/RogersKonnor/status/1783922512549609599
  - If the anchor is invisible, it wont show the popup.
  - `form.addEventListener("invalid", () => {}, true)` ; 
  - Whats fascinating is you need to use event capturing to grab it the "invalid" event.

- ##  `<select>` 标签里面可以塞一个 `<hr>` 作为选项分割线，不过只支持比较新的 Safari 17+ 和 Chrome 119+
- https://twitter.com/hal__lee/status/1734180106476900846

- ## I only just learned about `HTMLInputElement.valueAsNumber` and I'm baffled(困惑；难倒). Is this the Mandela effect or something
- https://twitter.com/gaforres/status/1730658548764602636
- `valueAsDate` also for date inputs. Not just getters either, but setters too!

- ## Tip: number inputs have a `valueAsNumber` property, which allows you to quickly get their numeric value 
- https://twitter.com/mgechev/status/1429662217318850560
  - use `input.valueAsNumber` instead of `parseInt(input.value)` 

- ## 🌰 [A Better Way to Work With Number and Date Inputs in JavaScript](https://www.builder.io/blog/numbers-and-dates)

```JS
const myInput = document.querySelector('input.my-input')
const number = myInput.valueAsNumber
const date = myDateInput.valueAsDate
```

- ## Forms tip
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

- ## How to use JavaScript's FormData to collect form fields without refs or state
- https://twitter.com/ReactTraining/status/1716822590533353817
  - 1. Start by giving inputs names
  - 2. Use `new FormData` on the `event.target` . 
  - 3. Use `.get` to access fields by name.

- ## Unpopular opinion: Don't use http verbs PUT, PATCH, DELETE. Just use POST for everything. Reasons:
- https://twitter.com/matthewcp/status/1716549522015310116
  - `<form>` doesn't support the others. Frameworks that allow it do so through hacks.
  - URLs are free, you don't gain anything by overloading them.
  - Purity < practicality
- A bunch of infra-adjacent stuff is easier if you use proper verbs. Eg. PATCH is idempotent, POST is not.
  - *PUT is idempotent, PATCH is not necessarily. (According to MDN)
  - This is good in theory but broken in modern practice. E.g. Next.js caches POST requests, probably because GraphQL uses them even for reads without side-effects.
  - I used to make this argument, but now I think it's over-rated and I agree with the OP. It's just too hard to make every form do the right thing with respect to updates vs. creates. Also, it's rare that retrying an update is really what you want.
- Simplicity that works >>>> anything else.

- ## 使用fetch()上传formData数据时，千万不要在headers中设定content-type！
- https://twitter.com/ahshengchen/status/1687377120459378688

- multipart/form-data 如果修改了content type会覆盖解析数据需要的boundary。标准server就解析不到数据了，可以用postman or paw之类的查看一下和application/x-www-form-urlencoded的报文区别。

- 可以 postman 里测好了，用他的代码生成代码

- ## Wrote a guide about 11 popular HTML and JS mistakes in forms.
- https://twitter.com/sitnikcode/status/1661411602443247616
  - [11 HTML best practices for login & sign-up forms—Martian Chronicles, Evil Martians’ team blog](https://evilmartians.com/chronicles/html-best-practices-for-login-and-signup-forms)

- ## Apparently "email" and "number" inputs don't support setting a selection programmatically? That's a very very weird limitation
- https://twitter.com/fabiospampinato/status/1723356899037298691
  - "use the platform" should really be "use the good parts of the platform", not everything that's built into the browser is good, or even passable. 
  - And accidentally using a buggy part of a browser is a pretty important issue, because those the bugs that you basically can't fix.
- That was actually multiple times a reason for me to use text inputs instead of number inputs.

- ## Using the JavaScript `FormData` Web API, you can progressively enhance a simple, accessible form, into a more dynamic form, without the downsides of heavy JS frameworks that do the same thing.
- https://twitter.com/SaraSoueidan/status/1521469586691997696
  - [Progressive Enhancement and HTML Forms: use FormData](https://www.bram.us/2022/04/22/progressive-enhancement-and-html-forms-use-formdata/)
