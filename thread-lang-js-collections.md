---
title: thread-lang-js-collections
tags: [collections, lang-js, thread]
created: 2023-11-10T07:36:40.096Z
modified: 2023-11-10T07:38:26.990Z
---

# thread-lang-js-collections

# guide

# dev-xp
- Map对象
  - 可作为key的有: 空字符串'', undefined
# discuss-stars
- ## 

- ## 

- ## 

- ## Learn about JavaScript array methods cheat sheet 
- https://twitter.com/davidm_ml/status/1787056238196392392

- ## i actually didn't knew that mutating while looping on a `forEach` would skip indexes
- https://twitter.com/meijer_s/status/1676506116736397312
- Does it skip indexes when you delete elements in the loop? This is the sort of thing that makes me nervous to see but theoretically I would expect it to work
  - It does indeed. 

```JS
const h = new Map();

for (let i = 0; i < 10; i++) {
  h.set(`x-custom-${i}`, i % 3 === 0 ? i : undefined);
}

h.forEach((v, k) => {
  if (v && v !== 'undefined' && v !== 'null') return;
  h.delete(k);
});

// 💡 上面delete后，对应的kv就消失了，这里只会迭代打印3次
h.forEach((v, k) => {
  console.log(k, v);
});
```

- ## 1MillionItems.forEach(() => { … // ☠️ }) This experience sucks.
- https://twitter.com/tannerlinsley/status/1516185993535111172
- https://github.com/TomerAberbach/lfi
  - A lazy functional iteration library supporting sync, async, and concurrent iteration.

- ## I just spent ~4 hours investigating an "eats-all-the-gigabytes" memory leak in JavaScript and the solution turned out to be:
- https://twitter.com/andrestaltz/status/1473669713490235397
  - Because `map` passes 3 args: item, index, thisObj. Friends, be careful.

```diff
-arr.map(myFunction)
+arr.map(x => myFunction(x))
```

# discuss-reduce
- ## 

- ## 

- ## Just a reminder that using `reduce` doesn't always mean iterating less. 
- https://twitter.com/i_like_robots/status/1418874992146755584
  - 追求极致性能时可适度放弃immutable，使用mutable方法
  - The first example using has O(n²) complexity due to the additional iterations required by the spread operator and is ~50x slower than `filter/map` and ~100x slower than using array `push` .

```JS
// slow
items.reduce((acc, item) => item.prop ? [...acc, item.prop] : acc, []);

// equivalent to slow
items.reduce((acc, item) => {
  if (item.name) {
    return [].concat(
      typeof acc[Symbol.iterator] === 'function' ? acc.map(i => i) : [], item.name
    )

    return acc;
  }
}, []);

// fast
items.filter((item) => item.prop).map((item) => item.prop);

// faster
items.reduce((acc, item) => {
  item.prop && acc.push(item.prop);
  return acc;
}, []);
```

- if you're thinking "that's cool in theory but I'm sure engines have optimisations for this" then nope, you're wrong. And 100x slower is generous, some browsers are 1000x slower! If you're doing this lots of times in your apps then you could make them noticeably faster.
- And of course **`reduce` with object spread creating a newly cloned object for each iteration is no better - it's also super slow**.

- Ditch the `reduce` in the final example for a `for-of` loop to make it more readable. If you're using reduce simple for looping, just use a loop. Way less for the reader to think about, and it reads sequentially.

- Nice! It's also doesn't counted as a harmful mutation because it's internal scoped one with no effect on externals. @getify talked nicely about this in his book "Functional-light JavaScript"
  - tbh I don’t bother sticking to theory and mutate when it is ok

