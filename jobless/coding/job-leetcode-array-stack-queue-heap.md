---
title: job-leetcode-array-stack-queue-heap
tags: [algorithms, coding, heap, job, leetcode, queue, stack]
created: '2021-09-21T19:40:24.161Z'
modified: '2021-10-06T14:54:06.837Z'
---

# job-leetcode-array-stack-queue-heap

# guide

# 数组中的第K个最大元素

```JS
/**
 * * 数组中的第K个最大元素
 * https://leetcode-cn.com/problems/kth-largest-element-in-an-array/
 * https://github.com/sisterAn/JavaScript-Algorithms/issues/62
 */
function findKthLargest(nums, k) {
  const len = nums.length;
  if (len === 1) return nums[0];

  // 整个数组，从最后一个非叶子节点从后往前构建大顶堆，使数组整体有序
  for (let i = Math.floor(len / 2 - 1); i >= 0; i--) {
    heapifyMax(nums, i, len);
  }

  // 处理到第k个数就可以结束了
  for (let j = len - 1; j >= len - k; j--) {
    swap(nums, 0, j);
    heapifyMax(nums, 0, j);
  }

  return nums[len - k];
}
```

# 前K个高频元素

```JS
/**
 * * 前 K 个高频元素。给定一个非空的整数数组，返回其中出现频率前 k 高的元素。
 * https://leetcode-cn.com/problems/top-k-frequent-elements/
 * https://github.com/sisterAn/JavaScript-Algorithms/issues/61
 * 遍历一遍数组统计每个元素的频率，并将元素值（ key ）与出现的频率（ value ）保存到 map 中
 */
function topKFrequent(nums, k) {
  // let map ={};// 最好不用字面量，若扩展到任意数组的元素频率统计，需要区分 1和 '1'
  const map = new Map();

  nums.forEach((num) => {
    if (map.has(num)) {
      map.set(num, map.get(num) + 1);
    } else {
      map.set(num, 1);
    }
  });
  const mapSize = map.size;
  const mapKeys = [...map.keys()];

  if (mapSize <= k) {
    return mapKeys;
  }

  for (let i = Math.floor(mapSize / 2 - 1); i >= 0; i--) {
    heapifyMax(mapKeys, i, mapSize, map);
  }

  for (let j = mapSize - 1; j >= mapSize - k; j--) {
    swap(mapKeys, 0, j);
    heapifyMax(mapKeys, 0, j, map);
  }

  return mapKeys.slice(-k).reverse();
}
```

# 最小的k个数

```JS
/**
 * * 最小的k个数；
 * * 思路：堆排序，维护一个 K 大小的小顶堆。
 * https://leetcode-cn.com/problems/zui-xiao-de-kge-shu-lcof/
 * https://github.com/sisterAn/JavaScript-Algorithms/issues/59
 *
 * 动态数组可能会插入或删除元素，难道我们每次求 Top k 问题的时候都需要对数组进行重新排序吗？
 */

function getLeastNumbers(arr, k) {
  if (k === 0) return [];
  const len = arr.length;
  if (len <= 1) return arr;

  for (let i = Math.floor(len / 2 - 1); i >= 0; i--) {
    heapifyMin(arr, i, len);
  }

  for (let j = len - 1; j >= len - k; j--) {
    swap(arr, 0, j);
    heapifyMin(arr, 0, j);
  }

  console.log(arr);

  return arr.slice(-k).reverse();
}

function heapifyMin(arr, i, heapSize) {
  for (let j = 2 * i + 1; j < heapSize; j = 2 * j + 1) {
    if (j + 1 < heapSize && arr[j] > arr[j + 1]) {
      j++;
    }

    if (arr[i] > arr[j]) {
      swap(arr, i, j);
      i = j;
    } else {
      break;
    }
  }
}
```

# 用两个栈实现队列

```JS
/**
 * * 用两个栈实现队列
 * https://leetcode-cn.com/problems/yong-liang-ge-zhan-shi-xian-dui-lie-lcof/
 * https://github.com/sisterAn/JavaScript-Algorithms/issues/34
 * 双栈可以实现序列倒置
 */

const CQueue = function() {
  this.stack1 = [];
  this.stack2 = [];
};

// 入队元素push到栈1的顶部
CQueue.prototype.appendTail = function(value) {
  this.stack1.push(value);
};

// 出队时将栈2顶部出栈；若栈2空则先将栈1所有元素出栈放到栈2
CQueue.prototype.deleteHead = function() {
  if (this.stack2.length) {
    return this.stack2.pop();
  }

  if (!this.stack1.length) return -1;

  while (this.stack1.length) {
    this.stack2.push(this.stack1.pop());
  }

  // 删除队首元素
  return this.stack2.pop();
};
```

