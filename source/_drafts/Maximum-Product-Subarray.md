title: Maximum Product Subarray
author: Halfopen
date: 2018-01-04 22:56:23
tags:
---
### [152\. Maximum Product Subarray](https://leetcode.com/problems/maximum-product-subarray/description/)

Difficulty: **Medium**

Find the contiguous subarray within an array (containing at least one number) which has the largest product.

For example, given the array `[2,3,-2,4]`,  
the contiguous subarray `[2,3]` has the largest product = `6`.

求数组中乘积最大的子序列。

#### Solution
因为都是整数，所以不用考虑小数，因此乘积的绝对值肯定是越来越大。

唯一的区别就是可能有负数，因此要保存两个结果，一个正数一个负数结果。

```
class Solution {
    public int maxProduct(int[] nums) {
        
    }
}
```