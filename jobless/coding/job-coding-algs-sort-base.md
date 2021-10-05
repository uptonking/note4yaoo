---
title: job-coding-algs-sort-base
tags: [algorithms, coding, job, sort, leetcode]
created: '2021-10-05T10:09:53.229Z'
modified: '2021-10-05T10:10:07.435Z'
---

# job-coding-algs-sort-base

# guide

- 不必执着于哪个是性能最高的算法，影响排序的因素很多
  - 常见因素包括数量多少、极值分布、空间要求、稳定性等
  - 经常碰到数据预处理和类型转换比排序用时更多的情况

```JS
/** 交换数组中i,j两个索引位置的值 */
function swap(nums, i, j) {
  const temp = nums[i];
  nums[i] = nums[j];
  nums[j] = temp;
}

/**
 * * 数值数组排序测试模版；
 * * https://leetcode-cn.com/problems/sort-an-array/
 * @param {number[]} nums
 * @return {number[]}
 * 
 */
function arraySort(nums) {
  const len = nums.length;
  if (len <= 1) return nums;

  return nums;
};
```

# 快速排序

```JS
/** 交换数组中i,j两个索引位置的值 */
function swap(nums, i, j) {
  const temp = nums[i];
  nums[i] = nums[j];
  nums[j] = temp;
}

function quickSort(nums) {
  const len = nums.length;
  if (len <= 1) return nums;

  const pivotIndex = Math.floor(len / 2);
  const pivot = nums.splice(pivotIndex, 1)[0];

  const low = [];
  const high = [];

  // 这里要用nums.length，因为splice修改了nums数组
  for (let i = 0; i < nums.length; i++) {
    if (nums[i] < pivot) {
      low.push(nums[i]);
    } else {
      high.push(nums[i]);
    }
  }

  return [...quickSort(low), pivot, ...quickSort(high)];

  // leetcode oj实测，concat需要200ms，展开语法需要164ms
  // return quickSort(low).concat(pivot).concat(quickSort(high));
};
```

# 归并排序

```JS
/** 交换数组中i,j两个索引位置的值 */
function swap(nums, i, j) {
  const temp = nums[i];
  nums[i] = nums[j];
  nums[j] = temp;
}

function mergeSort(nums) {
  const len = nums.length;
  if (len <= 1) return nums;

  const mid = Math.floor(len / 2);

  const left = nums.slice(0, mid);
  const right = nums.slice(mid);

  return merge(mergeSort(left), mergeSort(right));
};

function merge(nums1, nums2) {

  const temp = [];

  while (nums1.length && nums2.length) {
    if (nums1[0] < nums2[0]) {
      temp.push(nums1.shift());
    } else {
      temp.push(nums2.shift());
    }
  }

  if (nums1.length) temp.push(...nums1);
  if (nums2.length) temp.push(...nums2);

  return temp;

  // 展开语法会列出所有元素，性能影响较大
  // return [...temp, ...nums1, ...nums2];
}
```

# 堆排序

```JS
/** 交换数组中i,j两个索引位置的值 */
function swap(nums, i, j) {
  const temp = nums[i];
  nums[i] = nums[j];
  nums[j] = temp;
}

function heapSort(nums) {
  const len = nums.length;
  if (len <= 1) return nums;

  for (let i = Math.floor(len / 2 - 1); i >= 0; i--) {
    heapifyMax(nums, i, len);
  }

  // 每次循环中未排序元素数量时 len-1
  for (let j = len - 1; j >= 0; j--) {
    swap(nums, 0, j);
    heapifyMax(nums, 0, j);
  }

  return nums;
};

function heapifyMax(nums, i, heapSize) {

  // 循环找出子节点的最大值，然后交换到堆顶
  for (let j = 2 * i + 1; j < heapSize; j = 2 * j + 1) {
    if (j + 1 < heapSize && nums[j] < nums[j + 1]) {
      j++;
    }

    if (nums[j] > nums[i]) {
      swap(nums, i, j);
      i = j;
    } else {
      break;
    }
  }
}
```
