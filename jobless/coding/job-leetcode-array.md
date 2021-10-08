---
title: job-leetcode-array
tags: [algorithms, array, coding, job, leetcode]
created: '2021-10-05T09:00:35.959Z'
modified: '2021-10-06T14:45:51.381Z'
---

# job-leetcode-array

# guide

- 从数组中随机取一个元素的方法
  - `items[Math.floor(Math.random()*items.length)]`
# 合并两个有序数组
- 给你两个有序整数数组 nums1 和 nums2，请你将 nums2 合并到 nums1 中，使 num1 成为一个有序数组。

```JS
/**
 * * 合并2个有序数组，原地合并
 * * 思路：因为有序，所以可以从后向前处理，
 * https://leetcode-cn.com/problems/merge-sorted-array/
 */
function mergeTwoSortedArr(nums1, m, nums2, n) {
  let mm = m - 1;
  let nn = n - 1;

  let i = m + n - 1;

  while (nn >= 0) {

    // nums1元素值太大了，已经处理完全部放右边了
    if (mm < 0) {
      nums1[i--] = nums2[nn--];
      continue;
    }

    nums1[i--] = nums1[mm] < nums2[nn] ? nums2[nn--] : nums1[mm--];
  }

}
```

```JS
/**
 * * 合并两个数组，数组可无序；
 * * 思路是归并排序的合并部分算法
 * - m和n表示元素个数
 */
function mergeTwoArr(nums1, m, nums2, n) {
  const temp = [];
  const resultLen = m + n;

  // 两边都还有数组
  while (m && n) {
    if (nums1[0] < nums2[0]) {
      temp.push(nums1.shift());
      m--;
    } else {
      temp.push(nums2.shift());
      n--;
    }
  }

  // if (m > 0) temp.push(...nums1.slice(0, m));
  // if (n > 0) temp.push(...nums2.slice(0, n));
  temp = [...temp, ...nums1, ...nums2];

  // oj系统不支持直接修改
  // nums1 = temp;
  for (let i = 0; i < resultLen; i++) {
    nums1[i] = temp[i]
  }

  return nums1
}

// 以下是归并排序合并部分，作为参考
function mergeArrays2(nums1, m, nums2, n) {
  const temp = [];
  while (nums1.length && nums2.length) {
    if (nums1[0] <= nums2[0]) {
      temp.push(nums1);
    } else {
      temp.push(nums2);
    }
  }

  return [...temp, ...nums1, ...nums2];
}
```

# 数组的交集

```JS
/**
 * * 给定两个数组，编写一个函数来计算它们的交集。
 * 我们可以不考虑输出结果的顺序。
 * https://leetcode-cn.com/problems/intersection-of-two-arrays
 * https://github.com/sisterAn/JavaScript-Algorithms/issues/6
 */
function getIntersectionOfTwoArr(nums1, nums2) {
  // return [...new Set(nums1.filter((item) => nums2.includes(item)))];
  return Array.from(new Set(nums1.filter((item) => nums2.includes(item))))

}

// 标记法，用空间换时间
function intersection(nums1, nums2) {

  const map1 = {};
  const map2 = {};

  const result = [];

  nums1.forEach(item => {
    map1[item] = true;
  });

  nums2.forEach(item => {
    // map1中也存在，且map2中还没访问过
    if (map1[item] && !map2[item]) {
      result.push(item);
      map2[item] = true;
    }
  });

  return result;
}

function intersection(arr1, arr2) {
  // 用set可减少内存消耗，但时间并没有减少
  const set2 = new Set(arr2);
  return Array.from(new Set(arr1.filter(item => set2.has(item))));
}
```

```JS
/**
 * * 计算多个数组的交集。
 * * 思路：从最短数组开始找。
 * https://github.com/sisterAn/JavaScript-Algorithms/issues/10
 *
 */
function getIntersectionOfMultiArr(...arrays) {
  if (arrays.length === 1) return arrays[0];

  /** 寻找最短数组的索引下标 */
  let shortestArr = 0;
  for (let i = 0; i < arrays.length; i++) {
    if (arrays[i].length < arrays[shortestArr].length) {
      shortestArr = i;
    }
  }

  const restArr = arrays.splice(shortestArr, 1);
  return [
    ...new Set(
      arrays[shortestArr].filter((item) =>
        // Determines whether all the members of an array satisfy the specified test.
        restArr.every((arr) => arr.includes(item)),
      ),
    ),
  ];
}

function getIntersectionOfMultiArr2(...arrs) {

  return arrs.reduce(function(prev, cur) {

    return [...new Set(cur.filter((item) => prev.includes(item)))];
  });
}
```

# 打乱数组 洗牌算法

> 设计算法来打乱一个没有重复元素的整数数组。

