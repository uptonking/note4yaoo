---
title: job-algs-base-sort
tags: [algorithms, job, sort]
created: '2021-09-24T19:46:02.713Z'
modified: '2021-09-24T19:46:42.224Z'
---

# job-algs-base-sort

> Sort Algorithms 经典排序算法

# guide
- tips
  - 不必执着于哪个是性能最高的算法，影响排序的因素很多
    - 常见因素包括数量多少、极值分布、空间要求、稳定性等
    - 会碰到数据处理和类型转换用的时间比排序用的时间更多

```JS
/**
 * 排序测试模版；
 * 在线oj测试 https://leetcode-cn.com/problems/sort-an-array/
 * @param {number[]} nums
 * @return {number[]}
 * 
 */
var sortArray = function(nums) {};
```

# Conclusions 总结
- 排序算法分类
  - 选择排序：直接选择排序、堆排序
  - 插入排序：直接插入排序、二分插入排序、希尔排序
  - 交换排序：冒泡排序、快速排序
  - 归并排序
  - 分配排序（非比较排序）：基数排序、计数排序、桶排序
  - 其他排序算法
    - 拓扑排序
    - 二分排序
- 时间复杂度
| 算法          | 平均时间复杂度    |空间复杂度  | 稳定性度  |   备注     |
| :-----------: |:-------------:|:--------:|:--------:|:----------|
| 选择排序      |    O(N2)          |   O(1)  |   F     |  n小好     |
| 堆排序        |    O(N*logN)      |   O(1)  |   F     |  n大好     |
| 插入排序      |    O(N2)          |   O(1)  |   ✅️     |大部分有序好 |
| 希尔排序      |    O(N^m) `1<m<2` |   O(1)  |   F      |           |
| 冒泡排序      |    O(N2)          |   O(1)  |   ✅️     |   n小好    |
| 快速排序      |    O(N*logN)      |O(logN)  |   F      |   n大好    |
| 归并排序      |    O(N*logN)      |   O(N)  |   ✅️     |    n大好   |
| 基数排序      |    O(d(r+N))      | O(rd+N) |   T      |           |
- 复杂度说明
  - 桶排序平均时间复杂度也为O(N)
- 排序算法总结
  - 平均速度最快：快速排序
  - 所需辅助空间最少：堆排序
  - 所需辅助空间最多/非就地排序：归并排序
  - 具有稳定性的排序算法：插入排序、冒泡排序、归并排序
- 稳定性
  - 假定在待排序的记录序列中存在多个具有相同的关键字的记录，
  - 若经过排序，这些记录的相对次序保持不变则称这种排序算法是稳定的，否则称为不稳定的
- 原地性
  - 原地排序就是指在排序过程中不申请多余的存储空间，只利用原来存储待排数据的存储空间进行比较和交换的数据排序
- 影响排序效果的因素
  - 待排序的记录数目n
  - 记录的大小
  - 关键字的结构及其初始状态
  - 对稳定性的要求
  - 语言工具的条件
  - 存储结构
  - 时间和辅助空间复杂度等
- 方法选择  
  - 若n较小(如n≤50)，可采用直接插入或直接选择排序。
    - 当记录规模较小时，直接插入排序较好；
    - 否则因为直接选择移动的记录数少于直接插入，应选直接选择排序为宜。
  - 若文件初始状态基本有序(指正序)，则应选用直接插人、冒泡或随机的快速排序为宜；
  - 若n较大，则应采用时间复杂度为O(nlogn)的排序方法：快速排序、堆排序或归并排序。
    - 快速排序是目前基于比较的内部排序中**被认为是最好**的方法，当待排序的关键字是随机分布时，快速排序的平均时间最短；
    - 堆排序所需的辅助空间少于快速排序，并且不会出现快速排序可能出现的最坏情况。这两种排序都是不稳定的。  
    - 若要求排序稳定，则可选用归并排序。
      - 但本章介绍的从单个记录起进行两两归并的排序算法并不值得提倡，通常可以将它和直接插入排序结合在一起使用。
      - 先利用直接插入排序求得较长的有序子文件，然后再两两归并之。
      - 因为直接插入排序是稳定的，所以改进后的归并排序仍是稳定
