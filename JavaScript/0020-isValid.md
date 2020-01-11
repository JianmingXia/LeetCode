# 有效的括号

## 题目描述
给定一个只包括 '('，')'，'{'，'}'，'['，']' 的字符串，判断字符串是否有效。

有效字符串需满足：

左括号必须用相同类型的右括号闭合。
左括号必须以正确的顺序闭合。
注意空字符串可被认为是有效字符串。

### 示例
```
示例 1:
输入: "()"
输出: true

示例 2:
输入: "()[]{}"
输出: true

示例 3:
输入: "(]"
输出: false

示例 4:
输入: "([)]"
输出: false

示例 5:
输入: "{[]}"
输出: true
```

## 思路分析
这题依然比较简单，一个简单的入栈出栈实现，中间加了一些分支判断，主要是为了优化细节部分：
- 长度如果是奇数，必然 false
- 如果当前栈是空的，出现的字符是后半段，必然 false

## 代码
- 时间复杂度O(n)
- 空间复杂度O(n)

```
const chars = ["(", "{", "[", "]", "}", ")"];
const charsLen = chars.length;
const secondHalf = Math.ceil(charsLen / 2);

/**
 * @param {string} s
 * @return {boolean}
 */
const isValid = function(s) {
  if (typeof s === "undefined") {
    return false;
  }

  if (s.length % 2 === 1) {
    return false;
  }

  let res = [];
  for (let i = 0; i < s.length; i++) {
    const index = chars.indexOf(s[i]);

    // if (index < 0) {
    //   return false;
    // }

    if (res.length === 0) {
      if (index >= secondHalf) {
        return false;
      }

      res.push(index);
      continue;
    }

    if (res[res.length - 1] + index === chars.length - 1) {
      res.pop();
    } else {
      res.push(index);
    }
  }

  return res.length === 0;
};
```