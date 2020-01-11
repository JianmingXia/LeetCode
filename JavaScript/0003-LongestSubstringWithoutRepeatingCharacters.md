# Longest Substring Without Repeating Characters（3.无重复字符的最长子串）

## 题目描述
Given a string, find the length of the longest substring without repeating characters.

### Example:
```
Given "abcabcbb", the answer is "abc", which the length is 3.

Given "bbbbb", the answer is "b", with the length of 1.

Given "pwwkew", the answer is "wke", with the length of 3. Note that the answer must be a substring, "pwke" is a subsequence and not a substring.
```

## 思路分析
无重复字符的最长子串，从下标0开始，直到遇到第一个重复字符，此时这段字符串即为无重复字符的子串。为了找到最长子串，需要继续进行查找，基于之前的结果，在子串中出现重复的位置向后截断，加上当前的重复字符，继续查找。

## 代码
- 时间复杂度O(n)
- 空间复杂度O(n)

```
/**
 * @param {string} s
 * @return {number}
 */
var lengthOfLongestSubstring = function(s) {
    if(s.length <= 1) {
        return s.length;
    }
    
    let longest_length = 0;
    
    let sub_str = "";
    for(let i = 0; i < s.length; i++) {
        let char = s.charAt(i);
        if(sub_str.indexOf(char) == -1) {
            sub_str += char;
            longest_length = sub_str.length > longest_length ? sub_str.length : longest_length;
        } else {
            sub_str = sub_str.substring(1+sub_str.indexOf(char)) + char;
        }
    }
    
    return sub_str.length > longest_length ? sub_str.length : longest_length;
};
```