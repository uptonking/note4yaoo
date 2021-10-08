---
title: job-leetcode-map-dict
tags: [algorithms, coding, hashmap, job, leetcode]
created: '2021-10-05T09:02:53.624Z'
modified: '2021-10-06T14:46:37.860Z'
---

# job-leetcode-map-dict

# guide

# 设计数据结构：LRU 最近最少使用
- LRUCache(int capacity) 
  - 以正整数作为容量 capacity 初始化 LRU 缓存
- int get(int key) 
  - 如果关键字 key 存在于缓存中，则返回关键字的值，否则返回 -1 。
- void put(int key, int value) 
  - 如果关键字已经存在，则变更其数据值；
  - 如果关键字不存在，则插入该组「关键字-值」。
  - 当缓存容量达到上限时，它应该在写入新数据之前删除最久未使用的数据值，从而为新的数据值留出空间。

```JS
/**
 * * 设计和实现一个 LRU (最近最少使用) 缓存机制。
 * * 数据的保存慎用 {}，因为迭代keys的顺序不同方法得到的结果可能不同
 * https://leetcode-cn.com/problems/lru-cache/
 * https://github.com/sisterAn/JavaScript-Algorithms/issues/7
 * - 超出容量时，需要删除最不经常使用的key，要删除的key总是数组索引下标0
 */

/**
 * * 使用Map既可以保存数据，也可以记住插入顺序，注意set()更新时不会改变顺序
 * - Map删除key后，has返回值直接判断是否存在key，可以不用管属性值是否是0/null
 */
function LRUCache(capacity) {
  this.capacity = capacity || 16;
  this.cache = new Map();
}
LRUCache.prototype.get = function(key) {
  if (this.cache.has(key)) {
    const val = this.cache.get(key);
    this.cache.delete(key);

    this.cache.set(key, val);
    return val;
  }

  return -1;
};
LRUCache.prototype.put = function(key, value) {
  if (this.cache.has(key)) {
    this.cache.delete(key);

    this.cache.set(key, value);
  } else {
    this.cache.set(key, value);

    if (this.cache.size > this.capacity) {
      // 先获取Map的第一个key，注意keys()方法返回值类型是 iterator
      this.cache.delete(this.cache.keys().next().value);
    }
  }
};
```

```JS
/**
 * * 设计和实现一个 LRU (最近最少使用) 缓存机制。
 * * 使用双向链表处理插入删除，使用Map只保存节点值，不记录顺序
 * https://www.iitter.com/other/8206.html
 * 典型的用空间来换时间的做法
 */
function LRUCache2(capacity) {
  this.capacity = capacity || 16;
  /** 保存的是 key,ListNode,只保存数据，不保存顺序 */
  this.cache = new Map();

  // head/tail在每次操作结束后始终指向头尾哨兵辅助节点，且不含有效数据
  // head.next是第1个数据节点
  this.head = new ListNode('head', -1);
  // tail.prev是最后一个数据节点
  this.tail = new ListNode('tail', -1);

  this.head.next = this.tail;
  this.tail.prev = this.head;
}

function ListNode(key, val) {
  this.val = val;
  this.key = key;
  this.prev = null;
  this.next = null;
}

LRUCache2.prototype.get = function(key) {
  if (this.cache.has(key)) {
    const keyNode = this.cache.get(key);

    moveToTail(keyNode, this.tail);

    return keyNode.val;
  }

  return -1;
};

LRUCache2.prototype.put = function(key, value) {
  if (this.cache.has(key)) {
    const keyNode = this.cache.get(key);
    keyNode.val = value;

    moveToTail(keyNode, this.tail);
    // this.get(key);
  } else {
    const newNode = new ListNode(key, value);

    // 将新节点加到链表尾部
    newNode.next = this.tail;
    newNode.prev = this.tail.prev;

    this.tail.prev.next = newNode;
    this.tail.prev = newNode;

    this.cache.set(key, newNode);

    if (this.cache.size > this.capacity) {
      // 删除队头数据
      this.cache.delete(this.head.next.key);

      // 从 head > node1 > node2 的头部部分，删除node1
      // 👀️ 下面2行顺序不能换，注意多练习，先处理后面节点的prev，在修改前面节点的next
      this.head.next.next.prev = this.head;
      this.head.next = this.head.next.next;
    }
  }
};

/**
 * 将节点node中链表中删除，并添加到链表尾部
 */
function moveToTail(node, tail) {
  // 从链表中删除keyNode
  node.prev.next = node.next;
  node.next.prev = node.prev;

  // 将keyNode插入链表尾部
  node.next = tail;
  node.prev = tail.prev;

  tail.prev.next = node;
  tail.prev = node;
}
```

