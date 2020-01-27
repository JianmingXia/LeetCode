# 将有序数组转换为二叉搜索树

## 题目描述
将一个按照升序排列的有序数组，转换为一棵高度平衡二叉搜索树。

### 示例
```
给定有序数组: [-10,-3,0,5,9],

一个可能的答案是：[0,-3,9,-10,null,5]，它可以表示下面这个高度平衡二叉搜索树：

      0
     / \
   -3   9
   /   /
 -10  5
```

### 说明
本题中，一个高度平衡二叉树是指一个二叉树每个节点的左右两个子树的高度差的绝对值不超过 1。

## 思路分析
题目是将有序数组转换为二叉搜索树，这里我们可以思考一下，我们使用中序遍历出的数据也是有序的。这里我们选中中间的节点，作为“根节点”，中间节点的左边及右边分别构建左右子树。

## 代码
- 时间复杂度O(n)
- 空间复杂度O(n)

```
const buildTree = (nums, low, high) => {
  if(low > high) {
    return null;
  }

  const mid = low + Math.ceil((high - low) / 2);

  const root = {
    val: nums[mid]
  }

  root.left = buildTree(nums, low, mid - 1);
  root.right = buildTree(nums, mid + 1, high);

  return root;
}

/**
 * Definition for a binary tree node.
 * function TreeNode(val) {
 *     this.val = val;
 *     this.left = this.right = null;
 * }
 */
/**
 * @param {number[]} nums
 * @return {TreeNode}
 */
var sortedArrayToBST = function(nums) {
  return buildTree(nums, 0, nums.length - 1);
};
```