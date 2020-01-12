# 加一

## 题目描述
给定一个由整数组成的非空数组所表示的非负整数，在该数的基础上加一。

最高位数字存放在数组的首位， 数组中每个元素只存储单个数字。

你可以假设除了整数 0 之外，这个整数不会以零开头。

### 示例
```
示例 1:

输入: [1,2,3]
输出: [1,2,4]
解释: 输入数组表示数字 123。

示例 2:

输入: [4,3,2,1]
输出: [4,3,2,2]
解释: 输入数组表示数字 4321。
```

## 思路分析
这题思路其实比较简单，反向迭代数组，注意进位即可。
千万不要想着直接转成数字进行运算，再转为数组——因为会溢出。。。

## 代码
- 时间复杂度O(n)
- 空间复杂度O(1)

```
/**
 * @param {number[]} digits
 * @return {number[]}
 */
var plusOne = function(digits) {
  for (let i = digits.length - 1; i >= 0; i--) {
    const newValue = digits[i] + 1;
    digits[i] = newValue % 10;

    // 没有进位
    if (digits[i] !== 0) {
      break;
    }
  }

  if (digits[0] === 0) {
    digits.unshift(1);
  }

  return digits;
};
```