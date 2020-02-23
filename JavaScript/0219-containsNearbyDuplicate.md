# 存在重复元素 II

## 题目描述
给定一个整数数组和一个整数 k，判断数组中是否存在两个不同的索引 i 和 j，使得 nums [i] = nums [j]，并且 i 和 j 的差的绝对值最大为 k。

### 示例
```
示例 1:

输入: nums = [1,2,3,1], k = 3
输出: true

示例 2:

输入: nums = [1,0,1,1], k = 1
输出: true

示例 3:

输入: nums = [1,2,3,1,2,3], k = 2
输出: false
```

## 思路分析
这题与上次类似，不过需要注意的是：上题记录标志位即可，此题需要记录上次出现的下标。另外，需要审题细致：“i 和 j 的差的绝对值最大为 k”。

## 代码
- 时间复杂度O(n)
- 空间复杂度O(n)

```
/**
 * @param {number[]} nums
 * @param {number} k
 * @return {boolean}
 */
var containsNearbyDuplicate = function(nums, k) {
  let res = {};

  for (let i = 0; i < nums.length; i++) {
    if (res[nums[i]] >= 0 && i - res[nums[i]] <= k) {
      return true;
    } else {
      res[nums[i]] = i;
    }
  }

  return false;
};
```