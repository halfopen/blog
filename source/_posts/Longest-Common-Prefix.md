title: Longest Common Prefix
author: Halfopen
tags:
  - leetcode
  - easy
categories:
  - 刷题
date: 2017-12-11 21:33:00
---
### [14\. Longest Common Prefix](https://leetcode.com/problems/longest-common-prefix/description/)

Difficulty: **Easy**

Write a function to find the longest common prefix string amongst an array of strings.

求一堆数组的最长公共前缀

#### 思路
这里，采用了从完整字符串往前遍历，一步一步缩小前缀的长度

#### My Solution
```
class Solution {
    public String longestCommonPrefix(String[] strs) {
        if(strs.length==0)return "";
        String pre = strs[0];
        for(int i=0;i<strs.length;++i){
            while(strs[i].indexOf(pre)!=0){
                pre = pre.substring(0, pre.length()-1);
            }
        }
        return pre;
    }
}
```