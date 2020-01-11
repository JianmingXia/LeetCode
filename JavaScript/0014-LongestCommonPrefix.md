# 最长公共前缀

## 题目描述
编写一个函数来查找字符串数组中的最长公共前缀。

如果不存在公共前缀，返回空字符串 ""。

### 示例
```
示例 1:
输入: ["flower","flow","flight"]
输出: "fl"

示例 2:
输入: ["dog","racecar","car"]
输出: ""
解释: 输入不存在公共前缀。
```

### 说明
所有输入只包含小写字母 a-z 。

## 思路分析
这一题也是比较简单的，找出字符串的公共前缀，正常的思路从“一个字符”一直遍历到“最短字符串长度”的字符即可。当然在这里我也做了一个优化，运用了二分查找的思想，效率会高不少。
不过我还是出了两个解题思路，第二个解题思路是我在提交之后想到的。
先说第一个思路：运用二分查找的思想进行判断，如果前缀都相等，则 low = mid，继续二分查找；否则 high = mid - 1，继续二分查找。
在做完之后，我看用时上才战胜 72% 的提交，突然想到我每次进行的二分查找，进行比对的次数太多了。故而做了一个小小的优化，还是使用二分查找，不过顺序上有所变化。先找出第 1 个与第 2 个的“最长公共前缀”，然后拿着“最长公共前缀”与第 N 个进行比较，以此类推~。执行时间上也有近 10% 的提升，用时上也战胜了 86%。

## 代码
- 时间复杂度O(n)
- 空间复杂度O(n)

解题思路1：
```
const commonPrefixEqual = (strs, len) => {
  const prefix = strs[0].substring(0, len);
  for(let i = 1; i < strs.length; i++) {
    if(!strs[i].startsWith(prefix)) {
      return false;
    }
  }

  return true;
}

var longestCommonPrefix = function(strs) {
  let minLength = Number.MAX_VALUE;
  if(strs.length === 0) {
    return "";
  }
  if(strs.length === 1) {
    return strs[0];
  }

  for(const str of strs) {
    if(str.length < minLength) {
      minLength = str.length;
    }
  }

  if(minLength === 0) {
    return "";
  }

  let low = 0;
  let high = minLength;
  let index = Math.ceil((low + high) / 2);
  let flag = -1;
  while(low <= high) {
    const equal = commonPrefixEqual(strs, index);

    if(equal) {
      flag = index;

      low = index + 1;
      index = Math.ceil((low + high) / 2);
    } else {
      high = index - 1;
      index = Math.ceil((low + high) / 2);
    }
  }

  return strs[0].substring(0, flag);
};
```

解题思路2：
```
var getTwoStrCommonPrefix = (strOne, strTwo) => {
  let low = 0;
  let high = strOne.length > strTwo.length ? strTwo.length : strOne.length;
  let index = Math.ceil((low + high) / 2);
  let flag = -1;
  while(low <= high) {
    const equal = strOne.substring(0, index) === strTwo.substring(0, index);

    if(equal) {
      flag = index;

      low = index + 1;
      index = Math.ceil((low + high) / 2);
    } else {
      high = index - 1;
      index = Math.ceil((low + high) / 2);
    }
  }

  return strOne.substring(0, flag);
}

var longestCommonPrefix = function(strs) {
  if(strs.length === 0) {
    return "";
  }

  if(strs.length === 1) {
    return strs[0];
  }

  let baseStr = strs[0];
  for(let i = 1; i < strs.length; i++) {
    baseStr = getTwoStrCommonPrefix(baseStr, strs[i]);

    if(baseStr.length === 0) {
      return "";
    }
  }

  return baseStr;
};
```