---
title: job-coding-algs-tree
tags: [algorithms, coding, job, tree, leetcode]
created: '2021-10-05T09:02:06.952Z'
modified: '2021-10-05T09:02:30.252Z'
---

# job-coding-algs-tree

# guide

```JS
// 二叉树的节点定义
function TreeNode(val, left, right) {
  this.val = val === undefined ? 0 : val;
  this.left = left === undefined ? null : left;
  this.right = right === undefined ? null : right;
}
```

- todo
  - 二叉树转链表
# 给定一个二叉树，找出其最大深度
- 思路1: 递归求左右子树的深度，从叶到根每层+1
- 思路2: 层序遍历

```JS
/**
 * * 给定一个二叉树，找出其最大深度。
 * 深度为根节点到最远叶子节点的最长路径上的节点数。
 * https://github.com/sisterAn/JavaScript-Algorithms/issues/42
 * https://leetcode-cn.com/problems/maximum-depth-of-binary-tree/
 */
function maxDepth(root) {
  if (!root) return 0;
  return Math.max(maxDepth(root.left), maxDepth(root.right)) + 1;
}
```

# 给定一个二叉树，判断它是否是高度平衡的二叉树

> 一个二叉树每个节点的左右两个子树的高度差的绝对值不超过1。

```JS
/**
 * * AVL树是指左右子树深度差不超过1的二叉树；
 * 思路：自顶向下的比较每个节点的左右子树的最大高度差，如果二叉树中每个节点的左右子树最大高度差
 * 小于等于1 ，即每个子树都平衡时，此时二叉树才是平衡二叉树
 * https://github.com/sisterAn/JavaScript-Algorithms/issues/44
 */
export function isBalanced(root) {
  if (!root) return true;
  const getDepth = (node) => {
    if (!node) return -1;
    return Math.max(getDepth(node.left), getDepth(node.right)) + 1;
  };
  return (
    Math.abs(getDepth(root.left) - getDepth(root.right)) <= 1 &&
    isBalanced(root.left) &&
    isBalanced(root.right)
  );
}
```

# 给定一个二叉树, 找到该树中两个指定节点的最近公共祖先

```JS
/**
 * * 给定一个二叉树, 找到该树中两个指定节点的最近公共祖先
 * https://leetcode-cn.com/problems/lowest-common-ancestor-of-a-binary-tree/
 * https://github.com/sisterAn/JavaScript-Algorithms/issues/43
 */
export function lowestCommonAncestor(root, p, q) {
  if (!root || root === p || root === q) return root;
  const left = lowestCommonAncestor(root.left, p, q);
  const right = lowestCommonAncestor(root.right, p, q);
  if (!left) return right;
  if (!right) return left;
  return root;
}
```

# 找到该树中两个指定节点间的最短距离

```JS
/**
 * * 给定一个二叉树, 找到该树中两个指定节点间的最短距离。
 * 思路：
 * - a.找到最近公共祖先lca节点； 
 * - b.分别求出两节点到lca的距离； 
 * - c. 距离相加
 * https://github.com/sisterAn/JavaScript-Algorithms/issues/82
 */
export function shortestDistance(root, p, q) {
  const lowestCA = lowestCommonAncestor(root, p, q);
  const pDis = [];
  const qDis = [];
  getPath(lowestCA, p, pDis);
  getPath(lowestCA, q, qDis);
  return pDis.length + qDis.length;
}
/**
 * * 计算根节点root到节点node的路径。
 * - 从root节点开始向下查找node节点
 */
export function getPath(root, node, paths) {
  if (root === node) return true;
  paths.push(root);
  let hasFound = false;
  if (root.left) {
    hasFound = getPath(root.left, node, paths);
  }
  if (root.right) {
    hasFound = getPath(root.right, node, paths);
  }
  if (hasFound === false) {
    // 如果没找到，说明不在这里节点的子树
    paths.pop();
  }
  return hasFound;
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

# 翻转二叉树

```JS
/**
 * * 翻转二叉树。二叉树的左右子树交换
 * https://leetcode-cn.com/problems/invert-binary-tree/
 * - 从根节点开始前序遍历每个节点，然后交换左右子树既可
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

# 判断两个树节点值完全相同

```JS
/**
 * * 判断2棵树val完全相同
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

# 二叉树转链表

```JS
/**
 * * 二叉树转链表。展开后的单链表应该与二叉树 先序遍历 顺序相同。
 * https://leetcode-cn.com/problems/flatten-binary-tree-to-linked-list/submissions/
 * https://blog.voyz.vip/2020/12/31/LeetCode%E7%AE%97%E6%B3%95%E7%AC%94%E8%AE%B0-Day54/
 *
 */
export function flatten(root) {
  if (!root) return null;
  let current = root;
  while (current) {
    if (!current.left) {
      current = current.right;
      continue;
    }
    const next = current.left;
    let pre = next;
    while (pre.right) {
      pre = pre.right;
    }
    pre.right = current.right;
    current.right = next;
    current.left = null;
  }
  return root;
}
```

# 从根到叶的路径中，判断是否存在满足目标和的路径

```JS
/**
 * * 给定一个二叉树和一个目标和，判断该树中是否存在根节点到叶子节点的路径，这条路径上所有节点值相加等于目标和。
 *
 * https://leetcode-cn.com/problems/path-sum/
 * https://github.com/sisterAn/JavaScript-Algorithms/issues/45
 */
export function hasPathSum(root, targetSum) {
  if (!root) return false;
  if (root.left === null && root.right === null) {
    return root.val === targetSum;
  }
  targetSum = targetSum - root.val;
  return hasPathSum(root.left, targetSum) || hasPathSum(root.right, targetSum);
}
```

# 从根到叶的路径中，寻找满足目标和的节点路径

```JS
export function pathSum(root, targetSum) {
  if (!root) {
    return [];
  }
  const result = [];
  const dfs = (node, sum, path) => {
    if (!node) {
      return 0;
    }
    path = [...path, node.val];
    sum = sum - node.val;
    if (!node.left && !node.right && sum === 0) {
      result.push(path);
      return;
    }
    node.left && dfs(node.left, sum, path);
    node.right && dfs(node.right, sum, path);
  };
  dfs(root, targetSum, []);
  return result;
}
```

# 二叉树的序列化

```JS
/**
 * 二叉树的序列化与反序列化
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

# 二叉搜索树 BST

---

# 二叉搜索树中第 K 小的元素

```JS
/**
 * * 二叉搜索树中第K小的元素
 * https://leetcode-cn.com/problems/kth-smallest-element-in-a-bst/
 * https://github.com/sisterAn/JavaScript-Algorithms/issues/86
 * - 中序遍历二叉搜索树，输出第 k 个既可
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
