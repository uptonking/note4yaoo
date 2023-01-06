---
title: job-leetcode-array-stack-queue-heap
tags: [algorithms, coding, heap, job, leetcode, queue, stack]
created: 2021-09-21T19:40:24.161Z
modified: 2021-10-06T14:54:06.837Z
---

# job-leetcode-array-stack-queue-heap

# guide

# 用两个栈实现队列

```JS
/**
 * * 用两个栈实现队列
 * * 思路：双栈可以实现序列倒置
 * https://leetcode-cn.com/problems/yong-liang-ge-zhan-shi-xian-dui-lie-lcof/
 * https://github.com/sisterAn/JavaScript-Algorithms/issues/34
 */
const CQueue = function() {
  this.stack1 = [];
  this.stack2 = [];
};

// 入队元素push到栈1的顶部
CQueue.prototype.appendTail = function(value) {
  this.stack1.push(value);
};

// 👀️ 出队时将栈2顶部出栈；若栈2空则先将栈1所有元素出栈放到栈2再将顶部出栈
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
 * * 思路：双端队列。没必要一次性获取窗口内所有元素；
 * * 思路：
 * * - 逐个入队元素，若已有值索引在窗口范围之前，或已有值<=当前值，则去掉失效或不够大的已有元素。
 * * - 这样数组头部总是最大值，也就是当前滑动窗口的最大值。
 * * - 每次循环都能找到当前窗口的最大值并放在数组头部
 * https://leetcode-cn.com/problems/sliding-window-maximum/
 * https://github.com/sisterAn/JavaScript-Algorithms/issues/33
 */
function maxSlidingWindow2(nums, k) {
  // 存放每个滑动窗口的最大值
  const result = [];

  // 存储窗口中值的索引，双端队列中第一个元素永远是最大值，且是递减的
  const deque = [];

  for (let i = 0; i < nums.length; i++) {
    // 若头部元素在窗口范围之前，则需要去掉头部元素
    if (deque[0] < i - k + 1) {
      deque.shift();
    }

    // 小于当前元素的都不可能是当前滑动窗口的最大值，应该从尾部去掉，循环找到当前的最大值
    while (nums[deque[deque.length - 1]] <= nums[i]) {
      deque.pop();
    }

    // 将当前元素放到尾部
    deque.push(i);

    // 从第k个元素开始才构成滑动窗口
    if (i >= k - 1) {
      // 依次把最大值（队头）添加到结果 result 中
      result.push(nums[deque[0]]);
    }
  }

  return result;
}

// 暴力法，暴力多重循环会超时
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
 * * 碰到左括号就入栈对应的右括号，若当前元素是右括号但不是栈顶元素，就说明不是有效括号
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
 * * 思路：遍历字符串，依次入栈，入栈时判断与栈顶元素是否一致，如果一致，即这两个元素相同相邻，则需要将栈头元素出栈，并且当前元素也无需入栈
 * https://leetcode-cn.com/problems/remove-all-adjacent-duplicates-in-string/
 * https://github.com/sisterAn/JavaScript-Algorithms/issues/26
 * 选择两个相邻且相同的字母，并删除它们。
 * * 扩展 删除字符串中出现次数 >= 2 次的相邻字符
 */
function removeDuplicates(s) {
  if (s.length <= 1) return s;

  const stack = [s[0]];

  for (let i = 1; i < s.length; i++) {
    if (s[i] === stack[stack.length - 1]) {
      stack.pop();
    } else {
      stack.push(s[i])
    }
  }

  return stack.join('');
}
```

# 最小栈（包含getMin函数的栈）

```JS
/**
 * * 最小栈（包含getMin函数的栈）
 * * 思路：进栈时记录最小值，出栈时，更新最小值
 * 设计一个支持 push ，pop ，top 操作，并能在常数时间内检索到最小元素的栈。
 * https://leetcode-cn.com/problems/min-stack/
 * https://github.com/sisterAn/JavaScript-Algorithms/issues/23
 */

function MinStack() {
  this.items = [];
  this.min = null;
}

// 检索栈中的最小元素
MinStack.prototype.getMin = function() {
  return this.min;
};

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
```
