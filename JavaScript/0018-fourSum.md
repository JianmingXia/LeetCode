# 四数之和

## 题目描述
给定一个包含 n 个整数的数组 nums 和一个目标值 target，判断 nums 中是否存在四个元素 a，b，c 和 d ，使得 a + b + c + d 的值与 target 相等？找出所有满足条件且不重复的四元组。

### 示例
```
给定数组 nums = [1, 0, -1, 0, -2, 2]，和 target = 0。

满足要求的四元组集合为：
[
  [-1,  0, 0, 1],
  [-2, -1, 1, 2],
  [-2,  0, 0, 2]
]
```

### 说明
答案中不可以包含重复的四元组。

## 思路分析
与“三数之和”类似，没有想到很好的办法，只能在外面加个嵌套

## 代码
- 时间复杂度O(n³)
- 空间复杂度O(n)

```
/**
 * @param {number[]} nums
 * @param {number} currentIndex
 * @param {number} endIndex
 * @param {number} step
 * @return {number}
 */
const getNextNotEqualIndex = (nums, currentIndex, endIndex, step) => {
  for (let i = currentIndex + step; i != endIndex; i += step) {
    if (nums[i] != nums[currentIndex]) {
      return i;
    }
  }

  return endIndex;
};

/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number[][]}
 */
var fourSum = function(nums, target) {
  if (!nums || nums.length < 4) {
    return [];
  }

  // 先进行排序，题中需要去重，这里有助于去重
  nums.sort((a, b) => a - b);

  let res = [];
  for (let i = 0; i < nums.length - 3; i++) {
    if (i !== 0 && nums[i] === nums[i - 1]) {
      continue;
    }

    for (let j = i + 1; j < nums.length - 2; j++) {
      if (j !== i + 1 && nums[j] === nums[j - 1]) {
        continue;
      }

      let start = j + 1;
      let end = nums.length - 1;
      while (start < end) {
        if (nums[i] + nums[j] + nums[start] + nums[end] > target) {
          end = getNextNotEqualIndex(nums, end, start, -1);
        } else if (nums[i] + nums[j] + nums[start] + nums[end] < target) {
          start = getNextNotEqualIndex(nums, start, end, 1);
        } else {
          res.push([nums[i], nums[j], nums[start], nums[end]]);

          start = getNextNotEqualIndex(nums, start, end, 1);
          end = getNextNotEqualIndex(nums, end, start, -1);
        }
      }
    }
  }

  return res;
};
```