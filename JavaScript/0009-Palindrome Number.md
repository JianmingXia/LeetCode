# Palindrome Number（9.回文数）

## 题目描述
Determine whether an integer is a palindrome. An integer is a palindrome when it reads the same backward as forward.

### Example 1:
```
Input: 121
Output: true
```

### Example 2:
```
Input: -121
Output: false
Explanation: From left to right, it reads -121. From right to left, it becomes 121-. Therefore it is not a palindrome.
```

### Example 3:
```
Input: 10
Output: false
Explanation: Reads 01 from right to left. Therefore it is not a palindrome.
```

Follow up:

Coud you solve it without converting the integer to a string?

## 思路分析
这道题依然不难，判断一个数是否为回文数：
- 个位数——是回文数（快速判断）
- 负数——不是回文数
- 10的整数倍——不是回文数
- \>10的数：将传入值 不断取余，计算反转后的数，判断与传入值是否相等
- 进阶：直接计算反转后的数太麻烦了，比如12121，需要取余5次。有个更简便的方法：
  - 还是将传入值不断取余，不断计算反转后的数，但是现在多加个判断，当反转值 >= 剩下的值时，进行判断，举例：
    - 12321：反转值为123，剩下值为12, 123 / 10 取整== 12
    - 1221：反转值为12，剩下值为12, 12 == 12
    - 1231：反转值为13，剩下值为12, 13 != 12

## 代码
- 时间复杂度O(1)
- 空间复杂度O(1)

### 普通版
```
/**
 * @param {number} x
 * @return {boolean}
 */
var isPalindrome = function(x) {
    if(x >= 0 && x < 10) {
        return true;
    }
    
    if(x < 0 || x % 10 == 0) {
        return false;
    }
    
    let old_num = x;
    let result = 0;
    
    while(old_num > 0) {
        result = result * 10 + old_num % 10;
        old_num = Math.floor(old_num / 10);
    }
    
    return x == result;
};
```

### 优化版
```
/**
 * @param {number} x
 * @return {boolean}
 */
var isPalindrome = function(x) {
    if(x < 10 && x >= 0) {
        return true;
    }
    
    if(x < 0 || x % 10 == 0) {
        return false;
    }
    
    let result = 0;
    
    while(result < x) {
        result = result * 10 + x % 10;
        x = Math.floor(x / 10);
    }
    
    if(result == x) {
        return true;
    }
    
    return x == Math.floor(result / 10);
};
```