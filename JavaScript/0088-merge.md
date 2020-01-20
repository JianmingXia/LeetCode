# 合并两个有序数组

## 题目描述
给定两个有序整数数组 nums1 和 nums2，将 nums2 合并到 nums1 中，使得 num1 成为一个有序数组。

### 示例
```
输入:
nums1 = [1,2,3,0,0,0], m = 3
nums2 = [2,5,6],       n = 3

输出: [1,2,2,3,5,6]
```

### 说明
初始化 nums1 和 nums2 的元素数量分别为 m 和 n。
你可以假设 nums1 有足够的空间（空间大小大于或等于 m + n）来保存 nums2 中的元素。

## 思路分析
这一题算是正常合并有序数组的一个变种——要求在某个数组上原地进行合并。因此在合并的过程中，关于效率我也是有考虑的：
- 在指定数组上不断迭代，找到合适的位置进行插入：这样在后续进行迭代时，比较次数会越来越小
- 直接使用二分查找，这个方法比较简单粗暴，同时我翻看了之前的提交记录，第 35 题刚好是查找插入位置的，适合这里的场景。

在进行合并的时候需要注意，本来我是打算使用 slice，但是传入的数组是包含 [0, 0, 0]的，故而操作需要小心——所以这部分是自己手动实现，毕竟 slice 底层也是类似的处理逻辑。

### Note
这里还想到一个优化，上次查找到的 pos 在查询的时候传入，可以减少比较次数，但是试过之后，发现效率没有大的改动——想来对于二分查找来说，这点优化对于性能的提升不大

## 代码
- 时间复杂度O(n)
- 空间复杂度O(1)

```
var searchInsert = function(nums, len, target) {
  if(len === 0) {
    return 0;
  }

  let low = 0;
  let high = len - 1;
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

/**
 * @param {number[]} nums1
 * @param {number} m
 * @param {number[]} nums2
 * @param {number} n
 * @return {void} Do not return anything, modify nums1 in-place instead.
 */
var merge = function(nums1, m, nums2, n) {
  for(let num2 of nums2) {
    const pos = searchInsert(nums1, m, num2);

    for(let i = m - 1; i >= pos ; i--) {
      nums1[i + 1] = nums1[i];
    }

    nums1[pos] = num2;
    m += 1;
  }
};
```