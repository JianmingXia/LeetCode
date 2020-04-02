# 最接近的三数之和

## 题目描述
给定一个包括 n 个整数的数组 nums 和 一个目标值 target。找出 nums 中的三个整数，使得它们的和与 target 最接近。返回这三个数的和。假定每组输入只存在唯一答案。

### 示例
```
例如，给定数组 nums = [-1，2，1，-4], 和 target = 1.

与 target 最接近的三个数的和为 2. (-1 + 2 + 1 = 2).
```

## 思路分析
与“三数之和”的思路类似，复用逻辑即可

## 代码
- 时间复杂度O(n²)
- 空间复杂度O(1)

```
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number}
 */
var threeSumClosest = function(nums, target) {
  // 便于有序找到最佳方案
  nums.sort((a, b) => a - b);

  let closestNum = nums[0] + nums[1] + nums[2];

  for(let i = 0; i < nums.length - 2; i++) {
    let start = i + 1;
    let end = nums.length - 1;
    while(start < end) {
      const currentValue = nums[i] + nums[start] + nums[end];

      if(Math.abs(target - closestNum) > Math.abs(target - currentValue)) {
        closestNum = currentValue;
      }
      
      if(currentValue > target) {
        end--;
      } else if(currentValue < target) {
        start++;
      } else {
        return target;
      }
    }
  }

  return closestNum;
};
```