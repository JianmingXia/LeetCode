# 下一个排列

## 题目描述
实现获取下一个排列的函数，算法需要将给定数字序列重新排列成字典序中下一个更大的排列。

如果不存在下一个更大的排列，则将数字重新排列成最小的排列（即升序排列）。

必须原地修改，只允许使用额外常数空间。

### 示例
```
以下是一些例子，输入位于左侧列，其相应输出位于右侧列：

1,2,3 → 1,3,2
3,2,1 → 1,2,3
1,1,5 → 1,5,1
```

## 思路分析
这个逻辑有点难说，不过理解了规律也就好了：
- 从右开始向左遍历：找到第一个满足 a[index] < a[index + 1] 的 index
  - 如果找到了指定 index：在 index 右边找到大于 a[index] 的最小值，进行交换（这里是为了找到下一个更大的排列）
- 从 index + 1 起，反转数组（这步操作也是找到下一个更大的排列）

## 代码
- 时间复杂度O(n)
- 空间复杂度O(n)

```
/**
 * 
 * @param {number[]} nums 
 * @param {number} source 
 * @param {number} target 
 */
const swapNums = (nums, source, target) => {
  const tmp = nums[source];
  nums[source] = nums[target];
  nums[target] = tmp;
}

/**
 * 
 * @param {number[]} nums 
 * @param {number} start 
 */
const reverseNums = (nums, start) => {
  let end = nums.length - 1;

  while(start < end) {
    swapNums(nums, start, end);

    start++;
    end--;
  }
}

/**
 * @param {number[]} nums
 * @return {void} Do not return anything, modify nums in-place instead.
 */
var nextPermutation = function(nums) {
  let findIndex = nums.length - 2;

  while(findIndex >= 0 && nums[findIndex + 1] <= nums[findIndex]) {
    findIndex--;
  }

  // 找到了可交换的值
  if(findIndex >= 0) {
    let tmpIndex = nums.length - 1;
    // 直至找到刚好比 findIndex 大的值进行替换
    while(tmpIndex > findIndex && nums[tmpIndex] <= nums[findIndex]) {
      tmpIndex--;
    }

    swapNums(nums, findIndex, tmpIndex);
  }

  // findIndex 后倒序
  reverseNums(nums, findIndex + 1)    
};
```