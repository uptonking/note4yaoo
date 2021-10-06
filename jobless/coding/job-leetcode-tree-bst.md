---
title: job-leetcode-tree-bst
tags: [bst, job, leetcode, tree]
created: '2021-10-06T17:25:04.121Z'
modified: '2021-10-06T17:25:25.427Z'
---

# job-leetcode-tree-bst

# guide
- 二叉搜索树的一个重要的特性是中序序列是升序的
# 合法二叉搜索树

```JS
/**
 * * 检查一棵树是否为合法二叉搜索树。
 * * 思路: 递归比较根节点和左右
 * https://leetcode-cn.com/problems/legal-binary-search-tree-lcci/
 */
function isValidBST(root) {
  // 判断是否在界限内部
  function isValidBSTCore(root, lower, upper) {
    // 如果是null，则返回 true
    if (root === null) return true;
    // 右子树节点的比较
    if (lower !== null && root.val <= lower) return false;
    // 左子树节点的比较
    if (upper !== null && root.val >= upper) return false;
    // 对子树进行递归; 左子树都要比根节点小，右子树都要比根节点大
    return isValidBSTCore(root.left, lower, root.val) && isValidBSTCore(root.right, root.val, upper);
  }
  return isValidBSTCore(root, null, null)
}
```

```JS
/**
 * * 思路：bst中序遍历的结果是升序
 */
export function isValidBST(root) {
  if (!root) return true;
  const stack = [];
  let current = root;
  let prev;
  while (stack.length || current) {
    while (current) {
      stack.push(current);
      current = current.left;
    }
    // 最下方的左节点
    current = stack.pop();
    if (prev && prev.val >= current.val) {
      return false;
    }
    prev = current;
    current = current.right;
  }
  return true;
}
```

# 将有序数组转换为二叉搜索树
- 给你一个整数数组 nums ，其中元素已经按 升序 排列，请你将其转换为一棵 高度平衡 二叉搜索树。

```JS
/**
 * * 将有序数组转换为二叉搜索树
 * * 思路：数组中间位置作为根节点，递归构建
 * https://leetcode-cn.com/problems/convert-sorted-array-to-binary-search-tree/
 *
 */
function sortedArrayToBST(nums) {
  const len = nums.length;
  if (!nums || len === 0) return null;
  if (len === 1) return new TreeNode(nums[0]);
  const mid = Math.floor(len / 2);
  const root = new TreeNode(nums[mid]);
  root.left = sortedArrayToBST(nums.slice(0, mid));
  root.right = sortedArrayToBST(nums.slice(mid + 1));
  return root;
}
```

# 二叉搜索树中第 K 小的元素

```JS
/**
 * * 二叉搜索树中第K小的元素
 * * 思路：中序遍历二叉搜索树，输出第 k 个既可
 * https://leetcode-cn.com/problems/kth-smallest-element-in-a-bst/
 * https://github.com/sisterAn/JavaScript-Algorithms/issues/86
 */
export function kthSmallest(root, k) {
  if (!root) return -1;
  const stack = [];
  let current = root;
  // 遍历一个就加一
  let i = 0;
  while (stack.length || current) {
    while (current) {
      stack.push(current);
      current = current.left;
    }
    current = stack.pop();
    i++;

    if (i === k) return current.val;

    current = current.right;
  }
}
```

# 实现一个二叉搜索树迭代器

```JS
/**
 * * 二叉搜索树迭代器
 * https://leetcode-cn.com/problems/binary-search-tree-iterator/
 * - 使用二叉搜索树的根节点初始化迭代器。
 * - 调用 next() 将返回二叉搜索树中的下一个最小的数。
 * -
 */
function BSTIterator(root) {
  /** 存放升序序列 */
  this.vals = [];

  // 必须用箭头函数，否则this指向错误，this.vals不存在
  const inOrder = (node) => {
    if (node) {
      inOrder(node.left);
      this.vals.push(node.val);
      inOrder(node.right);
    }
  };

  inOrder(root);
}

BSTIterator.prototype.next = function() {
  return this.vals.shift();
};

BSTIterator.prototype.hasNext = function() {
  return this.vals.length > 0;
};
```
