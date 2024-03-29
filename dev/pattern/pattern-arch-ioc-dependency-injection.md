---
title: pattern-arch-ioc-dependency-injection
tags: [dependency-injection, pattern]
created: 2021-08-04T13:38:54.030Z
modified: 2021-08-04T13:40:01.125Z
---

# pattern-arch-ioc-dependency-injection

# guide

# blogs

## [How to Design a Type Friendly Context](https://saul-mirone.github.io/how-to-design-a-type-friendly-context/)

- Koa makes it really popular that apps should built by a simple core to load plugins, and bundles of plugins to implement unique features. 
  - Today lots of apps are built with this pattern. For example, vscode and webpack.
- when Koa meets static type checking, everything stop working. 
  - Type system cannot infer what property is really on ctx and what’s not
- It’s a common problem of languages with static type system: how to handle object shared between modules elegantly?
  - The key is using IoC. With this pattern we can inject type information into context.
- Let’s reconsider the design of context in koa, we can see that the context is an object with properties you can modify, such as `ctx.foo`. 
  - What if we transform this API into `ctx.get(foo)`? 
  - Since the creation of foo is what we can control, we can write some information on it.
- We just split up the entire `ctx` into several pieces of `slice`s.
  - We create a `metadata` that brings slice’s information on it. 
  - And a `slice factory` that can be used to inject on context.
  - We use a simple `Map` as the container of slices, with the `symbol` as key so the slices will not be conflict between each other.

```typescript

type Ctx = Map<symbol, Slice>;

type Slice<T = unknown> = {
  id: symbol;
  set: (value: T) => void;
  get: () => T;
};

type Metadata<T> = {
  id: symbol;
  (ctx: Ctx): Slice<T>;
};

const createSlice = <T>(defaultValue: T): Metadata<T> => {
  const id = Symbol("Slice");

  const metadata = (ctx: Ctx) => {
    let inner = defaultValue;
    const slice: Slice<T> = {
      id,
      set: (next) => {
        inner = next;
      },
      get: () => inner
    };
    ctx.set(id, slice as Slice);
    return slice;
  };
  metadata.id = id;

  return metadata;
};

const createCtx = () => {
  const map: Ctx = new Map();

  const getSlice = <T>(metadata: Metadata<T>): Slice<T> => {
    const value = map.get(metadata.id);
    if (!value) {
      throw new Error("Slice not injected");
    }
    return value as Slice<T>;
  };

  return {
    inject: <T>(metadata: Metadata<T>) => metadata(map),
    get: <T>(metadata: Metadata<T>): T => getSlice(metadata).get(),
    set: <T>(metadata: Metadata<T>, value: T): void => {
      getSlice(metadata).set(value);
    }
  };
};
```

```JS
// testing

const num = createSlice(0);
const ctx1 = createCtx();
const ctx2 = createCtx();

ctx1.inject(num);
ctx2.inject(num);

const values = [];

const x = ctx1.get(num);
values.push(x);

ctx1.set(num, x + 1);

values.push(ctx1.get(num));
values.push(ctx2.get(num));

expect(values).toEqual([0, 1, 0]);
```

# discuss-design-pattern-ioc
- ## 

- ## 

- ## I couldn't understand Dependency Injection until I discovered this trick.
- https://twitter.com/RaulJuncoV/status/1715338944185827575
- The 5 questions I ask myself before creating an object.
1. Is this object a service or a utility class?
Service classes contain important business logic.
Utility classes are stateless and have helper methods.
If it's a service, use DI to inject it instead.

2. Will I need to swap this implementation for another?
Using "new" creates tight coupling to a specific class.
This makes it hard to swap out implementations for testing or extended functionality.
Use interfaces and inject the dependency to make swapping implementations easier.

3. Does this object have external dependencies?
If the object has its dependencies, you're also coupling your class to its dependencies.
It's better to let a DI framework handle the instantiation and resolve all the dependencies.

4. Is the object for carrying data?
You don't need to inject objects that hold data (DTOs, POCOs, etc.)
If it's just a data carrier, using "new" is OK.

5. Is the object relevant within a limited scope?
You don't need to inject temporary collections or other transient state-holding objects.
In simple terms, always question the "new".

- I would even go further and forget "the object" and focus on roles. 
