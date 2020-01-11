# Reverse Integer（7.反转整数）

## 题目描述
Given a 32-bit signed integer, reverse digits of an integer.

### Example 1:
```
Input: 123
Output: 321
```

### Example 2:
```
Input: -123
Output: -321
```

Example 3:
```
Input: 120
Output: 21
```

Note:
Assume we are dealing with an environment which could only store integers within the 32-bit signed integer range: [−2^31,  2^31 − 1]. For the purpose of this problem, assume that your function returns 0 when the reversed integer overflows.

## 思路分析
题目还是很简单的，将一个32位整数反转，如果数值超过范围，则返回0。
在javascript中，先处理整数部分（正负先计入）：
- 分割成数组
- 数组反转
- 转成字符串
- 结合符号与边界值比较

## 代码
- 时间复杂度O(n)
- 空间复杂度O(n)

```
/**
 * @param {number} x
 * @return {number}
 */
var reverse = function(x) {
    let result = Math.abs(x).toString().split("").reverse().join("");
    
    if(x > 0) {
        if(result > Math.pow(2, 31) - 1) {
            return 0;
        }
    } else {
        if(result > Math.pow(2, 31)) {
            return 0;
        }
        result = "-" + result;
    }
    
    return parseInt(result);
};
```