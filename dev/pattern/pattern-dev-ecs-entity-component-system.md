---
title: pattern-dev-ecs-entity-component-system
tags: [entity-component-system]
created: 2023-04-12T08:05:07.308Z
modified: 2023-04-12T08:06:04.859Z
---

# pattern-dev-ecs-entity-component-system

# guide

# blogs

## [漫谈Entity Component System (ECS) - 知乎](https://zhuanlan.zhihu.com/p/270927422)

- 对于很多人来说，ECS只是一个可以提升性能的架构，但是我觉得ECS更强大的地方在于可以降低代码复杂度。

- 在游戏项目开发的过程中，一般会使用OOP的设计方式让GameObject处理自身的业务，然后框架去管理GameObject的集合。
- 但是使用OOP的思想进行框架设计的难点在于一开始就要构建出一个清晰类层次结构。
- 经过一段时间的开发，总会在某个时间点开始引入多重继承。
  - 实现一个又可工作、又易理解、又易维护的多重继承类层次结构的难度通常超过其得益。
  - 因此多数游戏工作室禁止或严格限制在类层次结构中使用多重继承。
  - 若非要使用多重继承，要求一个类只能多重继承一些 简单且无父类的类(min-in class)，例如Shape和Animator。

- 也就是说在大型游戏项目中，OOP并不适用于框架设计。但是也不用完全抛弃OOP，只是在很大程度上，代码中的类不再具体地对应现实世界中的具体物件，ECS中类的语义变得更加抽象了。

- ECS有一个很重要的思想：数据都放在一边，需要的时候就去用，不需要的时候不要动。
  - ECS 的本质就是数据和操作分离。
  - 传统OOP思想常常会面临一种情况，A打了B，那么到底是A主动打了B还是B被A打了，这个函数该放在哪里。
  - 但是ECS不用纠结这个问题，数据存放到Component种，逻辑直接由System接管。
  - 借着这个思想，我们可以大幅度减少函数调用的层次，进而缩短数据流传递的深度。

- Entity由多个Component组成，Component由数据组成，System由逻辑组成。

## [一个无框架的ECS实现（Entity-Component-System） - 知乎](https://zhuanlan.zhihu.com/p/32787878)

- 游戏，大多都会出现这样一个Entity-Manager系统。
  - 因为游戏本质就是大量实体行为（Entity）以及他们之间的交互（Manager）
