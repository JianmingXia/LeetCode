# 存在重复元素

## 题目描述
给定一个整数数组，判断是否存在重复元素。

如果任何值在数组中出现至少两次，函数返回 true。如果数组中每个元素都不相同，则返回 false。

### 示例
```
示例 1:

输入: [1,2,3,1]
输出: true

示例 2:

输入: [1,2,3,4]
输出: false

示例 3:

输入: [1,1,1,3,3,4,3,2,4,2]
输出: true
```

## 思路分析
两个思路：
- 通过 Map 的占位原理，第一次出现设置 key 对应的值为 true，后面再出现即表示重复
- 通过 Set 的值不可重复，与原数组比较元素的个数即可

## 代码
- 时间复杂度O(n)
- 空间复杂度O(n)

### 思路 1
```
/**
 * @param {number[]} nums
 * @return {boolean}
 */
var containsDuplicate = function(nums) {
  let res = {};

  for(const num of nums) {
    if(res[num]) {
      return true;
    } else {
      res[num] = true;
    }
  }

  return false;
};
```

### 思路 2
```
/**
 * @param {number[]} nums
 * @return {boolean}
 */
var containsDuplicate = function(nums) {
  return new Set(nums).size !== nums.length;
};
```