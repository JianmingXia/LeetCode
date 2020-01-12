# 搜索插入位置

## 题目描述
给定一个排序数组和一个目标值，在数组中找到目标值，并返回其索引。如果目标值不存在于数组中，返回它将会被按顺序插入的位置。

你可以假设数组中无重复元素。
### 示例
```
示例 1:

输入: [1,3,5,6], 5
输出: 2

示例 2:

输入: [1,3,5,6], 2
输出: 1

示例 3:

输入: [1,3,5,6], 7
输出: 4

示例 4:

输入: [1,3,5,6], 0
输出: 0
```

## 思路分析
话不多说，这题实际上微改版的二分查找

## 代码
- 时间复杂度O(n)
- 空间复杂度O(1)

```
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number}
 */
var searchInsert = function(nums, target) {
  if(nums.length === 0) {
    return 0;
  }

  let low = 0;
  let high = nums.length - 1;
  let mid;
  while(low <= high) {
    mid = Math.ceil((low + high) / 2);

    if(nums[mid] > target) {
      high = mid - 1;
    } else if(nums[mid] < target) {
      low = mid + 1;
    } else {
      return mid;
    } 
  }

  return nums[mid] > target ? mid : mid + 1;
};
```