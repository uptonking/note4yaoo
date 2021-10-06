---
title: job-leetcode-map-dict
tags: [algorithms, coding, hashmap, job, leetcode]
created: '2021-10-05T09:02:53.624Z'
modified: '2021-10-06T14:46:37.860Z'
---

# job-leetcode-map-dict

# guide

# LRU 最近最少使用

```JS
/**
 * * 设计和实现一个 LRU (最近最少使用) 缓存机制
 * https://leetcode-cn.com/problems/lru-cache/
 * https://github.com/sisterAn/JavaScript-Algorithms/issues/7
 * - 超出容量时，需要删除最不经常使用的key，这个key一直维持在数组索引下标0
 */
function LRUCache(capacity) {
  this.cache = Object.create(null);
  /** 使用单独的数组维护key的使用顺序 */
  this.keys = [];
  /** 最大缓存数量 */
  this.capacity = capacity;
}

LRUCache.prototype.get = function(key) {
  if (this.cache[key]) {
    // 最新获取过的key都放在数组末尾
    removeKey(this.keys, key);
    this.keys.push(key);
    return this.cache[key];
  }

  return -1;
};

LRUCache.prototype.put = function(key, val) {
  if (this.cache[key]) {
    // 若已存在，则更新缓存

    // 最新加入缓存的，也加到末尾
    removeKey(this.keys, key);
    this.keys.push(key);
    this.cache[key] = val;
  } else {
    this.keys.push(key);
    this.cache[key] = val;
    if (this.keys.length > this.capacity) {
      // 若超出容量
      // removeKey(this.keys, this.keys[0]);
      this.keys.shift();
      this.cache[key] = null;
    }
  }

  return -1;
};

function removeKey(arr, key) {
  if (!arr.length) return;
  const idx = arr.indexOf(key);
  if (idx !== -1) {
    return arr.splice(idx, 1);
  }
}
```

# 设计一个在常数时间O(1)下插入获取元素的数据结构

```JS
/**
 * * 设计一个支持在平均时间复杂度O(1)下，常数时间插入、删除和获取随机元素
 */

const RandomizedSet = function() {
  // 保存 值
  this.list = [];
  // 保存 值，值在list中的索引
  this.map = {};
};

RandomizedSet.prototype.insert = function(val) {
  if (this.map[val]) return false;

  // 直接插入数组
  this.list.push(val);
  this.map[val] = this.list.length;
  return true;
};

RandomizedSet.prototype.remove = function(val) {
  if (!this.map[val]) return false;

  const final = this.list[this.list.length - 1];

  // 下面这块主要是把要数组的尾值赋给对应的val值的位置，之后把数组最后的值踢出去即可
  const index = this.map[val];
  // 这里的index-1即我们拿到的index不是数组的下标，还需要减1。
  this.list[index - 1] = final;
  this.map[final] = index;

  // 从map对象中删除
  delete this.map[val];

  this.list.pop();

  return true;
};

RandomizedSet.prototype.getRandom = function() {
  const index = Math.floor(Math.random() * this.list.length);
  return this.list[index];
};
```


