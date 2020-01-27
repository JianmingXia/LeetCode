# 二叉树的层次遍历 II

## 题目描述
给定一个二叉树，返回其节点值自底向上的层次遍历。 （即按从叶子节点所在层到根节点所在的层，逐层从左向右遍历）

### 示例
```
给定二叉树 [3,9,20,null,null,15,7],

    3
   / \
  9  20
    /  \
   15   7
返回其自底向上的层次遍历为：

[
  [15,7],
  [9,20],
  [3]
]
```

## 思路分析
题目都叫层序遍历了，那我们自然按照层序的方式进行遍历，只不过最后需要注意将数组进行翻转。

## 代码
- 时间复杂度O(n)
- 空间复杂度O(n)

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
 * @return {number[][]}
 */
var levelOrderBottom = function(root) {
  if(!root) {
    return [];
  }

  let currentList = [root];

  const res = [];
  while(currentList.length > 0) {
    let row = [];
    let nextList = [];

    for(const node of currentList) {
      row.push(node.val);
      
      if(node.left) {
        nextList.push(node.left);
      }

      if(node.right) {
        nextList.push(node.right);
      }
    }
    
    currentList = nextList;
    res.push(row);
  }

  return res.reverse();
};
```