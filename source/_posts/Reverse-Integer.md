title: Reverse Integer
author: Halfopen
tags:
  - leetcode
  - easy
categories:
  - 刷题
date: 2017-11-22 21:18:00
---
### [7\. Reverse Integer](https://leetcode.com/problems/reverse-integer/description/)

Difficulty: **Easy**

Given a 32-bit signed integer, reverse digits of an integer.

**Example 1:**

```
**Input:** 123
**Output:**  321
```

**Example 2:**

```
**Input:** -123
**Output:** -321
```

**Example 3:**

```
**Input:** 120
**Output:** 21
```

**Note:**  
Assume we are dealing with an environment which could only hold integers within the 32-bit signed integer range. For the purpose of this problem, assume that your function returns 0 when the reversed integer overflows.

#### My Solution
最简单解法，直接用系统的parseInt
```java
class Solution {
    public int reverse(int x) {
        String ts = Math.abs(x)+"";
        StringBuilder sb=new StringBuilder();
        for(int i=ts.length()-1;i>=0;--i){
            sb.append(ts.charAt(i));
        }
        try{
            if(x<0){
                return Integer.parseInt("-"+sb.toString());
            }else{
                return Integer.parseInt(sb.toString());
            }
        }catch(Exception e){
            return 0;
        }
    }
}
```
取余解法
```java
class Solution {
    public int reverse(int x) {
        long rev= 0;
        while( x != 0){
            rev= rev*10 + x % 10;
            x= x/10;
            if( rev > Integer.MAX_VALUE || rev < Integer.MIN_VALUE)
                return 0;
        }
        return (int) rev;
    }
}
```