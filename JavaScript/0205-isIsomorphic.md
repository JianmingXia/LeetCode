# 同构字符串

## 题目描述
给定两个字符串 s 和 t，判断它们是否是同构的。

如果 s 中的字符可以被替换得到 t ，那么这两个字符串是同构的。

所有出现的字符都必须用另一个字符替换，同时保留字符的顺序。两个字符不能映射到同一个字符上，但字符可以映射自己本身。

### 示例
```
示例 1:

输入: s = "egg", t = "add"
输出: true

示例 2:

输入: s = "foo", t = "bar"
输出: false

示例 3:

输入: s = "paper", t = "title"
输出: true
```

### 说明
你可以假设 s 和 t 具有相同的长度。

## 思路分析
### 思路 1
这个思路应该比较容易想到，我们在替换字符时，肯定是要统一替换的，不能同一个字符用不同的符号替代。我们我的思路比较简单，第一个出现的就是 0，依次类推~

### 思路 2
思路 1 其实是先转换成“未知数”，最后再判断同个位置上的未知数。思路 2 有的取巧，对每个位置的值，判断在两个字符串中第一次出现的位置是否相同，这个思路也是可以解决的。


## 代码
- 时间复杂度O(n)
- 空间复杂度O(n)

### 思路 1
```
const getCharToNum = str => {
  let chars = [];
  let res = [];

  for (let i = 0; i < str.length; i++) {
    // 元素
    const index = chars.indexOf(str[i]);
    if (index >= 0) {
      res.push(index);
    } else {
      chars.push(str[i]);
      res.push(res.length);
    }
  }

  return res;
};

/**
 * @param {string} s
 * @param {string} t
 * @return {boolean}
 */
var isIsomorphic = function(s, t) {
  const num1 = getCharToNum(s);

  const num2 = getCharToNum(t);

  return JSON.stringify(num1) === JSON.stringify(num2);
};
```

### 思路 2
```
/**
 * @param {string} s
 * @param {string} t
 * @return {boolean}
 */
var isIsomorphic = function(s, t) {
  for(let i = 0; i < s.length; i++) {
    if(s.indexOf(s[i]) != t.indexOf(t[i])) {
      return false;
    }
  }
  
  return true;
};
```