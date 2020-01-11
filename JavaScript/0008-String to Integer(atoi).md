# String to Integer (atoi)（8.字符串转整数）

## 题目描述
Implement atoi to convert a string to an integer.

**Hint**: Carefully consider all possible input cases. If you want a challenge, please do not see below and ask yourself what are the possible input cases.

**Notes**: It is intended for this problem to be specified vaguely (ie, no given input specs). You are responsible to gather all the input requirements up front.

**Requirements for atoi**:

The function first discards as many whitespace characters as necessary until the first non-whitespace character is found. Then, starting from this character, takes an optional initial plus or minus sign followed by as many numerical digits as possible, and interprets them as a numerical value.

The string can contain additional characters after those that form the integral number, which are ignored and have no effect on the behavior of this function.

If the first sequence of non-whitespace characters in str is not a valid integral number, or if no such sequence exists because either str is empty or it contains only whitespace characters, no conversion is performed.

If no valid conversion could be performed, a zero value is returned. If the correct value is out of the range of representable values, INT_MAX (2147483647) or INT_MIN (-2147483648) is returned.

## 思路分析
本题就是让实现一个atoi函数：
- 清除前面的空格
- 记录是否有"-" 或 "+"的符号
- 开始计算数值（每读到下一位，将之前的值 * 10）
- 与边界值比较

## 代码
- 时间复杂度O(1)
- 空间复杂度O(1)

```
/**
 * @param {string} str
 * @return {number}
 */
var myAtoi = function(str) {
    if(str.length == 0) {
        return 0;
    }
    
    let index = 0;
    let is_minus = false;
    let length = str.length;
    let result = 0;
    
    // 清除空格
    while(str[index] == " ") {
        index++;
    }
    
    // 符号
    if(str[index] == "-" || str[index] == "+") {
        is_minus = str[index++] == "-" ? true : false;
    }
    
    const int_max = 2147483647;
    const int_min = -2147483648;
    
    // 数值
    while (index < length && str.charAt(index) >= '0' && str.charAt(index) <= '9') {
        if (result > Math.pow(2, 31) / 10 || 
            (result == Math.floor(Math.pow(2, 31) / 10) && str.charAt(index) - '0' > 7)) {
            return is_minus ? int_min : int_max;
        }

        result = 10 * result + (str.charAt(index++) - '0');
    }
    
    return is_minus ? -1 * result : result;
};
```