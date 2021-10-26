---
title: job-leetcode-tree-path-sum
tags: [leetcode, repeat, tree]
created: '2021-10-08T19:43:31.119Z'
modified: '2021-10-08T19:52:20.160Z'
---

# job-leetcode-tree-path-sum

# 二叉树的最大深度

```JS
/**
 * * 给定一个二叉树，找出其最大深度。
 * * 思路1: 递归求左右子树的深度，从叶到根每层+1
 * * 思路2: 层序遍历
 * 深度为根节点到最远叶子节点的最长路径上的节点数。
 * https://leetcode-cn.com/problems/maximum-depth-of-binary-tree/
 * https://github.com/sisterAn/JavaScript-Algorithms/issues/42
 */
function maxDepth(root) {
  if (!root) return 0;

  return 1 + Math.max(maxDepth(root.left), maxDepth(root.right));
}
```

# 二叉树的最小深度

```JS
/***
 * * 二叉树的最小深度。与求最大深度相反
 * 最小深度是从根节点到最近叶子节点的最短路径上的节点数量。
 * https://leetcode-cn.com/problems/minimum-depth-of-binary-tree/
 */
function minDepth(root) {
  if (!root) return 0;

  // 如果左或右子树为空的话是构不成子树的。而最小深度是要求从根节点到子树的。
  if (!root.left && root.right) {
    return 1 + minDepth(root.right);
  }
  if (!root.right && root.left) {
    return 1 + minDepth(root.left);
  }

  return 1 + Math.min(minDepth(root.left), minDepth(root.right));
}
```

# 找到该树中两个指定节点间的最短距离

```JS
/**
 * * 给定一个二叉树, 找到该树中两个指定节点间的最短距离。
 * * 思路：
 * * a.找到最近公共祖先lca节点； 
 * * b.分别求出两节点到lca的距离； 
 * * c. 距离相加
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
 * * 思路：类似前序遍历，先入栈，递归查找左右子树，若没找到就出栈
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

# 路径总和: 从根到叶的路径中，判断是否存在满足目标和的路径

```JS
/**
 * * 是否存在 根节点到叶子节点 的路径，所有节点值相加等于目标和 targetSum
 * * 思路：先判断叶子节点直接比较，否则每层减去根节点值，再递归左右子树
 * - 给定一个二叉树和一个目标和，判断该树中是否存在根节点到叶子节点的路径，这条路径上所有节点值相加等于目标和。
 * https://leetcode-cn.com/problems/path-sum/
 * https://github.com/sisterAn/JavaScript-Algorithms/issues/45
 */
export function hasPathSum(root, targetSum) {
  if (!root) return false;

  if (root.left === null && root.right === null) {
    // 若是叶节点，则直接比较总和
    return root.val === targetSum;
  }

  targetSum = targetSum - root.val;
  return hasPathSum(root.left, targetSum) || hasPathSum(root.right, targetSum);
}
```

# 路径总和: 从根到叶的路径中，寻找满足目标和的节点路径

```JS
/**
 * * 找出所有 从根节点到叶子节点 路径总和等于给定目标和的路径。
 * https://leetcode-cn.com/problems/path-sum-ii/
 */
export function pathSum(root, targetSum) {
  if (!root) return [];
  const result = [];

  const dfs = (node, sum, path) => {
    if (!node) return 0;
    path = [...path, node.val];
    sum = sum - node.val;

    // 若到叶节点刚好满足就是了
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

# 求根节点到叶节点数字之和

```JS
/**
 * * 求根节点到叶节点数字之和
 * 树的每个结点都存放一个 0-9 的数字，每条从根到叶子节点的路径都代表一个数字。
 * https://leetcode-cn.com/problems/sum-root-to-leaf-numbers/
 * https://github.com/Chocolate1999/leetcode-javascript/issues/43
 */
function sumNumbers(root) {
  let sum = 0;

  const dfs = (root, cur) => {
    // 终止条件
    if (!root) return 0;

    // 计算当前节点的值
    cur = cur * 10 + root.val;

    // 找到一条路径，返回路径和
    if (!root.left && !root.right) {
      return cur;
    }

    // 对左右子树递归，求总和
    return dfs(root.left, cur) + dfs(root.right, cur);
  };

  sum = dfs(root, 0);

  return sum;
}
```

# 二叉树的直径

```JS
/**
 * * 二叉树的直径。
 * * 思路： 将二叉树的直径转换为：二叉树的每个节点的左右子树的高度和的最大值。
 * * 递归左右子树求直径，每次+1或0；
 * 直径长度是任意两个结点路径长度中的最大值，这条路径可能穿过也可能不穿过根结点
 * https://leetcode-cn.com/problems/diameter-of-binary-tree/
 * - root的直径 = root左子树高度 + root右子树高度
 * - root的高度 = max {root左子树高度, root右子树高度} + 1
 */
function diameterOfBinaryTree(root) {
  let ret = 0;

  const dfs = (node) => {
    if (!node) return 0;

    const left = node.left ? dfs(node.left) + 1 : 0;
    const right = node.right ? dfs(node.right) + 1 : 0;

    // 更新直径最大值
    ret = Math.max(left + right, ret);

    // 子树高度
    return Math.max(left, right);
  };

  dfs(root);

  return ret;
}
```

# 二叉树中的最大路径和

```JS
/**
 * * 二叉树中的最大路径和
 * * 与求直径类似，但每次递归加的是节点值
 * https://leetcode-cn.com/problems/binary-tree-maximum-path-sum/
 * https://github.com/Chocolate1999/leetcode-javascript/issues/57
 * https://leetcode-cn.com/problems/binary-tree-maximum-path-sum/solution/shou-hui-tu-jie-hen-you-ya-de-yi-dao-dfsti-by-hyj8/
 * 路径 被定义为一条从树中任意节点出发，沿父节点-子节点连接，达到任意节点的序列。
 * 同一个节点在一条路径序列中 至多出现一次 。路径 至少包含一个 节点，且不一定经过根节点。
 * 路径和 是路径中各节点值的总和。
 */
function maxPathSum(root) {
  let maxSum = Number.MIN_SAFE_INTEGER;

  const dfs = (node) => {
    if (!node) return 0;

    const left = dfs(node.left); // 左子树提供的最大路径和
    const right = dfs(node.right); // 右子树提供的最大路径和

    // 当前子树内部的最大路径和
    const innerMaxSum = left + node.val + right;
    maxSum = Math.max(maxSum, innerMaxSum); // 挑战最大纪录

    const outputMaxSum = node.val + Math.max(0, left, right); // 当前子树对外提供的最大和

    // 如果对外提供的路径和为负，直接返回0。否则正常返回
    return outputMaxSum < 0 ? 0 : outputMaxSum;
  };

  dfs(root); // 递归的入口

  return maxSum;
}
```
