---
title: lang-js-typescript-issues
tags: [issues, lang, typescript]
created: 2021-03-22T14:43:52.929Z
modified: 2021-03-22T14:46:20.632Z
---

# lang-js-typescript-issues

# guide

# not-yet
- class的constructor和字段属性如何共用类型定义和注释
  - 将类型P1单独定义在外部
  - class C1 implements P1
  - implements会继承P1的jsdoc注释，但不会继承类型
  - C1的字段需要再次用P1['field1']声明类型，否则没有类型
# ts-limitations
- ## [How to build a TypeScript class constructor with object defining class fields? - Stack Overflow](https://stackoverflow.com/questions/49061774/how-to-build-a-typescript-class-constructor-with-object-defining-class-fields)
- 可以使用 Pick或Partial

```typescript
class Item {
    public id: number;
    public updatedAt?: number;
    public createdAt?: number;
    constructor(data: Pick<Item, "id" | "updatedAt" | "createdAt">) {
        Object.assign(this, data);
    }
    method() {}
}
const item = new Item({ id: 1  }); //id is required others fields are not
const item2 = new Item({ id: 1, method() {}  }); // error method is not allowed
```

- [Infer class constructor arguments from instance of class in TypeScript - Stack Overflow](https://stackoverflow.com/questions/64841408/infer-class-constructor-arguments-from-instance-of-class-in-typescript)
- This is currently a limitiation in TypeScript. Class instances do not have strongly-typed constructor properties; as you noted, the compiler only sees its type as Function. 
# issues