- 参考资料
  - [Java常用排序算法-程序员必须掌握的8大排序算法](http://blog.csdn.net/qy1387/article/details/7752973)  
  - [八大排序算法总结与java实现](https://itimetraveler.github.io/2017/07/18/%E5%85%AB%E5%A4%A7%E6%8E%92%E5%BA%8F%E7%AE%97%E6%B3%95%E6%80%BB%E7%BB%93%E4%B8%8Ejava%E5%AE%9E%E7%8E%B0/)  
# 01 SelectionSort 选择排序

## 原理

- 实现思路
  - 在要排序的一组数中，选出最小的一个数与第一个位置的数交换；
  - 然后在剩下的数当中再找最小的与第二个位置的数交换，如此循环到倒数第二个数和最后一个数比较为止。
- 思路有点类似插入排序，也分已排序区间和未排序区间。
  - 但是选择排序每次会从未排序区间中找到最小的元素，将其放到已排序区间的末尾。
- 特征
**条件**
- 优点
- 缺点
 
- 应用场景
- 锦标赛排序
  - 两两比较，不足补无穷大，小的作为根，构造树
- 没必要用
- 复杂度O(logN)

## js实现

```JS
/** 💡️ 内层循环仅选出最小索引但不交换 */
function selectionSort(nums) {
  // 每次循环处理从i开始的元素序列
  for (let i = 0; i < nums.length - 1; i++) {
    // 每次循环要找出最小元素的索引
    let min = i;
    for (let j = i; j < nums.length; j++) {
      if (nums[j] < nums[min]) {
        min = j;
      }
    }
    let temp = nums[i];
    nums[i] = nums[min];
    nums[min] = temp;
  }
  return nums
}

// 减少了内层循环的计算量
function selectionSort2(nums) {
  // 第i个未排序的元素
  for (let i = 0; i < nums.length - 1; i++) {
    let j = i;
    // 每次循环要找出最小元素的索引
    let min = j;
    while (j < nums.length) {
      // 在内层循环中每次选出最小的
      if (nums[j] < nums[min]) {
        min = j;
      }
      j++;
    }
    // 将最小的元素交换到第i个位置，i及其左边都是排好序的了
    let temp = nums[i];
    nums[i] = nums[min];
    nums[min] = temp;
  }
  return nums
}
```

- ref
  - [选择排序](https://github.com/doocs/leetcode/blob/main/basic/sorting/SelectionSort/README.md)
# 02 insertionSort 直接插入排序

## 原理

- 实现思路
  - 在要排序的一组数中，假设前面(n-1)[n>=2]个数已经是排好顺序的，现在要把第n个数插到前面的有序数中，使得这n个数也是排好顺序的。
  - 如此反复循环，直到全部排好顺序。
  - 在插入排序中，经过每一轮的排序处理后，数组前端的数是排好序的。
- 特征
**条件**
 
- 优点
- 缺点
 
- 应用场景

## js实现

```JS
/** 💡️ 从后往前逐个比较并交换 */
function insertionSort(nums) {
  // 将第i项作为待插入项
  for (let i = 1; i < nums.length; i++) {
    for (let j = i; j > 0 && nums[j] < nums[j - 1]; j--) {
      let temp = nums[j];
      nums[j] = nums[j - 1];
      nums[j - 1] = temp;
    }
  }
  return nums;
}

function insertionSort2(nums) {
  // 将数组第1个元素看成有序序列，开始处理第2,3,4...个元素
  for (let i = 1; i < nums.length; i++) {
    // 每次循环都要将当前项插入到有序序列的正确位置
    let temp = nums[i];
    let j = i - 1;
    // 从已排好序的前段数组的末尾开始，将比较项往前移
    while (nums[j] > temp && j > 0) {
      nums[j + 1] = nums[j];
      j--;
    }
    // 若temp比所有项都大，则放在已排好序的末尾
    nums[j + 1] = temp;
  }
  return nums;
}
```

- ref
  - [插入排序](https://github.com/doocs/leetcode/blob/main/basic/sorting/InsertionSort/README.md)
# 03 ShellSort 希尔排序

## 原理

- 实现思路
  - 先将要排序的一组数按某个增量d（n/2, n为要排序数的个数）分成若干组，每组中记录的下标相差d. 
  - 对每组中全部元素进行直接插入排序，然后再用一个较小的增量（d/2）对它进行分组，在每组中再进行直接插入排序。
  - 当增量减到1时，进行直接插入排序后，排序完成
- 希尔排序，也被称为递减增量排序，是简单插入排序的一种改进版本。
  - 在插入排序中，如果待排序列中的某个元素，距离有序数列中待插入位置非常远，就需要比较很多次才可以到达插入位置
  - 希尔排序就是先把整个序列排得相对比较有序，再进行插入排序的时候，需要比较的次数就会变得很少。
  - 插入排序的增量(间隔)为 1，希尔排序相当于将这个间隔从最大为数组长度的一半一直降到 1
  - 希尔排序就是将处在相同间隔的元素提取出来单独进行插入排序，然后逐步将间隔减小到 1 的过程。
- 特征
**时间复杂度** 
**空间复杂度** 
**条件**
 
- 优点
- 缺点
 
- 应用场景

## js实现

```JS
/** 💡️ 注意边界条件要正确处理，思路与直接插入排序基本相同 */
function shellSort(nums) {
  const len = nums.length;
  for (let gap = Math.floor(len / 2); gap >= 1; gap = Math.floor(gap / 2)) {
    for (let i = gap; i < len; i += gap) {
      for (let j = i; j > 0 && nums[j] < nums[j - gap]; j -= gap) {
        const temp = nums[j];
        nums[j] = nums[j - gap];
        nums[j - gap] = temp;
      }
    }
  }
  return nums;
}

function shellSort(nums) {
  const len = nums.length;
  let gap = Math.floor(len / 2);
  while (gap > 0) {
    for (let i = gap; i < len; i++) {
      let temp = nums[i];
      for (let j = i; j > 0 && nums[j] < nums[j - gap]; j -= gap) {
        const temp = nums[j];
        nums[j] = nums[j - gap];
        nums[j - gap] = temp;
      }
    }
    gap = Math.floor(gap / 2);
  }
  return nums;
}
```

- ref
  - [希尔排序](https://github.com/doocs/leetcode/blob/main/basic/sorting/ShellSort/README.md)
# 04 MergeSort 归并排序

## 原理

- 实现思路
  - 归并排序的核心思想是分治，把一个复杂问题拆分成若干个子问题来求解。
  - 把数组从中间划分为两个子数组，一直递归地把子数组划分成更小的数组，直到子数组里面只有1个元素的时候开始排序。
  - 排序的方法就是按照大小顺序合并两个元素。接着依次按照递归的顺序返回，不断合并排好序的数组，直到把整个数组排好序。
- 特征
**时间复杂度** 
**空间复杂度** 
**条件**
 
- 优点
- 缺点
 
- 应用场景
- Top K 问题
  - 堆化，取前 K 个元素
- 中位数问题
  - 维护两个堆，一大（前50%）一小（后50%），奇数元素取大顶堆的堆顶，偶数取取大、小顶堆的堆顶

- ref
  - [前端进阶算法9： 堆排序、Top K、中位数问题](https://github.com/sisterAn/JavaScript-Algorithms/issues/60)

## js实现

```JS
/** 💡️ 先递归的拆分数组，再两两合并  */
function mergeSort2(nums) {
  const len = nums.length;
  if (len === 1) {
    return nums;
  }
  const mid = Math.floor(len / 2);
  const lnums = nums.slice(0, mid);
  const rnums = nums.slice(mid);
  return merge(mergeSort(lnums), mergeSort(rnums));
}

function merge(lnums, rnums) {
  // 临时的有序数组，一直存放到两个数组中有一个为空
  const arr = [];
  while (lnums.length && rnums.length) {
    if (lnums[0] < rnums[0]) {
      arr.push(lnums.shift())
    } else {
      arr.push(rnums.shift())
    }
  }
  return [...arr, ...lnums, ...rnums]
  // return arr.concat(lnums).concat(rnums);
}
```

```JS
/** 先拆分数组到只有1个元素，然后相邻两两合并 */
function mergeSort(nums, left, right) {
  if (left >= right) {
    return
  }
  // (left+right) >> 1
  let mid = Math.floor((left + right) / 2);
  mergeSort(nums, left, mid);
  mergeSort(nums, mid + 1, right);
  let i = left;
  let j = mid + 1;
  let k = 0;
  let temp = [];
  // 把较小的数先移到新数组中
  while (i <= mid && j <= right) {
    if (nums[i] < nums[j] > ) {
      temp[k++] = nums[i++];
    } else {
      temp[k++] = nums[j++]
    }
  }
  // 把左边剩余的数移入数组
  while (i <= mid) {
    temp[k++] = nums[i++]
  }
  // 把右边边剩余的数移入数组
  while (j <= right) {
    temp[k++] = nums[j++]
  }
  // 把新数组中的数覆盖nums数组
  for (let x = left, y = 0; x <= right; x++, y++) {
    nums[x] = temp[y]
  }
}
```

- ref
  - [用 JavaScript 实现归并排序](https://segmentfault.com/a/1190000037697664)
  - [JavaScript实现归并排序-递归法与非递归法](https://blog.csdn.net/q918922703_1/article/details/101211914)
# 05 QuickSort 快速排序

## 原理

- 实现思路
  - 选择一个基准元素, 通常选择第一个元素或者最后一个元素, 通过一趟扫描，将待排序列分成两部分, 
  - 一部分比基准元素小, 一部分大于等于基准元素, 此时基准元素在其排好序后的正确位置, 然后再用同样的方法递归地排序划分的两部分。
- 快速排序也采用了分治的思想
  - 把原始的数组筛选成较小和较大的两个子数组，然后递归地排序两个子数组。
- 特征
**时间复杂度** 
**空间复杂度** 
**条件**
 
- 优点
- 缺点
 
- 应用场景
  - 快速排序，枢纽元如果是重复的值，选择不同位置的相同元素，就可能破坏次序。

## js实现

```JS
/**  💡️ splice+concat  */
function quickSort(nums) {
  if (nums.length <= 1) {
    return nums;
  }
  let pivotIndex = Math.floor(nums.length / 2);
  // 从数组中去掉基准值，并获取这个基准值
  let pivot = nums.splice(pivotIndex, 1)[0];
  let left = [];
  let right = [];
  for (let i = 0; i < nums.length; i++) {
    if (nums[i] < pivot) {
      left.push(nums[i])
    } else {
      right.push(nums[i])
    }
  }
  return [...quickSort(left), pivot, ...quickSort(right)]
  // return quickSort(left).concat([pivot], quickSort(right));
}

// 未实现，待改进
function quickSort2(nums, left, right) {
  if (nums.length <= 1) {
    return nums;
  }
  if (left >= right) {
    return;
  }
  // 选定一个基准值，这里选择中间位置
  let pivot = nums[Math.floor((left + right) / 2)];
  let i = left;
  let j = right;
  while (i < j) {
    while (nums[++i] < pivot);
    while (nums[--j] > pivot);
    if (i < j) {
      let temp = nums[i];
      nums[i] = nums[j]
      nums[j] = temp;
    }
  }
  quickSort(nums, left, j);
  quickSort(nums, j + 1, right);
}
```

```JS
/**
 * 快排 
 * @param {*} p  起始下标
 * @param {*} r  结束下标 + 1
 */
function quickSort(A, p = 0, r) {
  r = r || A.length;
  if (p < r - 1) {
    const q = divide(A, p, r);
    quickSort(A, p, q);
    quickSort(A, q + 1, r);
  }
  return A;
}
/**
 *
 * @param {*} p  起始下标
 * @param {*} r  结束下标 + 1
 */
function divide(A, p, r) {
  // 基准点
  const pivot = A[r - 1];
  // i初始化是-1，也就是起始下标的前一个
  let i = p - 1;
  for (let j = p; j < r - 1; j++) {
    // 如果比基准点小就i++，然后交换元素位置
    if (A[j] <= pivot) {
      i++;
      swap(A, i, j);
    }
  }
  // 最后将基准点插入到i+1的位置
  swap(A, i + 1, r - 1);
  // 返回最终指针i的位置
  return i + 1;
}

function swap(A, i, j) {
  const t = A[i];
  A[i] = A[j];
  A[j] = t;
}
```

- ref
  - [js算法-快速排序(Quicksort)](https://segmentfault.com/a/1190000017814119)
# 06 HeapSort 堆排序

## 原理

- 实现思路
  - 初始时把要排序的数的序列看作是一棵顺序存储的二叉树，调整它们的存储顺序，使之成为一个堆，这时堆的根节点的数最大。
  - 然后将根节点与堆的最后一个节点交换。然后对前面(n-1)个数重新调整使之成为堆。
  - 依此类推，直到只有两个节点的堆，并对它们作交换，最后得到有n个节点的有序序列。
  - 从算法描述来看，堆排序需要两个过程，一是建立堆，二是堆顶与堆的最后一个元素交换位置。
  - 所以堆排序有两个函数组成。一是建堆的渗透函数，二是反复调用渗透函数实现排序的函数。  
  - 堆的存储： 堆由数组来实现，相当于对二叉树做层序遍历。
  - 对于结点i(i为节点所在数组的索引号)，其子结点为 2i+1 与 2i+2，其父节点为 Math.floor((i+1)/2))-1 或 Math.ceil(i/2)-1 
- 特征
**时间复杂度** 
**空间复杂度** 
**条件**
 
- 优点
- 缺点
 
- 应用场景

## js实现

```JS
function heapSort(nums) {
  const len = nums.length;

  // 从后往前初始化大顶堆，从第一个非叶子结点开始，i代表可作为子树根节点的非叶子节点
  for (let i = Math.floor(len / 2 - 1); i >= 0; i--) {
    shiftDown(nums, i, len);
  }

  // 排序，每一次for循环找出一个当前最大值
  for (let i = len - 1; i > 0; i--) {
    // 将根节点与当前最后一个节点交换
    swap(nums, 0, i);
    // 从根节点开始调整，再次构建大顶堆
    shiftDown(nums, 0, i);
  }

}

/** 将i结点以下的堆整理为大顶堆，注意这一步实现的基础实际上是：假设结点i以下的子堆已经是一个大顶堆；
 * 将i节点与i节点的子节点中较大的交换，最后i节点位置的值是i原值、左右子节点值中最大的那个值
 */
function shiftDown(nums, i, length) {
  // 当前节点作为父节点，准备调换到堆中正确的位置
  let temp = nums[i];

  // 找到i的子节点中值最大的j
  for (let j = 2 * i + 1; j < length; j = 2 * j + 1) {
    temp = nums[i];
    if (j + 1 < length && nums[j] < nums[j + 1]) {
      j++; // 找到左右子节点中更大的那个
    }

    // /如果父节点i小于子节点j，则交换；否则跳出
    if (nums[j] > temp) {
      // 交换较大值到位置i
      swap(nums, i, j);
      i = j;
    } else {
      break;
    }
  }
}

function swap(A, i, j) {
  let temp = A[i];
  A[i] = A[j];
  A[j] = temp;
}
```

```JS
// ! 实现有问题
function heapSort(nums) {

  const len = nums.length

  for (let i = 0; i < len - 1; i++) {
    buildMaxHeap((nums, len - 1 - i))

    //交换堆顶和数组末位元素
    let temp = nums[0];
    nums[0] = nums[len - 1 - i];
    nums[len - 1 - i] = temp;
  }
}

function buildMaxHeap(nums, lastIndex) {

  //从lastIndex处节点即最后一个节点的父节点开始
  for (let i = Math.floor((lastIndex - 1) / 2); i >= 0; i--) {
    // 保存正在判断的节点，循环到父节点都比字节点大
    for (let j = i; 2 * j + 1 <= lastIndex;) {

      // j节点的值最大的子节点，默认是左子节点
      let biggerChild = 2 * j + 1;

      if (biggerChild < lastIndex && nums[biggerChild] < nums[biggerChild + 1]) {
        biggerChild++;
      }

      if (nums[j] < nums[biggerChild]) {
        let temp = nums[j];
        nums[j] = nums[biggerChild];
        nums[biggerChild] = temp;

        //将biggerIndex赋予k，开始while循环的下一次循环，重新保证k节点的值大于其左右子节点的值
        j = biggerChild;
      } else {
        break;
      }

    }

  }

}
```

- ref
  - [JS实现堆排序](https://segmentfault.com/a/1190000015487916)
# 07 BubbleSort 冒泡排序

## 原理

- 实现思路
  - 比较每相邻两个数，如果前者大于后者，就把两个数交换位置；这样一来，第一轮就可以选出一个最大的数放在最后面
- 特征
**时间复杂度** 
**空间复杂度** 
**条件**
 
- 优点
- 缺点
 
- 应用场景

## js实现

```JS
/** 💡️ 将较大值后移 */
function bubleSort(nums) {
  let swapped = false;
  for (let i = 0; i < nums.length - 1; i++) {
    swapped = false;
    for (let j = 0; j < nums.length - 1 - i; j++) {
      if (nums[j] > nums[j + 1]) {
        const t = nums[j];
        nums[j] = nums[j + 1];
        nums[j + 1] = t;
        swapped = true;
      }
    }
    // 如果某次循环完后，没有任何两数进行交换，就将标志位设置为 true，表示排序完成
    if (!swapped) break;
  }
  return nums;
}
/** 将较小值前移 */
function bubleSort2(nums) {
  for (let i = 0; i < nums.length - 1; i++) {
    for (let j = i; j < nums.length; j++) {
      if (nums[j] < nums[i]) {
        // 双重循环内的计算量会变得很大
        const t = nums[i];
        nums[i] = nums[j];
        nums[j] = t;
      }
    }
  }
  return nums;
}
```

# 08 RadixSort 基数排序
- 基本原理
  - 将所有待比较数值（正整数）统一为同样的数位长度，数位较短的数前面补零。
  - 然后，从最低位开始，依次进行一次排序。这
  - 样从最低位排序一直到最高位排序完成以后, 数列就变成一个有序序列。
- 基数排序按照优先从高位或低位来排序有两种实现方案：
  - MSD（Most significant digital）   
    - 从最左侧高位开始进行排序。先按k1排序分组, 同一组中记录, 关键码k1相等, 再对各组按k2排序分成子组,
    -  之后, 对后面的关键码继续这样的排序分组, 直到按最次位关键码kd对各子组排序后. 再将各组连接起来, 便得到一个有序序列。  
    - MSD方式适用于位数多的序列。
  - LSD （Least significant digital）  
    - 从最右侧低位开始进行排序。先从kd开始排序，再对kd-1进行排序，依次重复，直到对k1排序后便得到一个有序序列。  
    - LSD方式适用于位数少的序列。
- 特征
**时间复杂度** 
**空间复杂度** 
**条件**
 
- 优点
- 缺点
 
- 应用场景
# 09 CountingSort 计数排序
- 基本原理
- 特征
  - 计数排序不是比较排序，排序的速度快于任何比较排序算法。  
  - 当输入的元素是n个0到k之间的整数时，它的运行时间是O(n+k)。  
**时间复杂度** 
**空间复杂度** 
- **条件**
  - 只针对0和正整数
- 优点
- 缺点
 
- 应用场景
- 计数排序需要占用大量空间，它仅适用于数据比较集中的情况
  - 计数排序对于数据范围很大的数组，需要大量时间和内存，适用性不高。  
  - 例如：计数排序是用来排序0到100之间的数字的最好的算法，但是它不适合按字母顺序排序人名。  
  - 但计数排序可以用在基数排序中的算法来排序数据范围很大的数组。  
  - 当输入的元素是 n 个 0 到 k 之间的整数时，它的运行时间是 Θ(n + k)。

# 10 BucketSort 桶排序
- 基本原理
- 桶排序，也称箱排序，使用分治的思想  
  a. 将待排序的数据按映射函数分成连续的若干段，最好使数据平均分布  
  b. 确定桶数量  
  c. 每个桶内部排序  
  d. 按顺序输出数据  
- 假设数组元素最大值和最小值分别为max和min，则桶的个数为max - min + 1，
  - 也即数组区间[min, max]每个元素和桶下标区间[0, max - min + 1]中每个元素一一对应，这也是桶排序的核心思想。
- 特征
**时间复杂度** O(M+N) M是桶个数（一般为最大数），N是待排序个数
**空间复杂度** O(n)
**条件**
 
- 优点
- 缺点
 
- 应用场景
