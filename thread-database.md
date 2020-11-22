---
title: thread-database
tags: [database]
created: '2020-11-22T12:10:09.397Z'
modified: '2020-11-22T12:18:03.660Z'
---

# thread-database

## pieces

- ### [ObjectiveSQL: 让Java更像SQL](https://www.v2ex.com/t/727939)
- 到底是让Java像SQL一样编程，还是让SQL像Java一样编程，纠结了很久，还是让Java更像SQL，
  - Java的语法表现力不够，只能扩展Javac，实现了算法运算，比较运算，逻辑运算符重载，并封装了常用数据的的函数，抽象了Expression，使Java非常接近SQL，
  - 同时也实现了简单SQL编程的代码生成，基本不需要写代码，也不需要配置就能实现简单SQL的编程
- 我对比过mybatis的`DynamicSQLBuilder`，它做的太土了，大都数都是以字符串的形式体现，我的改进有三块：
  1. 动态代码生成：模型中的所有字段都会被动态生成一个Order的内部类Table中的字段。
  2. 算术运算、比较运算符和逻辑运算重载，也就是说Java中的 +, -, * / , >, <, &&, || 都会转换成SQL语句中的表达式，
  3. 我封装了常用数据库的常用函数，例如：count, sum等有上千个的，这样就不会出现字符
  - 上述做法的好处是，最大程度的避免的SQL的语法错误，动态代码提示和单元测试。