```JS
/**
 * * 洗牌算法。打乱数组。
 * - Fisher-Yates 洗牌算法，
 *   - 时间复杂度： O(n) 空间复杂度：O(n)
 *   * 基本思想就是从原始数组中随机取一个之前没取过的数字到新的数组中
 * - Knuth-Durstenfeld shuffle
 *   - 在Fisher 等人的基础上对算法进行了改进，在原始数组上对数字进行交互，省去了额外O(n)的空间
 * https://leetcode-cn.com/problems/shuffle-an-array/
 * https://github.com/sisterAn/JavaScript-Algorithms/issues/74
 * https://leetcode-cn.com/problems/shuffle-an-array/solution/jing-dian-xi-pai-suan-fa-fisher-yates-shufflesuan-/
 * https://segmentfault.com/a/1190000039246947
 * 浅拷贝数组，利用random()方法重制数组下标索引。
 * 可用来实现音乐随机播放。
 *
 */
const Solution = function(nums) {
  this.nums = nums;
};

// reset会返回原数组
Solution.prototype.reset = function() {
  return this.nums;
};

// 每次洗牌都返回的是新数组
// Knuth-Durstenfeld Shuffle
// 将“删除”的数字移至数组末尾，即将每个被删除数字与最后一个未删除的数字进行交换。
Solution.prototype.shuffle = function() {
  // 每次拷贝数组
  const res = [...this.nums];
  const len = res.length;

  // * 从后往前，相当于每次随机取一个不重复的元素，放到数组末尾，尾部元素一直都是乱序的
  for (let i = len - 1; i >= 0; i--) {
    const randIndex = Math.floor(Math.random() * (i + 1));
    swap(res, randIndex, i);
  }

  return res;
};

// Fisher–Yates shuffle
function shuffle(arr) {
  let random;
  const newArr = [];

  // 重复直到所有元素都被删除。
  while (arr.length) {
    // 从第1个到剩余的未删除项（包含）之间选择一个随机数 k。
    random = Math.floor(Math.random() * arr.length);

    // 从剩余的元素中将第k个元素删除并取出，放到新数组中。
    newArr.push(arr[random]);

    // 从原数组中删除
    arr.splice(random, 1);
  }

  return newArr;
}

const swap = function(arr, i, j) {
  const temp = arr[i];
  arr[i] = arr[j];
  arr[j] = temp;
};
```

# 合并重叠区间，返回不重叠的区间
- 思路
  - 先排序
  - 然后尝试两两合并

```JS
/**
 * * 合并重叠区间，返回不重叠的区间。合并区间
 * * 思路：先排序，若前区间终点大于后区间起点，则合并，然后调整i循环合并
 * https://leetcode-cn.com/problems/merge-intervals/
 * https://leetcode-cn.com/problems/merge-intervals/solution/fei-chang-tong-yi-li-jie-de-qian-duan-ji-7mmv/
 */
function mergeRanges(intervals) {
  // 先按区间起点大小排序
  intervals.sort((a, b) => a[0] - b[0]);

  for (let i = 0; i < intervals.length - 1; i++) {
    // 若前一个区间的终点比后一个区间比后一个区间的起点大，则说明可以合并
    if (intervals[i][1] >= intervals[i + 1][0]) {
      const merged = [...intervals[i], ...intervals[i + 1]];
      const newRange = [Math.min(...merged), Math.max(...merged)];

      intervals.splice(i, 2, newRange);

      // 检查当前重新调整后的区间是否可以跟后面的合并，上面删除了2个插入了1个，如i由0变-1，然后i++又变0
      i--;
    }
  }

  return intervals;
}
```

# 区间子数组个数

```JS
/**
 * * 区间子数组个数
 * 求连续、非空且其中最大元素满足大于等于L小于等于R的子数组个数
 * https://leetcode-cn.com/problems/number-of-subarrays-with-bounded-maximum/
 * https://leetcode-cn.com/problems/number-of-subarrays-with-bounded-maximum/solution/javascripthua-dong-chuang-kou-fa-by-jack-108/
 */

function numSubarrayBoundedMax(nums, left, right) {

  let count = 0;
  //窗口中的最右边的 区间内元素的索引 lastLeft
  let lastLeft = -1;
  //窗口最左位置索引
  let left = -1;

  for (let i = 0; i < A.length; i++) {
    if (A[i] <= R) {
      if (A[i] >= L && A[i] <= R) {
        lastLeft = i
        count += i - left
      } else {
        count += lastLeft - left
      }
    } else {
      lastLeft = i
      left = i
    }

  }

  return count
}
```

# 分割数组为连续子序列

```JS
/**
 * * 分割数组为连续子序列。每个子序列都由连续整数组成。
 * https://leetcode-cn.com/problems/split-array-into-consecutive-subsequences/
 * https://github.com/sisterAn/JavaScript-Algorithms/issues/117
 */
const isPossible = function(nums) {
  const max = nums[nums.length - 1];
  // arr：存储原数组中数字每个数字出现的次数
  // tail：存储以数字num结尾的且符合题意的连续子序列个数
  const arr = new Array(max + 2).fill(0);
  const tail = new Array(max + 2).fill(0);
  for (const num of nums) {
    arr[num]++;
  }
  for (const num of nums) {
    if (arr[num] === 0) continue;
    else if (tail[num - 1] > 0) {
      tail[num - 1]--;
      tail[num]++;
    } else if (arr[num + 1] > 0 && arr[num + 2] > 0) {
      arr[num + 1]--;
      arr[num + 2]--;
      tail[num + 2]++;
    } else {
      return false;
    }
    arr[num]--;
  }
  return true;
};
```

# 反转数组

```JS
/**
 * * 反转字符数组。原地修改。可以抽象为更一般的反转数组。
 * * 思路：头尾双指针夹逼中间，逐次交换头尾
 * https://leetcode-cn.com/problems/reverse-string/
 */

function reverseString(s) {
  const len = s.length;
  let i = 0;
  let j = len - 1;

  while (i <= j) {
    const temp = s[i];
    s[i] = s[j];
    s[j] = temp;
    i++;
    j--;
  }

}

function reverseString(s) {
  const len = s.length;
  const mid = Math.floor(len / 2);

  let temp;

  for (let i = 0; i < mid; i++) {
    temp = s[i];
    s[i] = s[len - i - 1];
    s[len - i - 1] = temp;
  }
}
```
