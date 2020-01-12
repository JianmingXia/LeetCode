# 外观数列

## 题目描述
「外观数列」是一个整数序列，从数字 1 开始，序列中的每一项都是对前一项的描述。前五项如下：

```
1.     1
2.     11
3.     21
4.     1211
5.     111221
```

1 被读作  "one 1"  ("一个一") , 即 11。
11 被读作 "two 1s" ("两个一"）, 即 21。
21 被读作 "one 2",  "one 1" （"一个二" ,  "一个一") , 即 1211。

给定一个正整数 n（1 ≤ n ≤ 30），输出外观数列的第 n 项。

注意：整数序列中的每一项将表示为一个字符串。

### 示例
```
示例 1:

输入: 1
输出: "1"

示例 2:

输入: 4
输出: "1211"
```

## 思路分析
这一题难度也不高，本来打算是通过找规律的方式求解，但是没有成功，于是就按照默认的方法来做：
- 默认值 1
- 遍历字符串来描述当前字符串，尽量找到连续相同的——不断迭代

## 代码
- 时间复杂度O(n)
- 空间复杂度O(n)

```
const countNum = (str) => {
  let res = '';
  for(let i = 0; i < str.length;) {
    let count = 1;
    while(str[i] == str[i + count]) {
      count++;
    }
    res += `${count}${str[i]}`
    i += count;
  }

  return res;
}

/**
 * @param {number} n
 * @return {string}
 */
var countAndSay = function(n) {
  let base = '1';

  for(let i = 2; i <= n; i++) {
    base = countNum(base);
  }

  return base;
};
```