---
title: lang-js-base-promise
tags: [ECMAScript, js, lang, promise]
created: 2022-11-23T17:39:35.125Z
modified: 2022-11-23T17:40:18.712Z
---

# lang-js-base-promise

# guide

- `catch()` method is a shortcut for `Promise.prototype.then(undefined, onRejected)`.
# examples
- ## [Promises - reject vs. throw - Stack Overflow](https://stackoverflow.com/questions/33445415/javascript-promises-reject-vs-throw)
- the biggest difference is that `reject` is a callback function that gets carried out after the promise is rejected, whereas `throw` cannot be used asynchronously. 
  - If you chose to use `reject`, your code will continue to run normally in asynchronous fashion whereas `throw` will prioritize completing the resolver function (this function will run immediately).
- Another important fact is that `reject()` DOES NOT terminate control flow like a return statement does. 
  - In contrast `throw` does terminate control flow.

```JS
new Promise(function() {
  setTimeout(function() {
    throw 'or nah';
    // return Promise.reject('or nah'); also won't work
  }, 1000);
}).catch(function(e) {
  console.log(e); // doesn't happen
});

new Promise(function(resolve, reject) {
  setTimeout(function() {
    reject('or nah');
  }, 1000);
}).catch(function(e) {
  console.log(e); // works!
});
```
