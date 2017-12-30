title: Factorial Trailing Zeroes
author: Halfopen
date: 2017-12-29 15:21:30
tags:
---
### [172\. Factorial Trailing Zeroes](https://leetcode.com/problems/factorial-trailing-zeroes/description/)

Difficulty: **Easy**

Given an integer _n_, return the number of trailing zeroes in _n_!.

**Note:** Your solution should be in logarithmic time complexity.

求n!中，末尾0的个数

等价 n!= a*10^k= a*5^k*2^k

因为10的因子只能是2和5，而每5个数之间，必定有2，所以只要数5的倍数的个数就好了
 n/5 + n/25 + n/125 + n/625 + n/3125+...

#### Solution


```c++
class Solution {
public:
    int trailingZeroes(int n) {
        int count = 0;
        while(n>0){
            count +=n/5;
            n/=5;
        }
        return count;
    }
};
```