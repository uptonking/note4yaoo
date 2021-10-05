---
title: job-coding-algs-tree-traversal
tags: [coding, job, traversal, tree, leetcode]
created: '2021-10-05T10:07:02.318Z'
modified: '2021-10-05T10:09:04.082Z'
---

# job-coding-algs-tree-traversal

# guide
- 二叉树遍历小结
  - 二叉树的前中后序深度优先遍历都基于stack，访问元素都使用 `stack.pop()`，只有后序遍历将访问结果`unshift`插入结果数组的第一个
  - 二叉树的层序遍历基于queue，访问元素使用 `queue.shift()`

```JS
// 二叉树的节点定义
function TreeNode(val, left, right) {
  this.val = val === undefined ? 0 : val;
  this.left = left === undefined ? null : left;
  this.right = right === undefined ? null : right;
}
```

```JS
// 二叉树遍历模版
function orderTraversal(root) {
  if (!root) return [];
  const ret = [];
  return ret;
}
// 用于基于循环实现的深度优先遍历
// const stack = [];
// let curr = root;
```

# 前序遍历

```JS
function preorderTraversal(root) {
  if (!root) return [];
  const ret = [];

  function preTree(node) {
    if (node) {
      ret.push(node.val);
      // node.left && preTree(node.left);
      // node.right && preTree(node.right);
      pretree(node.left);
      pretree(node.right);
    }
  }

  preTree(root);

  return ret;
}
```

```JS
function preorderTraversal(root) {
  if (!root) return [];
  const ret = [];
  const stack = [root];
  let curr = root;
  while (stack.length) {
    curr = stack.pop();
    ret.push(curr.val);

    curr.right && stack.push(curr.right);
    curr.left && stack.push(curr.left);
  }

  return ret;
}
```

- ref
  - https://leetcode-cn.com/problems/binary-tree-preorder-traversal/
  - https://github.com/sisterAn/JavaScript-Algorithms/issues/37
# 中序遍历

```JS
function inorderTraversal(root) {
  if (!root) return [];
  const ret = [];

  function inTree(node) {
    if (node) {
      inTree(node.left);
      ret.push(node.val);
      inTree(node.right);
    }
  }

  inTree(root);

  return ret;
}
```

```JS
function inorderTraversal(root) {
  if (!root) return [];

  const ret = [];

  const stack = [];
  let curr = root;

  while (stack.length || curr) {
    while (curr) {
      stack.push(curr);
      curr = curr.left;
    }

    curr = stack.pop();
    ret.push(curr.val);

    curr = curr.right
  }

  return ret;
}
```

- ref
  - https://leetcode-cn.com/problems/binary-tree-inorder-traversal/
  - https://github.com/sisterAn/JavaScript-Algorithms/issues/38
# 后序遍历

```JS
function postorderTraversal(root) {
  if (!root) return [];
  const ret = [];

  function postTree(node) {
    if (node) {
      postTree(node.left);
      postTree(node.right);
      ret.push(node.val)
    }
  }

  postTree(root);

  return ret;
}
```

```JS
function postorderTraversal(root) {
  if (!root) return [];
  const ret = [];

  const stack = [root];
  let curr = root;

  while (stack.length) {

    curr = stack.pop();

    ret.unshift(curr.val);

    curr.left && stack.push(curr.left);
    curr.right && stack.push(curr.right);
  }

  return ret;
}
```

- ref
  - https://leetcode-cn.com/problems/binary-tree-postorder-traversal/
  - https://github.com/sisterAn/JavaScript-Algorithms/issues/40
# 层序遍历

```JS
function levelorderTraversal(root) {
  if (!root) return [];
  const ret = [];

  function levelTree(node, depth) {
    if (node) {
      ret[depth] = ret[depth] || [];
      ret[depth].push(node.val);

      // ! 注意这里不能是++depth
      // levelTree(node.left, ++depth);
      levelTree(node.left, depth + 1);
      levelTree(node.right, depth + 1);
    }
  }

  levelTree(root, 0);

  return ret;
}
```

```JS
function levelorderTraversal(root) {
  if (!root) return [];
  const ret = [];

  const queue = [root];
  let curr = root;

  while (queue.length) {
    curr = queue.shift();

    ret.push(curr.val);

    curr.left && queue.push(curr.left);
    curr.right && queue.push(curr.right);
  }

  return ret;
}
```

```JS
// 返回每层的节点值，返回的是二维数组
function getNodesByLevelOrder(root) {
  if (!root) return [];
  const ret = [];

  const queue = [root];
  let curr = root;

  while (queue.length) {
    const levelVals = [];
    const levelSize = queue.length;

    // 每次处理完上一层的元素，然后就加入了下一层的元素
    for (let i = 0; i < levelSize; i++) {
      curr = queue.shift();
      levelVals.push(curr.val);

      curr.left && queue.push(curr.left);
      curr.right && queue.push(curr.right);
    }

    ret.push(levelVals);
    // ret.unshift(level);
  }

  return ret;
}
```

- ref
  - https://leetcode-cn.com/problems/binary-tree-level-order-traversal/
  - https://github.com/sisterAn/JavaScript-Algorithms/issues/47
  - https://github.com/sisterAn/JavaScript-Algorithms/issues/46
