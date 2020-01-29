# 旋转数组

## 题目描述
给定一个数组，将数组中的元素向右移动 k 个位置，其中 k 是非负数。

### 示例
```
示例 1:

输入: [1,2,3,4,5,6,7] 和 k = 3
输出: [5,6,7,1,2,3,4]
解释:
向右旋转 1 步: [7,1,2,3,4,5,6]
向右旋转 2 步: [6,7,1,2,3,4,5]
向右旋转 3 步: [5,6,7,1,2,3,4]

示例 2:

输入: [-1,-100,3,99] 和 k = 2
输出: [3,99,-1,-100]
解释: 
向右旋转 1 步: [99,-1,-100,3]
向右旋转 2 步: [3,99,-1,-100]
```

### 说明
- 尽可能想出更多的解决方案，至少有三种不同的方法可以解决这个问题。
- 要求使用空间复杂度为 O(1) 的 原地 算法。

## 思路分析
从题目中看，就是将数组进行偏移，只不过有个要求：空间复杂度为 O(1)。题目要求向右移动 k 个位置，这里我们先将 k 进行处理，取余数组的长度，避免浪费。

题目还有个要求，要尽可能想更多的解决方案：

### 方案 1
一位一位进行迁移，交换 k * len 次

### 方案 2
一次性迁移 k 位，交换 len 次，这个方案比方案 1 更优一点，避免交换多次，也是我的实现

### 方案 3
- 先反转 0 ~ k - 1 位
- 再反转 k ~ len - 1 位
- 最后反转整个数组

## 代码
- 时间复杂度O(n)
- 空间复杂度O(1)

```
const getMaxDivisor = (a, b) => {
  if(a < b) {
    a = a ^ b;
		b = a ^ b;
		a = a ^ b;
  }
  
	while(a % b != 0) {
		let tmp = a % b;
		a = b;
		b = tmp;
  }
  
	return b;
}

/**
 * @param {number[]} nums
 * @param {number} k
 * @return {void} Do not return anything, modify nums in-place instead.
 */
var rotate = function(nums, k) {
  const len = nums.length;
  k = k % len;
  
  if(k > 0) {
    // 最大公约数
    let maxDivisor = getMaxDivisor(len, k);

    let eachTimes = len / maxDivisor;
    let rounds = maxDivisor;

    // 循环 n 次
    while(rounds--) {
      let index = k - 1 - rounds;
      let tmp = nums[index];

      // 每次交换次数
      for(let i = 0; i < eachTimes; i++) {
        const newIndex = (index + k) % len;

        const newTmp = nums[newIndex];
        nums[newIndex] = tmp;
        tmp = newTmp;

        index = newIndex;
      }
    }
  }

  return nums;
};
```