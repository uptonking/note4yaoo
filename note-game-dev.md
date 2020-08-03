---
title: note-game-dev
tags: [dev, game]
created: '2020-07-13T13:27:14.170Z'
modified: '2020-08-03T13:29:04.709Z'
---

# note-game-dev

## guide 

- 游戏引擎架构
  - 渲染库
  - 动作系统
  - 物理系统
  - 战斗回合流程
  - 游戏编辑器

## catalog

- 主流游戏开发引擎
  - Unity3D
    - 免费不开源
  - Unreal Engine 4
    - 开源但只能学习不能再次分发
- common
  - https://github.com/libgdx/libgdx  /Apache 2
    - 基于gwt，放弃
  - https://github.com/cocos2d/cocos2d-x  /MIT
    - cocos2d-js不如-x好用
  - https://github.com/pixijs/pixi.js  /MIT
  - https://github.com/photonstorm/phaser  /MIT
    - 从性能到底层api的易用和强大
    - 没有做模块拆分，tween,particles等全在一个包中，release的min版本大概在2M，egret在700K左右
    - Phaser 2一直采用开源的Pixi2版本作为2D渲染引擎，在Phaser3中已放弃Pixi
    - Phaser 3.0.0 is released on 20180213.
  - https://github.com/godotengine/godot  /MIT

- misc
  - https://github.com/nicolodavis/boardgame.io  /MIT    
  - https://github.com/FormidableLabs/react-game-kit  /MIT
  - https://github.com/deck-of-cards/deck-of-cards  /MIT
  - https://github.com/layabox/layaair 
    - 引擎全部开源并且全部免费使用，包括商用
  - https://github.com/hiloteam/Hilo  /MIT
    - 阿里h5游戏解决方案，有申请专利
  - https://github.com/egret-labs/egret-core  /BSD/ts
