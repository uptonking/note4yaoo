---
title: job-algs-base-search
tags: [algorithms, job, search]
created: '2021-09-24T19:46:46.653Z'
modified: '2021-09-24T19:47:03.031Z'
---

# job-algs-base-search

> Search Algorithms 经典查找算法

# guide
- 查找：根据给定的某个值，在查找表中确定一个其关键字等于给定值的数据元素（或记录）。
# Conclusions 总结
- 插值类查找
  - 二分查找、插值查找、斐波拉契查找
- 静态查找和动态查找
  - 静态或者动态都是针对查找表而言的
  - 动态表指查找表中有删除和插入操作的表
- 无序查找和有序查找
  无序查找：被查找数列有序无序均可
  有序查找：被查找数列必须为有序数列

- 查找算法小结
  - 除顺序查找外，其他算法的思路基本相同，先对数据按某种方法进行排序，然后使用相应的规则查找。

- 时间复杂度  
|   查找算法    |  平均时间复杂度  |   备注  |  
|:-----------:|:--------------:|:-------|  
|   顺序查找    | O(N)          |         |  
|   二分查找    | O(logN)       |         |  
|   插值查找    | O(log(logN)   |         |  
| 斐波那契查找   | O(logN)       |         |  
|   二叉查找树  | O(logN)        |         |  
|   分块查找    |  -            |         |  
|   哈希查找    | O(1)          |         |  

# 01 SequentialSearch 顺序查找
- 基本原理  
  - 顺序查找也称为线形查找，属于无序查找算法。
  - 从数据结构线形表的一端开始，顺序扫描，依次将扫描到的结点关键字与给定值k相比较，若相等则表示查找成功；
  - 若扫描结束仍没有找到关键字等于k的结点，表示查找失败。  
- 条件
  - 无序或有序队列
- 优点
  - 算法简单，对查找表的记录没有任何要求
- 缺点
  - 效率低下
- 适用
  - 数据量较少时的查找
  - 顺序查找适合于存储结构为顺序存储或链接存储的线性表
# 02 BinarySearch 二分查找

## 原理

- 实现思路
  - 查找过程从数组的中间元素开始  
  - 如果中间元素正好是要查找的元素，则搜素过程结束；
  - 如果某一特定元素大于或者小于中间元素，则在数组大于或小于中间元素的那一半中查找，而且跟开始一样从中间元素开始比较。
  - 如果在某一步骤数组为空，则代表找不到。
  - 这种搜索算法每一次比较都使搜索范围缩小一半。
- 二分的本质并非“单调性”，而是“边界”，只要找到某种性质，使得整个区间一分为二，那么就可以用二分把边界点二分出来。

- 条件 **有序**
  - 必须采用顺序存储
  - 必须按key大小有序排列
- 优点  
  - 比较次数少，查找速度快，平均性能好
- 缺点  
  - 要求待查表为有序表，且插入删除困难
- 适用  
  - 折半查找方法适用于 **不经常变动** 而查找频繁的有序列表  
  - 折半查找的 **前提条件** 是需要有序表顺序存储，对于静态查找表，一次排序后不再变化，折半查找能得到不错的效率。
  - 但对于需要频繁执行插入或删除操作的数据集来说，维护有序的排序会带来不小的工作量，那就不建议使用

## js实现

```JS
/** 💡️ 二分查找，非递归，low/high是索引号 */
function binarySearch(nums, target) {

  let low = 0;
  let high = nums.length - 1;

  while (low <= high) {
    let mid = Math.floor((low + high) / 2);
    if (nums[mid] === target) {
      return mid;
    }
    if (nums[mid] > target) {
      high = mid - 1;
    } else {
      low = mid + 1;
    }
  }

  return -1;
}

var arr = [-34, 1, 3, 4, 5, 8, 34, 45, 65, 87];
binarySearch(arr, 4);
```

```JS
/** 💡️ 二分查找，递归，low/high是索引号 */
function binarySearch(nums, target, low, high) {
  // high = high || nums.length - 1; // 不能这样写，因为递归调用时参数变化了
  if (low === undefined) {
    low = 0;
  }
  if (high === undefined) {
    high = nums.length - 1;
  }
  // 若参数数组只有1个元素，也应该执行比较，所以这里不能为=
  if (low > high) {
    return -1;
  }

  const mid = Math.floor((low + high) / 2);

  if (nums[mid] === target) {
    return mid;
  }

  if (nums[mid] > target) {
    // 注意 递归要return，漏写之后难以排查
    return binarySearch(nums, target, low, mid - 1)
  } else {
    return binarySearch(nums, target, mid + 1, high)
  }

}

var arr = [-34, 1, 3, 4, 5, 8, 34, 45, 65, 87];
console.log('--/--, ', binarySearch(arr, 4))
```

# 03 InsertSearch 插值查找
- 基本原理
  - 基于二分查找算法，将查找点的选择改进为自适应选择，可以提高查找效率，也属于有序查找。  
  - 二分查找中查找点计算：`mid = (low+high)/2, 即mid = low + 1/2*(high-low)` ; 
  - 通过类比，我们可以将查找的点改进为：`mid = low + (key-a[low])/(a[high]-a[low])*(high-low)` ; 
  - 也就是将上述的比例参数1/2改进为自适应的，根据关键字在整个有序表中所处的位置，让mid值的变化更靠近关键字key，这样也就间接地减少了比较次数。  
- 条件  
- 适用
  - 数据量较大，而关键字分布又比较均匀的查找表  
  - 对于表长较大，而关键字分布又比较均匀的查找表来说，插值查找算法的平均性能比折半查找要好的多。  
  - 反之，数组中如果分布非常不均匀，那么插值查找未必是很合适的选择
# 04 FibonacciSearch 斐波那契查找  
- 基本原理  
  - 黄金比例又称黄金分割，是指事物各部分间一定的数学比例关系，即将整体一分为二，较大部分与较小部分之比等于整体与较大部分之比，其比值约为1:0.618或1.618:1。  
  - 斐波那契数列：1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89…….（从第三个数开始，后边每一个数都是前两个数的和）。然后我们会发现，随着斐波那契数列的递增，前后两个数的比值会越来越接近0.618。  
  - 斐波那契查找也是二分查找的一种提升算法，通过运用黄金比例的概念在数列中选择查找点进行查找，提高查找效率，斐波那契查找也属于一种有序查找算法。  
  - 相对于折半查找，一般将待比较的key值与第mid=（low+high）/2位置的元素比较，比较结果分三种情况：  
    - `=`，mid位置的元素即为所求  
    - `>`，low=mid+1  
    - `<`，high=mid-1  
  - 斐波那契查找与折半查找很相似，是根据斐波那契序列的特点对有序表进行分割的，要求开始表中记录的个数为某个斐波那契数小1，即n=F(k)-1; 
  - 开始将k值与第F(k-1)位置的记录进行比较(及mid=low+F(k-1)-1), 比较结果也分为三种  
    - `=`，mid位置的元素即为所求  
    - `>`，low=mid+1, k-=2  
      - low=mid+1说明待查找的元素在[mid+1, high]范围内，k-=2 说明范围[mid+1, high]内的元素个数为n-(F(k-1))= Fk-1-F(k-1)=Fk-F(k-1)-1=F(k-2)-1个，所以可以递归的应用斐波那契查找。
    - `<`，high=mid-1,k-=1  
      - low=mid+1说明待查找的元素在[low,mid-1]范围内，k-=1 说明范围[low,mid-1]内的元素个数为F(k-1)-1个，所以可以递归 的应用斐波那契查找。```

- 条件  
- 优点  
  - 平均性能要比折半查找好；
- 缺点   
  - 要求待查找的查找表必须顺序存储并且有序，且需满足条件：如果一个有序表的元素个数为n，并且n正好是（某个斐波那契数-1), 时，才能用斐波那契查找法。
# 03 BinarySortTreeSearch 二叉查找树/排序树
- 基本原理  
  1)若b是空树，则搜索失败，否则：  
  2)若x等于b的根节点的数据域之值，则查找成功；否则：  
  3)若x小于b的根节点的数据域之值，则搜索左子树；否则：  
  4)查找右子树。  
- 条件  
  - 先创建二叉排序树：   
  1)若它的左子树不空，则左子树上所有结点的值均小于它的根结点的值；  
  2)若它的右子树不空，则右子树上所有结点的值均大于它的根结点的值；  
  3)它的左、右子树也分别为二叉排序树。

# 04 BlockSearch 分块查找
- 基本原理  
  - 根据键值方式(Key value)进行查找，通过散列函数，定位数据元素  
- 条件  
  - 先创建哈希表（散列表）

# 05 HashSearch 哈希查找
- 基本原理
  - 将n个数据元素"按块有序"划分为m块（m ≤ n）。
  - 每一块中的结点不必有序，但块与块之间必须"按块有序"，即第1块中任一元素的关键字都必须小于第2块中任一元素的关键字，而第2块中任一元素又都必须小于第3块中的任一元素，……  
  - 然后使用二分查找及顺序查找。
- 条件  
- 适用  
  - 数据本身是无法排序、无法比较  
  - Hash是一种典型以空间换时间的算法，比如原来一个长度为100的数组，对其查找，只需要遍历且匹配相应记录即可，
  - 从空间复杂度上来看，假如数组存储的是byte类型数据，那么该数组占用100byte空间。
  - 现在我们采用Hash算法，我们前面说的Hash必须有一个规则，约束键与存储位置的关系，那么就需要一个固定长度的hash表，此时，仍然是100byte的数组，假设我们需要的100byte用来记录键与位置的关系，那么总的空间为200byte, 而且用于记录规则的表大小会根据规则，大小可能是不定的。