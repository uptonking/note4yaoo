---
title: job-leetcode-sort-base
tags: [algorithms, coding, job, leetcode, sort]
created: '2021-10-05T10:09:53.229Z'
modified: '2021-10-06T14:47:12.319Z'
---

# job-leetcode-sort-base

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

/**
 * * 💡️ 快速排序，递归实现，非原地排序
 */
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

```JS
/**
 * * 💡️ 快速排序，递归版，原地排序
 * [用 JavaScript 实现快速排序](https://segmentfault.com/a/1190000037611587)
 */
export function quickSort(nums, start, end) {
  if (start === undefined) start = 0;
  if (end === undefined) end = nums.length - 1;

  if (start >= end) return;

  const pivotIndex = partition(nums, start, end);

  quickSort(nums, start, pivotIndex - 1);
  quickSort(nums, pivotIndex + 1, end);

  return nums;
}

/**
 * 重新排列数组的元素，使得基准值左侧的有元素都<基准值，而右侧的所有元素都>=基准值。
 * 这一步称为分区。
 */
function partition(nums, start, end) {
  // 每次分区都以最后一个元素作为基准值，最后一个元素就固定在最后，在遍历时不参与交换了
  const pivot = nums[end];

  // 用来确定将数组分为2部分时基准值对应的索引
  let pivotIndex = start;
  for (let i = start; i < end; i++) {
    if (nums[i] < pivot) {
      swap(nums, i, pivotIndex);
      pivotIndex++;
    }
  }

  // 将固定在末尾的基准值交换到两部分序列中间的基准位置
  swap(nums, pivotIndex, end);

  return pivotIndex;
}

```

# 归并排序

```JS
/** 交换数组中i,j两个索引位置的值 */
function swap(nums, i, j) {
  const temp = nums[i];
  nums[i] = nums[j];
  nums[j] = temp;
}

/**
 * * 💡️ 归并排序，递归实现，非原地排序
 */
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

```JS
export function mergeSortRecursively2(nums, start, end) {
  if (start === undefined) start = 0;
  if (end === undefined) end = nums.length - 1;

  if (start >= end) return;

  const mid = Math.floor((start + end) / 2);

  mergeSortRecursively2(nums, start, mid);
  mergeSortRecursively2(nums, mid + 1, end);

  let l = start;
  let r = mid + 1;
  const tempArr = [];

  while (l <= mid && r <= end) {
    if (nums[l] <= nums[r]) {
      tempArr.push(nums[l++]);
    } else {
      tempArr.push(nums[r++]);
    }
  }
  while (l <= mid) {
    tempArr.push(nums[l++]);
  }
  while (r <= end) {
    tempArr.push(nums[r++]);
  }

  // 将局部排好序的临时序列写回原数组
  for (l = start, r = 0; l <= end; l++, r++) {
    nums[l] = tempArr[r];
  }

  return nums;
}
```

# 堆排序 / 最大堆

```JS
/** 交换数组中i,j两个索引位置的值 */
function swap(nums, i, j) {
  const temp = nums[i];
  nums[i] = nums[j];
  nums[j] = temp;
}

/**
 * * 💡️ 堆排序，循环实现，原地排序
 */
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

```JS
/** 
 * * 💡️ heapSort 排序算法模版，递归版
 */
export function heapSortRecursive(nums) {
  const len = nums.length;
  if (len <= 1) {
    return nums;
  }

  for (let i = Math.floor(len / 2 - 1); i >= 0; i--) {
    heapifyMaxRecursive(nums, i, len);
  }

  for (let j = len - 1; j > 0; j--) {
    swap(nums, 0, j);
    // j可以代表本轮未排序元素个数
    heapifyMaxRecursive(nums, 0, j);
  }

  return nums;
}

function heapifyMaxRecursive(nums, i, heapSize) {
  const left = 2 * i + 1;
  const right = 2 * i + 2;
  let largest = i;

  if (left < heapSize && nums[left] > nums[largest]) {
    largest = left;
  }
  if (right < heapSize && nums[right] > nums[largest]) {
    largest = right;
  }

  if (largest !== i) {
    swap(nums, largest, i);
    heapifyMaxRecursive(nums, largest, heapSize);
  }
}
```

# 最小堆

```JS
/**
 * * 基于小顶堆求最小的k个数。
 * - 当k为arr长度时，可以得到逆序数组
 */
function heapSortMin(arr, k) {
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

# 希尔排序

```JS

export function shellSort(nums) {
  const len = nums.length;
  if (len <= 1) {
    return nums;
  }

  for (let gap = Math.floor(len / 2); gap >= 1; gap = Math.floor(gap / 2)) {
    for (let i = gap; i < len; i += gap) {
      for (let j = i; j > 0 && nums[j] < nums[j - gap]; j -= gap) {
        swap(nums, j, j - gap);
      }
    }
  }

  return nums;
}I
```
