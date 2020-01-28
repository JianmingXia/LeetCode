# 验证回文串

## 题目描述
给定一个字符串，验证它是否是回文串，只考虑字母和数字字符，可以忽略字母的大小写。

### 示例
```
示例 1:

输入: "A man, a plan, a canal: Panama"
输出: true

示例 2:

输入: "race a car"
输出: false
```

### 说明
本题中，我们将空字符串定义为有效的回文串。

## 思路分析
这题其实就是一个简单“验证回文串”的题，只不过最开始我们需要做个“降噪”操作，这里我贴了两个降噪思路：
- 笨一点的，自己一个字符一个字符进行处理
- 更方便一点的，使用正则进行处理

## 代码
- 时间复杂度O(n)
- 空间复杂度O(n)

### 思路1
```
// 只考虑字母和数字字符，可以忽略字母的大小写
const parseStr = (str) => {
  let res = [];

  for(let i = 0; i < str.length; i++) {
    if(str[i] >= '0' && str[i] <= '9') {
      res.push(str[i]);
    } else if (str[i] >= 'A' && str[i] <= 'Z') {
      res.push(str[i]);
    } else if (str[i] >= 'a' && str[i] <= 'z') {
      res.push(str[i].toUpperCase());
    }
  }

  return res;
}

/**
 * @param {string} s
 * @return {boolean}
 */
var isPalindrome = function(s) {
  if(!s) {
    return true;
  }

  const newStrArr = parseStr(s);
  let start = 0;
  let end = newStrArr.length - 1;

  while (end > start) {
    if (newStrArr[start] != newStrArr[end]) {
      return false;
    }

    start++;
    end--;
  }

  return true;
};
```

### 思路2
```
/**
 * @param {string} s
 * @return {boolean}
 */
var isPalindrome = function(s) {
  const newStr = s.replace(/[^0-9a-zA-Z]/g, '').toLowerCase();

  let start = 0;
  let end = newStr.length - 1;
  
  while (end > start) {
    if (newStr[start] != newStr[end]) {
      return false;
    }

    start++;
    end--;
  }

  return true;
};
```