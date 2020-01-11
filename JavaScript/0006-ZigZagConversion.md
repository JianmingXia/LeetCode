# ZigZag Conversion（6.Z字形转换）

## 题目描述
The string "PAYPALISHIRING" is written in a zigzag pattern on a given number of rows like this: (you may want to display this pattern in a fixed font for better legibility)

```
P   A   H   N
A P L S I I G
Y   I   R
```

And then read line by line: "PAHNAPLSIIGYIR"
Write the code that will take a string and make this conversion given a number of rows:

```
string convert(string text, int nRows);
```

convert("PAYPALISHIRING", 3) should return "PAHNAPLSIIGYIR".

## 思路分析
这个题目其实就是单纯的找规律，多画几张图，找到了规律，一切都很好解决。
我们以row_num = 5行为例：

```
0       8               16
1     7   9           15  17
2   6       10      14
3 5           11  13
4               12
```

- 第0行
  数据：0/8/16 皆是2 * (row_num - 1)的整数倍

- 第1行
  数据：1/7/9/15/17，与第0行相差一位，加1或减1之后，都是 2 * (row_num - 1)的整数倍

- 第4行(n-1)
  数据：4/12，与第0行相差n-1位，加n-1或减n-1之后，都是 2 * (row_num - 1)的整数倍

## 代码
- 时间复杂度O(n)
- 空间复杂度O(n)

```
/**
 * @param {string} s
 * @param {number} numRows
 * @return {string}
 */
var valid = function(numRows, row, index) {
    return (index + row) % ( 2 * (numRows - 1)) == 0 || (index - row) % ( 2 * (numRows - 1)) == 0;
};

var convert = function(s, numRows) {
    let result = "";
    let len = s.length;
    let flag_arr = [];
    if(numRows <= 1) {
        return s;
    }
    
    for(let row = 0; row < numRows; row++) {
        for(let index = row; index < len; index++) {
            if(!flag_arr[index] && valid(numRows, row, index) ) {
                flag_arr[index] = true;
                result += s[index];
            }
        }
    }

    return result;
};
```