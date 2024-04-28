---
title: job-leetcode-repeat-everytime
tags: [algorithms, coding, job, leetcode, repeat]
created: 2021-09-21T19:40:24.161Z
modified: 2021-10-06T14:58:39.894Z
---

# job-leetcode-repeat-everytime

# guide

# 斐波那契数
- 该数列由 0 和 1 开始，后面的每一项数字都是前面两项数字的和。
  - `F(0) = 0，F(1) = 1` 前2项
  - `F(n) = F(n - 1) + F(n - 2)`，其中 n > 1

```JS
/**
 * * 斐波那契数列 fibonacci，如 f0=0, f1=1,f2=1,f3=2
 * * 思路：前2项预定义0、1，从i=2(即第3项)开始累加
 * https://leetcode-cn.com/problems/fibonacci-number/
 * * n从0开始
 */
function fibonacci(n) {
  // 处理 0、1
  if (n < 2) return n;

  // 记录前2个数
  let n1 = 0;
  let n2 = 1;

  let curr = 0;

  for (let i = 2; i < n + 1; i++) {
    curr = n1 + n2;
    n1 = n2;
    n2 = curr;
  }

  return curr;
}

/**
 * * 2次递归带来重复计算
 * https://blog.csdn.net/weixin_40170902/article/details/80835750
 */
function fibonacciRecursive(n) {

  // 处理 0、1；也是递归终止条件
  if (n < 2) return n;

  return fibonacciRecursive(n - 1) + fibonacciRecursive(n - 2);
}

/**
 * * 使用缓存优化fibonacci
 * - 优化的递归性能仍然不如循环
 * * cache中保存的是整个数列，但却缺前2项[,,1,2,3,5...]
 * https://segmentfault.com/a/1190000022973482
 */
function fibonacciRecursive(n, cache = []) {

  // 处理 0、1；递归终止条件
  if (n < 2) return n;

  if (cache[n]) return cache[n]

  cache[n] = fibonacciRecursive(n - 1, cache) + fibonacciRecursive(n - 2, cache);

  return cache[n];
}
```

# 两数之和

```JS
/**
 * * 两数之和。
 * 给定整数数组nums和整数目标值target，在该数组中找出和为目标值target的那两个整数，并返回它们的下标索引。
 * 假设每种输入只会对应一个答案。但是，数组中同一个元素在答案里不能重复出现。返回顺序任意
 * * 思路：用映射表存储 [元素值，元素索引]，然后求差找元素，再找索引
 * https://leetcode.cn/problems/two-sum/
 * https://github.com/sisterAn/JavaScript-Algorithms/issues/4
 */

function twoSum(nums, target) {
  const map = new Map();

  for (let i = 0; i < nums.length; i++) {
    const k = target - nums[i];

    if (map.has(k)) return [i, map.get(k)];

    // 存放 [元素值，索引下标]
    map.set(nums[i], i);
  }

  return [];
}
```

```JS
// 暴力法
function twoSum2(nums, target) {
  for (let i = 0; i < nums.length; i++) {
    for (let j = 0; j < nums.length; j++) {
      // 必须是2个不同的数
      if (i !== j && nums[i] + nums[j] === target) {
        return [i, j];
      }
    }
  }

  return [-1, -1];
}
```

# 三数之和

```js
/**
 * * 三数之和
 * * 思路：先排序 + 遍历元素curr(寻找curr+next+last的和为target的情况) 双指针夹逼相遇
 * 判断 nums 中是否存在三个元素 a，b，c ，请找出所有和为0且不重复的三元组。 答案中不可以包含重复的三元组。
 * https://leetcode.cn/problems/3sum/
 * https://github.com/sisterAn/JavaScript-Algorithms/issues/31
 */
function threeSum(nums, target=0) {
  nums.sort((a, b) => a - b);

  const ret = [];
  let second;
  let last;

  for (let i = 0; i < nums.length; i++) {
    // 因为是递增数组
    if (nums[i] > 0) break;

    if (i > 0 && nums[i] === nums[i - 1]) continue;

    second = i + 1;
    last = nums.length - 1;

    // 循环终止条件，因为是3个不同位置的元素
    while (second < last) {
      const sum = nums[i] + nums[second] + nums[last];

      if (sum < target) {
        second++;
        continue;
      }
      if (sum > target) {
        last--;
        continue;
      }

      // sum === 0

      ret.push([nums[i], nums[second], nums[last]]);

      // 去重
      while (second < last && nums[second] === nums[second + 1]) second++;
      while (second < last && nums[last] === nums[last - 1]) last--;

      second++;
      last--;
    }
  }

  return ret;
}
```

```JS
/**
 * * 利用两数和的思路，新建set去除重复元素；
 * 👎🏻️ 二维数组去重的时间/空间复杂度多过高，不推荐
 */
function threeSum(nums, target) {
  nums.sort((a, b) => a - b);

  const ret = [];
  const retSet = new Set();
  const map = new Map();

  for (let i = 0; i < nums.length - 2; i++) {
    const first = nums[i];

    // 下面就是求2数和的思路
    for (let j = i + 1; j < nums.length; j++) {
      // 第2个数
      const second = 0 - nums[j] - first;

      const maybeRet = [first, second, nums[j]].sort((a, b) => a - b);
      const maybeRetStr =
        String(String(maybeRet[0]) + maybeRet[1]) + maybeRet[2];

      if (map.has(second) && !retSet.has(maybeRetStr)) {
        ret.push([first, second, nums[j]]);
        retSet.add(maybeRetStr);
      }

      map.set(nums[j], j);
    }

    map.clear();
  }

  return ret;
}
```
