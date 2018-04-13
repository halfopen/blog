title: Sqrt(x)
author: Halfopen
date: 2018-04-11 10:43:16
tags:
---
### [69\. Sqrt(x)](https://leetcode.com/problems/sqrtx/description/)

Difficulty: **Easy**



Implement `int sqrt(int x)`.

Compute and return the square root of _x_.

**x** is guaranteed to be a non-negative integer.

**Example 1:**

```
**Input:** 4
**Output:** 2
```

**Example 2:**

```
**Input:** 8
**Output:** 2
**Explanation:** The square root of 8 is 2.82842..., and since we want to return an integer, the decimal part will be truncated.
```



#### Solution
普通方法
```java
class Solution {
    public int mySqrt(int x) {
        long i = x;
        while(i*i<=x ){
              i++;
        };
        return (int)i;
    }
}
```


牛顿法

求 x^2=D,相当于求 y = x^2-D的解

从x = D开始，向0的位置开始移动。 x = D和曲线交点是 (D, D^2-D),作切线y-(D^2-D)=2*D(x-D)，新的交点是 ( (1+D)/2, 0)

同理，如果上一个位置是i,新的交点位置就是 `(D+i*i)/(2*i)`

```java
class Solution {
    public int mySqrt(int x) {
        long i = x;
        while(i*i>x ){
            i = (x+i*i)/(2*i);
        };
        return (int)i;
    }
}
```