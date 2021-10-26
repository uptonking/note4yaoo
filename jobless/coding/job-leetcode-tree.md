---
title: job-leetcode-tree
tags: [algorithms, coding, job, leetcode, tree]
created: '2021-10-05T09:02:06.952Z'
modified: '2021-10-06T14:54:23.456Z'
---

# job-leetcode-tree

# guide

```JS
// 二叉树的节点定义
function TreeNode(val, left, right) {
  this.val = val === undefined ? 0 : val;
  this.left = left === undefined ? null : left;
  this.right = right === undefined ? null : right;
}
```

# 翻转二叉树

```JS
/**
 * * 翻转二叉树。二叉树的左右子树交换
 * * 思路：从根节点开始前序遍历每个节点，然后交换左右子树既可
 * https://leetcode-cn.com/problems/invert-binary-tree/
 */
export function invertTree(root) {
  if (!root) return null;

  const temp = root.left;
  root.left = root.right;
  root.right = temp;

  invertTree(root.left);
  invertTree(root.right);

  return root;
}
```

# 判断平衡的二叉树
- 一个二叉树每个节点的左右两个子树的高度差的绝对值不超过1。
  - AVL树是指左右子树深度差不超过1的二叉树

```JS
/**
 * * 判断平衡的二叉树。
 * * 思路：自顶向下的比较每个节点的左右子树的最大高度差，如果二叉树中每个节点的左右子树最大高度差
 * 小于等于1 ，即每个子树都平衡时，此时二叉树才是平衡二叉树
 * https://github.com/sisterAn/JavaScript-Algorithms/issues/44
 */
export function isBalanced(root) {
  if (!root) return true;

  const getDepth = (node) => {
    if (!node) return 0;
    return Math.max(getDepth(node.left), getDepth(node.right)) + 1;
  };

  return (
    Math.abs(getDepth(root.left) - getDepth(root.right)) <= 1 &&
    isBalanced(root.left) &&
    isBalanced(root.right)
  );
}
```

# 二叉树的最近公共祖先

```JS
/**
 * * 给定一个二叉树, 找到该树中两个指定节点的最近公共祖先
 * * 思路：
 * * a.若处理到了叶节点或根节点和目标节点之一相等，则祖先就是root
 * * b. 分别从root.left/right上递归找
 * * c. 若左子树上没找到，那一定在右子树上；反之亦然
 * * d. 若左右子树都可以找到，那就是root
 * https://leetcode-cn.com/problems/lowest-common-ancestor-of-a-binary-tree/
 * https://github.com/sisterAn/JavaScript-Algorithms/issues/43
 */
export function lowestCommonAncestor(root, p, q) {

  // 如果树为空树或 p 、 q 中任一节点为根节点，那么 p 、 q 的最近公共节点为根节点
  if (!root || root === p || root === q) return root;

  const left = lowestCommonAncestor(root.left, p, q);
  const right = lowestCommonAncestor(root.right, p, q);

  // 如果左子树没找到，那就在右子树上；树是连通的无环图
  if (!left) return right;
  if (!right) return left;

  // 如果p 、q节点在左右子树的最近公共祖先都存在，此时left===right===root
  return root;
}
```

# 二叉搜索树的最近公共祖先

```JS
/**
 * * 二叉搜索树的最近公共祖先，注意p,q节点大小未知
 * * 思路1：root值最大就在左子树上找，最小就在右子树找，否则就是root
 * * 思路2：普通二叉树的lca找法也适用，oj测试此法快一点点
 * https://leetcode-cn.com/problems/lowest-common-ancestor-of-a-binary-search-tree/
 *
 */
function lowestCommonAncestor(root, p, q) {
  if (!root) return null;

  if (root.val > p.val && root.val > q.val) {
    return lowestCommonAncestor(root.left, p, q);
  }
  if (root.val < p.val && root.val < q.val) {
    return lowestCommonAncestor(root.right, p, q);
  }

  return root;
}
```

# 给定一个二叉树，检查它是否是镜像对称的

