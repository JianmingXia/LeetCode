# 颠倒二进制位

## 题目描述
颠倒给定的 32 位无符号整数的二进制位。

### 示例
```
示例 1：

输入: 00000010100101000001111010011100
输出: 00111001011110000010100101000000
解释: 输入的二进制串 00000010100101000001111010011100 表示无符号整数 43261596，
      因此返回 964176192，其二进制表示形式为 00111001011110000010100101000000。
示例 2：

输入：11111111111111111111111111111101
输出：10111111111111111111111111111111
解释：输入的二进制串 11111111111111111111111111111101 表示无符号整数 4294967293，
      因此返回 3221225471 其二进制表示形式为 10101111110010110010011101101001。
```

### 说明
- 请注意，在某些语言（如 Java）中，没有无符号整数类型。在这种情况下，输入和输出都将被指定为有符号整数类型，并且不应影响您的实现，因为无论整数是有符号的还是无符号的，其内部的二进制表示形式都是相同的。
- 在 Java 中，编译器使用二进制补码记法来表示有符号整数。因此，在上面的 示例 2 中，输入表示有符号整数 -3，输出表示有符号整数 -1073741825。

## 思路分析
这一题就是将当前数字转为二进制，再进行反转，然后再转为数字——思路比较简单，实现方式倒是有几个。

## 代码
- 时间复杂度O(n)
- 空间复杂度O(n)

### 解法1
```
const getBitsFromNum = (num) => {
  let res = [];
  
  // 初始化
  for(let i = 0; i < 32; i++) {
    res.push(0);
  }

  let index = 0;
  while(num) {
    res[32 - index - 1] = num % 2;

    num = parseInt(num / 2);
    index++;
  }

  return res;
};

const getNumFromBits = (bits) => {
  let res = 0;
  for(let bit of bits) {
    res = 2 * res + bit;
  }

  return res;
};

/**
 * @param {number} n - a positive integer
 * @return {number} - a positive integer
 */
var reverseBits = function(n) {
  const bits = getBitsFromNum(n);

  return getNumFromBits(bits.reverse());
};
```

使用系统函数：

```
/**
 * @param {number} n - a positive integer
 * @return {number} - a positive integer
 */
var reverseBits = function(n) {
  return parseInt(n.toString(2).padStart(32, 0).split('').reverse().join(''), 2)
};
```

### 解法2

```
/**
 * @param {number} n - a positive integer
 * @return {number} - a positive integer
 */
var reverseBits = function(n) {
  let res = 0;
  
  let times = 32;
  while(times--){
    res = res * 2 + n % 2;
    n = parseInt(n / 2);
  }

  return res;
};
```