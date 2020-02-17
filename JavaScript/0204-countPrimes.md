# 计数质数

## 题目描述
统计所有小于非负整数 n 的质数的数量。

### 示例
```
示例:

输入: 10
输出: 4
解释: 小于 10 的质数一共有 4 个, 它们是 2, 3, 5, 7 。
```

## 思路分析
### 思路 1
思路比较简单，从数字 2 开始判断当前数字是否为质数，并同时计数。

### 思路 2
思路 1 的方案比较简单，而且会出现重复计算的情况，比如判断 25 是否为质数：从 2 => 5，不断进行判断是否能整除，此时 2 4 属于重复判断。为了解决这个问题，我会将之前的质数保存下来，迭代时使用质数来进行判断。

### 思路 3
前面两个思路是比较被动的，无法主动排除目标，这里引入了[埃拉托斯特尼筛法](https://zh.wikipedia.org/wiki/%E5%9F%83%E6%8B%89%E6%89%98%E6%96%AF%E7%89%B9%E5%B0%BC%E7%AD%9B%E6%B3%95)。

## 代码
- 时间复杂度O(n)
- 空间复杂度O(n)

### 思路1
```
const isPrime = (num) => {
  for(let i = 2; i * i <= num; i++) {
    if(num % i === 0) {
      return false;
    }
  }

  return true;
}

/**
 * @param {number} n
 * @return {number}
 */
var countPrimes = function(n) {
  let count = 0;

  for(let i = 2; i < n; i++) {
    if(isPrime(i)) {
      count++;
    }
  }

  return count;
};
```

### 思路2
```
const isPrime = (num, primes) => {
  if(primes.length === 0) {
    return true;
  }

  for(let i = 0; i < primes.length; i++) {
    if(num % primes[i] === 0) {
      return false;
    } else if(primes[i] * primes[i] > num) {
      return true;
    }
  }

  return true;
}

/**
 * @param {number} n
 * @return {number}
 */
var countPrimes = function(n) {
  const primes = [];

  for(let i = 2; i < n; i++) {
    if(isPrime(i, primes)) {
      primes.push(i);
    }
  }

  return primes.length;
};
```

### 思路 3
```
/**
 * @param {number} n
 * @return {number}
 */
var countPrimes = function(n) {
  const primes = new Array(n);

  let count = 0;
  for(let i = 2; i < n; i++) {
    if(!primes[i]) {
      count++;
      for(let j = 2; j * i < n; j++) {
        primes[j * i] = true;
      }
    }
  }

  return count;
};
```