- ## here are my thoughts on reduce vs chaining array methods vs for loop
- https://twitter.com/kentcdodds/status/1396820360792731648
  - [Array reduce vs chaining vs for loop](https://kentcdodds.com/blog/array-reduce-vs-chaining-vs-for-loop)
  - Actually, I wrote this over a year ago and now I use for loops a lot more. 
  - I think I should probably update the post to give the loop a more positive light. 
  - I think for of **loops are definitely easier to understand** than reduce.
- Ya, it’s obviously all subjective. but the for-loop (to me) is far more explicit and easy to parse
- Finally someone with a sensible and pragmatic take on this issue. I too just map and filter specially cause most UI is short lists (short for processing by even slow phones). I only use reduce for transformation between data types (array to object).

- ## reduce() is a very helpful function because it accomplishes two important tasks at once: writing unreadable code and showing off how smart you are
- https://twitter.com/eevee/status/1396445889883906053
- 2 years ago me was totally with you, but now i use it frequently. just give it a go
- “our core user metrics improved after replacing reduce with map and filter in our JavaScript code base” said no one ever

# discuss
- ## 

- ## 

- ## I often see filter calls that needlessly fall back to an empty array. 
- https://twitter.com/housecor/status/1761755043651366954
  - JavaScript's array.filter always returns an array.
  - Even when the array being filtered is empty.
  - Even when the filter finds no results.

- ## If you have a JS array and want a map from its value to their indexes, the shortest code to do so is probably `new Map(arr.map(Array))` , which feels like magic.
- https://twitter.com/NicoloRibaudo/status/1757877709688950985
- I wonder if `new Map(Object.entries(arr))` is significantly different (it's still two iterations)
  - This creates a index->value map rather than value->index

- new Map(arr.map((value, index) => [value, index]))

- ## I'm starting to avoid putting any data in an object keys.seems easier to iterate, filter, expand, 
- https://twitter.com/daKmoR/status/1382313714276270090
  - from `{k: 'v'}` to `{name: ` k `, value: 'v'}` .
  - Filtering and iterating especially seems nicer with an array of objects.
  - But by FAR the biggest benefit is extendability without a "breaking" change.
- `Object.keys, Object.values, Object.entries` are very helpful for structure #1. 
  - I tend to prefer the readability of #1 personally.
- I'm curious: in which cases? What are the pros/cons? The second object structure reminds me of XML.
- I tend to prefer Map. Best of both worlds imo. 
  - You can initialize it using an array, it's easy lookup (no need for find + predicate), easy filtering and iterating because it is Iterable by default.

- ## I often use JavaScript Maps and Sets and often have to enumerate over them. 
- https://twitter.com/trueadm/status/1411457860698005504
  - I benchmarked this about a year ago, and found extracting an array via `Array.from` and then looping over was fastest. 
  - Now it turns out `for…of` on the Map/Set is fastest. How things change.
- This was consistent between all browsers JS engines too. 
  - Interestingly, JSC (Safari) performs really well for cloning Sets and Maps via using the `constructor` .
  - `const clone = new Map(oldMap)` // clone
  - Every other JS engine performs better if you manually loop over and copy into the clone.
  - I mean using the `constructor` is by far the nicest way of doing it. I'd love it if the folks working on V8 and SpiderMonkey could optimize this code-path like the folks working on JSC have.
  - Probably not worth micro optimising then?
  - I think it is. I've found compilers and parsers to be good use-cases where these operations are frequent enough to translate into seconds of build time performance.
- The problem of course is the polyfill. Using the Babel polyfill for `for…of` statements means performance drops dramatically. Almost to the point where you consider not using them still.
- This week I found a >2x perf win on latest V8 by switching some heavy nested object iteration from `for (var [k, v] of Object.entries(o))` to `for (var k in o)` .
  - The use-case was to accumulate an array of all keys two levels deep.
  - Yup, `for/in` is much faster especially if your objects have stable shapes; especially in unoptimized code. Be careful with microbenchmarks. (But only if it matters...)
  - When using `for…in` it's also recommended to use `hasOwnProperty` , which adds additional overhead.

- ## TypeScript: .map() only works for Arrays, not for tuples.
- https://twitter.com/rauschma/status/1415750873788071939
- You can still *implement* with .map(), you just need a cast
- In fp-ts this is called `Tuple.bimap`

- ## Does `['a', 'b', 'c'].includes()` translate to a Set().has() internally?
- https://twitter.com/kuvos/status/1420101675747102722
- Doubt it. Too much overhead compared to linear search.

- ## Filtering an Object in TypeScript
- https://www.steveruiz.me/posts/how-to-filter-an-object
  - rest operator can also be used to filter props.

```typescript
// /in es6
function filterObject(obj, fn) {
  return Object.fromEntries(Object.entries(obj).filter(fn))
}

// /in ts
type Entry<T> = {
  [K in keyof T]: [K, T[K]]
}[keyof T]

function filterObject<T extends object>(
  obj: T,
  fn: (entry: Entry<T>, i?: number, arr?: Entry<T>[]) => boolean
) {
  return Object.fromEntries(
    (Object.entries(obj) as Entry<T>[]).filter(fn)
  ) as Partial<T>
}

// /in old browser

function filterObject2<T extends object>(
  obj: T,
  fn: (entry: Entry<T>, i?: number, arr?: Entry<T>[]) => boolean
): Partial<T> {
  const next = { ...obj };

  const entries: Entry<T>[] = []

  for (const key in obj) {
    entries.push([key, obj[key]])
  }

  for (let i = 0; i < entries.length; i++) {
    const entry = entries[i];
    if (!fn(entry, i, entries)) {
      delete next[entry[0]]
    }
  }

  return next;
}
```

- ## TIL: use array.every instead of forEach when you need to break
- https://twitter.com/sebastienlorber/status/1426235846647328774
  - This can replace while loops + break/continue; 
- The goal of *every* and *some* (and *none*/*any*) is not to break out of the loop or do anything with the items. Rather it's a higher-order function that checks whether *every* element in the array matches a predicate.
- this will be nicely labelled with "changes requested" when it gets reviewed

- ## if you're sorting an array in JS and keep forgetting how to write the compare functions
- https://twitter.com/DavidKPiano/status/1292237580780605440

```JS
nums.sort((a, z) => a - z);
(a, z) => a - z // ascending, like "a to z"
(a, z) => z - a // descending, like "z to a"
```

- ## Today I learned that `Array.concat()` can work just fine with non array variables.
- https://twitter.com/maxkoretskyi/status/1436010126415122434
  - It simply adds them to the array without inlining, so there's no need to use extra check if a variable is array or not.  
  - Of course, you pay with extra new array for that

```js
const a = 1;
const b = [2];

// no need for Array.isArray(a)
[].concat(a, b) // [1,2]
[a, ...b] // works too
```

- ## Array elements are actually properties with string keys
- https://twitter.com/rauschma/status/1438030552871981056

```JS
const arr = ['a', 'b'];
arr.prop = 123;

assert.deepEqual(
  Object.keys(arr),
  ['0', '1', 'prop']);

assert.equal(arr[0], 'a'); // true
assert.equal(arr['0'], 'a'); // true
```

- Just because you can doesn't mean you should
- I got bitten the other week by `Object.entries` returning the indexes as strings, not numbers.
- But modern JavaScript engines do manage to optimize Array access to behave like the array of languages like C or Java, and not like dictionaries

- ##  `Array.from` uses (rightly so) `Symbol.species` , while `Object.fromEntries` doesn't
- https://twitter.com/WebReflection/status/1461320477012631554
  - Amend: Array.from uses `this` , not Symbol.species … yet Object.fromEntries doesn’t

- ## When to use Map vs. Object, a reference guide.
- https://twitter.com/builderio/status/1513955108614193155
- would use for...of in objects too. key difference is also that object literals contain obj['constructor'] which might break expectations in some code.
- Maps iterate over entries, not keys by default, and Object.keys is iterable as well and symbols are allowed as keys in objects, not just strings.

- ## Do you still use the Array method .forEach()? Poll:
- https://twitter.com/rauschma/status/1525822812853870592
- I prefer for-of:
  - It works with any synchronous iterable [1].
  - for-await-of [2] is similar and works with async iterables.
  - You can `yield` and `await` inside for-of loops.
- If you need access to Array indices
  - for (const [index, elem] of arr.entries()) {  }
- .forEach() can’t be terminated early, but .some() can be used as a workaround (return `true` to break).
- for…of for minimizing the stack trace, and automatic infer types in TS
- I avoid foreach and favor filter, map and reduce. Unless you specifically need a custom iterator it's better form.

- ## It just occurred to me—.filter() could also be called .findAll()
- https://twitter.com/rauschma/status/1529099909575720962

- That’s destructuring to trigger the proxy getter and validate all at once … just one out of many examples where Proxy can improve DX a lot combined with modern JS syntax.

- ## TIL be careful with `Array.every` and empty arrays.
- https://twitter.com/steveruizok/status/1597207156436393984
  - if you dig into the chromium source, this is exactly how it's implemented

```JS
[].every(item => false) //true
[].some(item => false) //false
```

- ## One cool use case for Maps - creating a simple O(1) LRU cache
- https://twitter.com/Steve8708/status/1623906230841536515
  - Given how Maps preserve the order of their keys, implementation is trivial

- ## It might be nice if you could iterate over Sets in JS without going through slow-ass iterators. 
- https://twitter.com/fabiospampinato/status/1645916795071606786
  - It'd be even nicer if a Set-like class that worked like that was implementable efficiently within the language.
- class MySet extends Array and implement add using WeakSet to check for existence.
