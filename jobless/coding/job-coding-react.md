---
title: job-coding-react
tags: [coding, job, react, 手撕代码]
created: '2021-09-22T17:13:19.314Z'
modified: '2021-10-05T08:55:35.067Z'
---

# job-coding-react

# diff

```JS
      // 对比oldFiber和当前element
      const sameType = oldFiber && element && oldFiber.type === element.type; //检测类型是不是一样

      
      // 先比较元素类型
      if (sameType) {
        // 如果新老节点类型一样，复用老节点DOM，更新props
        newFiber = {
          type: oldFiber.type,
          props: element.props,
          dom: oldFiber.dom,
          return: workInProgressFiber,
          alternate: oldFiber, // 记录下上次状态
          effectTag: 'UPDATE' // 添加一个操作标记
        }
      } else if (!sameType && element) {
        // 如果类型不一样，有新的节点，创建新节点替换老节点
        newFiber = {
          type: element.type,
          props: element.props,
          dom: null, // 构建fiber时没有dom，下次perform这个节点是才创建dom
          return: workInProgressFiber,
          alternate: null, // 新增的没有老状态
          effectTag: 'REPLACEMENT' // 添加一个操作标记
        }
      } else if (!sameType && oldFiber) {
        // 如果类型不一样，没有新节点，有老节点，删除老节点
        oldFiber.effectTag = 'DELETION'; // 添加删除标记
        deletions.push(oldFiber); // 一个数组收集所有需要删除的节点
      }
```

# react-like
