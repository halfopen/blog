title: Reverse Bits
author: Halfopen
tags:
  - leetcode
  - easy
categories: []
date: 2018-04-10 19:25:00
---
### [190\. Reverse Bits](https://leetcode.com/problems/reverse-bits/description/)

Difficulty: **Easy**



Reverse bits of a given 32 bits unsigned integer.

For example, given input 43261596 (represented in binary as **00000010100101000001111010011100**), return 964176192 (represented in binary as **00111001011110000010100101000000**).

**Follow up**:  
If this function is called many times, how would you optimize it?

Related problem:



#### Solution



系统自带方法
```java
public class Solution {
    public int reverseBits(int n) {
        return Integer.reverse(n);
    }
}
```

```java
public int reverseBits(int n) {
    int result = 0;
    for(int i=0; i<32; i++){
        result <<= 1;
        result += n&1;
        n >>= 1;
    }
    return result;
}
```