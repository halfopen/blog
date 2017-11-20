title: Longest Substring Without Repeating Characters
author: Halfopen
tags:
  - leetcode
categories:
  - 刷题
date: 2017-11-20 18:56:00
---
## 题目描述：
Given a string, find the length of the longest substring without repeating characters. For example, the longest substring without repeating letters for "abcabcbb" is "abc", which the length is 3. For "bbbbb" the longest substring is "b", with the length of 1.

## 题目大意：
给定一个字符串，从中找出不含重复字符的最长子串的长度。例如，"abcabcbb"的不含重复字母的最长子串为"abc"，其长度是3。"bbbbb"的最长子串是"b"，长度为1。

## 解题思路：
“滑动窗口法”
用一个map记录字符最后一次出现的位置
用j记录子串的起点，用i遍历
如果字符出现过，判断出现过的位置和j的大小，取较大的一个
i-j+1就是子串的长度，每次不断更新结果，取较大的一个

## 代码
```java
class Solution {
        public int lengthOfLongestSubstring(String s) {
            int result=0;
            Map<Character, Integer> map = new HashMap<>();
            char c;
            int j=0;
            for(int i=0;i<s.length();++i){
                c = s.charAt(i);
                if(map.containsKey(c)){
                    j = Math.max(map.get(c)+1, j);  
                }
                map.put(c, i);
                
                result = Math.max(i-j+1, result);
            }
            return result;
        }
    }
```