```JS
/**
 * * 设计和实现一个 LRU (最近最少使用) 缓存机制。
 * * ❌️使用[]保存缓存数据的key，oj未通过，超出时间限制
 * * 用数组来模拟栈结构，当涉及大量插入或删除操作时，线性空间的缺点就很明显
 * - 注意处理属性值为0、null的情况
 */
function LRUCache3(capacity) {
  this.cache = Object.create(null);
  /** 使用单独的数组维护key的使用顺序 */
  this.keys = [];
  /** 最大缓存数量 */
  this.capacity = capacity;
}
LRUCache3.prototype.get = function(key) {
  // 注意 属性值可以为0、null
  if (this.cache[key] != null) {
    // 最新获取过的key都放在数组末尾
    removeKey(this.keys, key);
    this.keys.push(key);
    return this.cache[key];
  }

  return -1;
};
LRUCache3.prototype.put = function(key, val) {
  // 注意 属性值可以为0、null
  if (this.cache[key] != null) {
    // 若已存在，则更新缓存

    // 最新加入缓存的，加到末尾
    removeKey(this.keys, key);
    this.keys.push(key);
    this.cache[key] = val;
  } else {
    this.keys.push(key);
    this.cache[key] = val;
    if (this.keys.length > this.capacity) {
      // 若超出容量
      delete this.cache[this.keys[0]];
      this.keys.shift();
    }
  }
  return -1;
};

function removeKey(arr, key) {
  if (!arr.length) return;
  const idx = arr.indexOf(key);
  if (idx > -1) {
    return arr.splice(idx, 1);
  }
}
```

# 第一个只出现一次的字符

```JS
/**
 * * 第一个只出现一次的字符
 * https://leetcode-cn.com/problems/di-yi-ge-zhi-chu-xian-yi-ci-de-zi-fu-lcof/
 * https://github.com/sisterAn/JavaScript-Algorithms/issues/50
 * 使用 map 两次遍历即可：
 * 遍历字符串，将每个字符的值与出现次数记录到map中
 * 再次遍历 map.keys() ，获取 map 中每个字符出现的次数，判断是否仅仅只有 1 次，返回第一个仅出现一次的字符
 */
function firstUniqChar(s) {
  if (!s) return ' ';
  const map = {};
  for (let i = 0, len = s.length; i < len; i++) {
    // 出现1次的就是1，再次出现就会变0
    map[s[i]] = map[s[i]] === undefined ? 1 : 0;
  }
  for (const item in map) {
    if (map[item] === 1) {
      return item;
    }
  }
  return ' ';
}
```

# 设计一个在常数时间O(1)下插入获取元素的数据结构

```JS
/**
 * * 设计一个支持在平均时间复杂度O(1)下，常数时间插入、删除和获取随机元素
 * * 思路：常数时间就多考虑数组和映射表
 */
const RandomizedSet = function() {
  // 保存 值
  this.list = [];
  // 保存 值，值在list数组中的索引+1
  this.map = {};
};

RandomizedSet.prototype.getRandom = function() {
  const index = Math.floor(Math.random() * this.list.length);
  return this.list[index];
};

RandomizedSet.prototype.insert = function(val) {
  if (this.map[val]) return false;

  // 直接插入数组
  this.list.push(val);
  this.map[val] = this.list.length;
  return true;
};

// 每次删除元素时，将数组最后一个元素移动到待删除位置，然后数组pop
// map中直接删除元素值kv就可以了
RandomizedSet.prototype.remove = function(val) {
  if (!this.map[val]) return false;

  const lastItem = this.list[this.list.length - 1];

  // 下面这块主要是把要数组的尾值赋给对应的val值的位置，之后把数组最后的值踢出去即可
  const index = this.map[val];

  // 这里的index-1即我们拿到的index不是数组的下标，还需要减1。
  this.list[index - 1] = lastItem;
  this.map[lastItem] = index;

  this.list.pop();

  // 从map对象中删除
  delete this.map[val];

  return true;
};
```
