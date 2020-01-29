# 多数元素

## 题目描述
给定一个大小为 n 的数组，找到其中的多数元素。多数元素是指在数组中出现次数大于 ⌊ n/2 ⌋ 的元素。

你可以假设数组是非空的，并且给定的数组总是存在多数元素。

### 示例
```
示例 1:

输入: [3,2,3]
输出: 3

示例 2:

输入: [2,2,1,1,1,2,2]
输出: 2
```

## 思路分析
这题我有两个思路：

### 思路1
打算用哈希表来实现的，用于记录指定元素的次数，并且每次进行次数比较

### 思路2
直接运用摩尔投票法——这个方法我本来是打算应用的，后面查的时候突然发现叫摩尔投票法，很有趣。

## 代码
- 时间复杂度O(n)
- 空间复杂度O(n)

```
/**
 * @param {number[]} nums
 * @return {number}
 */
var majorityElement = function(nums) {
  let major = nums[0];
  let times = 1;
  for(let i = 1; i < nums.length; i++) {
    if(nums[i] === major) {
      times++;
    } else {
      if(times > 0) {
        times--;
      } else {
        times++;
        major = nums[i];
      }
    }
  }

  return major;
};
```