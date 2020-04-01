# 三数之和

## 题目描述
给你一个包含 n 个整数的数组 nums，判断 nums 中是否存在三个元素 a，b，c ，使得 a + b + c = 0 ？请你找出所有满足条件且不重复的三元组。

### 示例
```
给定数组 nums = [-1, 0, 1, 2, -1, -4]，

满足要求的三元组集合为：
[
  [-1, 0, 1],
  [-1, -1, 2]
]
```

### 说明
答案中不可以包含重复的三元组。

## 思路分析
- 首先对数组进行排序，之前对无序数组进行操作时，由于加了很多判断，最后也超时了，这里有两个原因：1 是性能本来就不高，其次是多了很多无效的判断。
- 接下来做数组的迭代：然后取当前迭代数组的右边，记为 start 及 end：
  - 若：nums[i] + nums[start] + nums[end] === 0，则为有效值。此时不要跳出循环，继续迭代
  - 否则：nums[i] + nums[start] + nums[end] !== 0 时，根据对应场景收缩 start 或 end
- 说明：代码中还有很多分支判断，主要是为了减少无效比较——fail fast

## 代码
- 时间复杂度O(n²)
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
  for(let i = currentIndex + step; i != endIndex; i += step) {
    if(nums[i] != nums[currentIndex]) {
      return i;
    }
  }

  return endIndex;
}

/**
 * @param {number[]} nums
 * @return {number[][]}
 */
var threeSum = function(nums) {
  if(!nums || nums.length < 3) {
    return [];
  }

  // 先进行排序，题中需要去重，这里有助于去重
  nums.sort((a, b) => a - b);

  let res = [];
  for(let i = 0; i < nums.length - 2; i++) {
    if(i !== 0 && nums[i] === nums[i - 1]) {
      continue;
    }

    let start = i + 1;
    let end = nums.length - 1;
    while(start < end) {
      // 前 2 个值 > 0，必然找不到目标值
      if(nums[i] + nums[start] > 0) {
        break;
      }
      // 最大值 < 0，必然找不到目标值
      if(nums[end] < 0) {
        break;
      }

      // 找到目标值
      if(nums[i] + nums[start] + nums[end] > 0) {
        end = getNextNotEqualIndex(nums, end, start, -1);
      } else if(nums[i] + nums[start] + nums[end] < 0) {
        start = getNextNotEqualIndex(nums, start, end, 1);
      } else {
        res.push([nums[i], nums[start], nums[end]]);

        start = getNextNotEqualIndex(nums, start, end, 1);
        end = getNextNotEqualIndex(nums, end, start, -1);
      }
    }
  }

  return res;
};
```