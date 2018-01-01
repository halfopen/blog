title: Count Primes
author: Halfopen
tags:
  - 素数
  - leetcode
  - easy
categories:
  - 刷题
date: 2018-01-01 17:54:00
---
### [204\. Count Primes](https://leetcode.com/problems/count-primes/description/)

Difficulty: **Easy**

**Description:**

Count the number of prime numbers less than a non-negative number, **_n_**.




#### Solution
```java
public class Solution {
    public int countPrimes(int n) {
        boolean[] notPrime = new boolean[n];
        int count = 0;
        for (int i = 2; i < n; i++) {
            if (notPrime[i] == false) {
                count++;
                for (int j = 2; i*j < n; j++) {
                    // 如果能表示成两个数的乘积，肯定不是素数
                    notPrime[i*j] = true;
                }
            }
        }
        
        return count;
    }
}
```