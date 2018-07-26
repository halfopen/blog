title: Implement strStr()
author: Halfopen
tags:
  - leetcode
  - easy
categories:
  - 刷题
date: 2018-05-30 19:13:00
---
### [28\. Implement strStr()](https://leetcode.com/problems/implement-strstr/description/)

Difficulty: **Easy**



Implement .

Return the index of the first occurrence of needle in haystack, or **-1** if needle is not part of haystack.

**Example 1:**

```
**Input:** haystack = "hello", needle = "ll"
**Output:** 2
```

**Example 2:**

```
**Input:** haystack = "aaaaa", needle = "bba"
**Output:** -1
```

**Clarification:**

What should we return when `needle` is an empty string? This is a great question to ask during an interview.

For the purpose of this problem, we will return 0 when `needle` is an empty string. This is consistent to C's  and Java's .

只要写出暴力方法即可


#### Solution
```
class Solution {
    public int strStr(String haystack, String needle) {
        if(null==needle || needle.length()==0)return 0;
        for(int i=0;i<=haystack.length()-needle.length();i++){ // 如果i不写成haystack.length()-needle.length(),会超时，这样写还可以避免needle比hastack长的问题
            int start=i;
            // 匹配子串
            for(int j=0;j<needle.length()&&i<haystack.length();j++){
                if(haystack.charAt(i) == needle.charAt(j)){
                    i++;
                    if(j==needle.length()-1)return start;
                }else{
                    break;
                }
            }
            i = start;
        }
        return -1;
    }
}
```