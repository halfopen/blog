title: Divide Two Integers
author: Halfopen
tags:
  - leetcode
  - medium
categories: []
date: 2017-12-22 13:40:00
---
### [29\. Divide Two Integers](https://leetcode.com/problems/divide-two-integers/description/)

Difficulty: **Medium**

Divide two integers without using multiplication, division and mod operator.

If it is overflow, return MAX_INT.

不用乘法，除法，取余实现除法

#### Solution
```java
class Solution {
    public int divide(int dividend, int divisor) {
        // 必须要用Long存，不然会丢失数据
        long result = Integer.MAX_VALUE;
        if(divisor==1)return dividend;
        if(divisor==0 || dividend == Integer.MIN_VALUE && divisor == -1)return (int)result;
        long d = Math.abs((long)divisor);
        
        long n = Math.abs((long)dividend);
        
        result = 0;
        while(n>=d){
            long tn = d;
            long tt = 1;
            // 9 /3 = 9-6 3-3,先尽量按倍数减
            while(tn<<1 <n){
                tt = tt<<1;
                tn = tn<<1;
            }
            n -= tn;
            result += tt;
        }
        if(dividend<0 && divisor<0 || dividend>0 && divisor>0)return (int)result;
        return -(int)result;
    }
}
```