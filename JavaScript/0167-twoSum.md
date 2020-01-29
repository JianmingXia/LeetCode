# 两数之和 II - 输入有序数组

## 题目描述
给定一个已按照升序排列 的有序数组，找到两个数使得它们相加之和等于目标数。

函数应该返回这两个下标值 index1 和 index2，其中 index1 必须小于 index2。

### 示例
```
输入: numbers = [2, 7, 11, 15], target = 9
输出: [1,2]
解释: 2 与 7 之和等于目标数 9 。因此 index1 = 1, index2 = 2 。
```

### 说明
- 返回的下标值（index1 和 index2）不是从零开始的。
- 你可以假设每个输入只对应唯一的答案，而且你不可以重复使用相同的元素。

## 思路分析
这一题之前也遇到过，是使用哈希表来做的，当时给出的数组是无序的，故而使用 hash 表的思想来进行操作。在本题中，依然可以使用 hash 表来操作，不过这里我换了个思路。由于数组是有序的，我们直接从数组的首尾逐步向中间靠拢，直至找到目标数字。

## 代码
- 时间复杂度O(n)
- 空间复杂度O(1)

```
/**
 * @param {number[]} numbers
 * @param {number} target
 * @return {number[]}
 */
var twoSum = function(numbers, target) {  
  let low = 0;
  let high = numbers.length - 1;

  while(low < high) {
    if(numbers[low] + numbers[high] > target) {
      high--;
    } else if(numbers[low] + numbers[high] < target) {
      low++;
    } else {
      return [low + 1, high + 1];
    }
  }
  
  return [];
};
```