# 二叉树的最大深度

## 题目描述
给定一个二叉树，找出其最大深度。

二叉树的深度为根节点到最远叶子节点的最长路径上的节点数。

说明: 叶子节点是指没有子节点的节点。

### 示例
```
给定二叉树 [3,9,20,null,null,15,7]，

    3
   / \
  9  20
    /  \
   15   7
返回它的最大深度 3 。
```

### 说明

## 思路分析
这题其实是一个普通的递归思路：
- 如果树为空，则最大深度为 0
- 否则其最大深度是 Max(左树的最大深度，右树的最大深度) + 1

## 代码
- 时间复杂度O(logn)
- 空间复杂度O(1)

```
/**
 * Definition for a binary tree node.
 * function TreeNode(val) {
 *     this.val = val;
 *     this.left = this.right = null;
 * }
 */
/**
 * @param {TreeNode} root
 * @return {number}
 */
var maxDepth = function(root) {
  if(!root) {
    return 0;
  }

  const leftDepth = maxDepth(root.left);
  const rightDepth = maxDepth(root.right);

  return 1 + (leftDepth > rightDepth ? leftDepth : rightDepth);
};
```