---
title: page-lang-js-proposal
tags: [ ECMAScript, js, lang, proposal]
created: '2021-01-19T10:56:19.934Z'
modified: '2021-01-19T10:56:51.898Z'
---

# page-lang-js-proposal

# [JavaScript ES2021 - You Need To See These ES12 Features](https://catalins.tech/javascript-es2021-you-need-to-see-these-es12-features)

- It's important to start the article by mentioning that ES2021 or ES12 is in stage 4 of the process. 
  - That means it's not released yet. 
  - The plan is to release ES12 in June 2021. 
  - What's new in ES12?
- ## `String.prototype.replaceAll()`
  - `'jxvxscript'.replaceAll('x', 'a');`
- ## `Promise.any`
  - The new method takes multiple promises and resolves once any of the promises is resolved. 
  - Promise.any() takes whichever promise resolves first. 
- ## `WeakRef`
  - WeakRef is the shorthand for Weak References, and its primary use is to hold a weak reference to another object.
  - That means it does not prevent the garbage collector from collecting the object. 
  - The Weak Reference is useful when we do not want to keep the object in the memory forever.
- ## `&&=, ||= and ??=`
  - Question question equals (??=)
  - Similarly to the Nullish Coalescing Operator, an assignment is performed only when the left operand is nullish or undefined.
  - `first ?? (first = second)` is the equivalent of `first ??= second`
  - The variable first gets assigned the variable second only if first is "null" or "undefined"
- ## Numeric separators
  - `2_145_723`
  - That is, you use underscores to improve the readability
