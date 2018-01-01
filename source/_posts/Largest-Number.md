title: Largest Number
author: Halfopen
tags:
  - leetcode
  - medium
categories:
  - 刷题
date: 2018-01-01 16:43:00
---
### [179\. Largest Number](https://leetcode.com/problems/largest-number/description/)

Difficulty: **Medium**

Given a list of non negative integers, arrange them such that they form the largest number.

For example, given `[3, 30, 34, 5, 9]`, the largest formed number is `9534330`.

Note: The result may be very large, so you need to return a string instead of an integer.

求一堆数组能组成的最大的数

#### Solution

面试和剑指offer都遇到过，Arrays.sort()貌似不能对int[] 用，只能对对象进行排序。

```java
class Solution {
    public String largestNumber(int[] nums) {
        List<Integer> l = new ArrayList<>();
        boolean flag = false;
        for(int i:nums){
            l.add(i);
            if(i!=0)flag=true;
        }
        if(!flag)return "0";
        Collections.sort(l, (b, a)->{
            return (a+""+b).compareTo(b+""+a); // 这个要对
        });
        StringBuilder sb = new StringBuilder();
        for(int i:l){
            sb.append(i+"");
        }
        return sb.toString();
    }
}
```