```JS
/**
 * * 给定一个二叉树，检查它是否是镜像对称的
 * https://leetcode-cn.com/problems/symmetric-tree/
 * https://github.com/sisterAn/JavaScript-Algorithms/issues/53
 * * 比较二叉树的 前序遍历 和 对称前序遍历 来判断是不是对称的。
 */
function isSymmetric(root) {
  const checkSymmetric = (r1, r2) => {
    if (r1 === null && r2 === null) return true;
    if (r1 === null || r2 === null) return false;
    if (r1.val !== r2.val) return false;
    return (
      checkSymmetric(r1.left, r2.right) && checkSymmetric(r1.right, r2.left)
    );
  };
  // 前序遍历，然后比较左右子节点的值
  return checkSymmetric(root, root);
}
```

# 判断两棵树节点值完全相同

```JS
/**
 * * 判断2棵树val完全相同
 * * 尾递归，类似前序遍历的思路
 * https://leetcode-cn.com/problems/same-tree/
 */
function isSameTree(root1, root2) {
  if (!root1 && !root2) return true;

  if (!root1 || !root2 || root1.val !== root2.val) return false;

  return (
    isSameTree(root1.left, root2.left) && isSameTree(root1.right, root2.right)
  );
}
```

# 另一棵树的子树

```JS
/**
 * * 另一棵树的子树
 * * 思路：先判断根点的值和根节点树，再递归左右子树
 * https://leetcode-cn.com/problems/subtree-of-another-tree/
 * - 如果一棵二叉树t是另一颗二叉树s的子树，那么有3种情况
 * - 1. s和t完全一样
 * - 2. t在s的左子树中（递归）
 * - 3. t在s的右子树中（递归）
 */
function isSubtree(root, subRoot) {
  if (!root) return false;
  // 值相等后再去判断，可以减少计算
  if (root.val === subRoot.val && isSameTree(root, subRoot)) {
    return true;
  }

  return isSubtree(root.left, subRoot) || isSubtree(root.right, subRoot);
}
```

# 二叉树展开为链表

```JS
/**
 * * 二叉树转链表。展开后的单链表应该与二叉树 先序遍历 顺序相同。
 * * 思路：做图分析，转换后的链表为前序遍历根左右，那可以把右子树挂在左子树最下方的节点
 * https://leetcode-cn.com/problems/flatten-binary-tree-to-linked-list/
 * https://juejin.cn/post/6856411258976600077
 */

function flatten(root) {
  let curr = root;
  let left;
  let temp;
  while (curr) {
    // 若左子树非空
    if (curr.left) {
      left = curr.left;
      temp = left;
      // 找到左子树的最后一个元素，一般是最下方的右叶子
      while (temp.right) {
        temp = temp.right;
      }

      // 将curr的右子树挂到左子树的最下方
      temp.right = curr.right;

      // 将左子树变为右子树
      curr.left = null;
      curr.right = left;
    }

    curr = curr.right;
  }
}

// 类似后序遍历，太巧妙了
function flatten(root) {

  // 记录前一个节点
  let prev = null;

  const dfs = node => {

    if (!node) return;

    dfs(node.right);
    dfs(node.left);

    node.left = null;
    node.right = prev;

    prev = node;
  }

  dfs(root)
}
```

# 二叉树的序列化

```JS
/**
 * * 二叉树的序列化与反序列化
 * https://leetcode-cn.com/problems/serialize-and-deserialize-binary-tree/
 * * 基于层序遍历实现序列化，空子节点序列化为 #
 */
export function serialize(root) {
  if (!root) {
    return '';
  }
  const result = [];
  const queue = [root];
  let current = root;
  while (queue.length) {
    // * 每次取第一个元素
    current = queue.shift();
    if (current) {
      result.push(current.val);
      queue.push(current.left, current.right);
    } else {
      result.push('#');
    }
  }
  return result.toString();
}
/**
 * * 基于层序遍历的字符串，生成二叉树，#代表的空节点反序列化为null
 */
export function deserialize(data) {
  if (!data) {
    return null;
  }
  data = data.split(',');
  const root = new TreeNode(data[0]);
  const queue = [root];
  let cursor = 1;
  while (cursor < data.length) {
    // * 每次取第一个元素作为父节点
    const parent = queue.shift();
    parent.left = data[cursor] != '#' ? new TreeNode(data[cursor]) : null;
    parent.right =
      data[cursor + 1] != '#' ? new TreeNode(data[cursor + 1]) : null;
    parent.left && queue.push(parent.left);
    parent.right && queue.push(parent.right);
    cursor += 2;
  }
  return root;
}
```