# 滑动窗口最大值问题
- 给定一个数组 nums 和滑动窗口的大小 k，请找出所有滑动窗口里的最大值。
- 大小为k的滑动窗口从数组的最左侧移动到数组的最右侧

```JS
/**
 * * 滑动窗口最大值问题。
 * https://leetcode-cn.com/problems/sliding-window-maximum/
 * https://github.com/sisterAn/JavaScript-Algorithms/issues/33
 * 暴力多重循环会超时
 */

// 使用一个双端队列存储窗口中值的索引 ，并且保证双端队列中第一个元素永远是最大值，那么只需要遍历一次 nums，就可以取到每次移动时的最大值。
function maxSlidingWindow2(nums, k) {
  // 存储窗口中值的索引，并且保证双端队列中第一个元素永远是最大值
  const deque = [];
  // 存放每个滑动窗口的最大值
  const result = [];

  for (let i = 0; i < nums.length; i++) {
    // 把滑动窗口之外的踢出
    if (i - deque[0] >= k) {
      deque.shift();
    }

    // 保证当队头出队时，新的队头依旧是最大值
    while (nums[deque[deque.length - 1]] <= nums[i]) {
      deque.pop();
    }

    deque.push(i);

    if (i >= k - 1) {
      // 依次把最大值（双端队列的队头）添加到结果 result 中
      result.push(nums[deque[0]]);
    }
  }

  return result;
}

const maxSlidingWindow = function(nums, k) {
  if (k === 1) return nums;

  let i = 0;
  const ret = [];

  while (i <= nums.length - k) {
    const max = Math.max(...nums.slice(i, i + k));
    ret.push(max);
    i++;
  }

  return ret;
};
```

# 有效的括号

```JS
/**
 * * 有效的括号
 * 给定一个只包括 '('，')'，'{'，'}'，'['，']' 的字符串 s ，判断字符串是否有效。
 * https://leetcode-cn.com/problems/valid-parentheses/
 * https://github.com/sisterAn/JavaScript-Algorithms/issues/25
 * 左括号必须用相同类型的右括号闭合。
 * 左括号必须以正确的顺序闭合
 */
function isValid(s) {
  // 注意左半边括号是key
  const map = {
    '{': '}',
    '(': ')',
    '[': ']',
  };

  const stack = [];

  for (let i = 0; i < s.length; i++) {
    if (map[s[i]]) {
      stack.push(s[i]);
    } else if (s[i] !== map[stack.pop()]) {
      // 只需判断右半边的括号顺序
      return false;
    }
  }

  return stack.length === 0;
}
```

# 删除字符串中的所有相邻重复项

```JS
/**
 * * 删除字符串中的所有相邻重复项。
 * https://leetcode-cn.com/problems/remove-all-adjacent-duplicates-in-string/
 * https://github.com/sisterAn/JavaScript-Algorithms/issues/26
 * 选择两个相邻且相同的字母，并删除它们。
 * 遍历字符串，依次入栈，入栈时判断与栈头元素是否一致，如果一致，即这两个元素相同相邻，则需要将栈头元素出栈，并且当前元素也无需入栈
 * * 扩展 删除字符串中出现次数 >= 2 次的相邻字符
 */
function removeDuplicates(s) {
  const stack = [];
  for (const c of s) {
    const prev = stack.pop();

    if (prev !== c) {
      stack.push(prev);
      stack.push(c);
    }
  }

  return stack.join('');
}
```

# 最小栈（包含getMin函数的栈）

```JS
/**
 * * 最小栈（包含getMin函数的栈）
 * https://leetcode-cn.com/problems/min-stack/
 * https://github.com/sisterAn/JavaScript-Algorithms/issues/23
 */

function MinStack() {
  this.items = [];
  this.min = null;
}

// 进栈
MinStack.prototype.push = function(x) {
  if (!this.items.length) this.min = x;
  this.min = Math.min(x, this.min);
  this.items.push(x);
};

// 出栈
MinStack.prototype.pop = function() {
  const num = this.items.pop();
  this.min = Math.min(...this.items);
  return num;
};

// 获取栈顶元素
MinStack.prototype.top = function() {
  if (!this.items.length) return null;
  return this.items[this.items.length - 1];
};

// 检索栈中的最小元素
MinStack.prototype.getMin = function() {
  return this.min;
};
```
