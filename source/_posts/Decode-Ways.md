title: Decode Ways
author: Halfopen
tags:
  - leetcode
  - medium
categories:
  - 刷题
date: 2018-01-02 09:48:00
---
### [91\. Decode Ways](https://leetcode.com/problems/decode-ways/description/)

Difficulty: **Medium**

A message containing letters from `A-Z` is being encoded to numbers using the following mapping:

```
'A' -> 1
'B' -> 2
...
'Z' -> 26
```

Given an encoded message containing digits, determine the total number of ways to decode it.

For example,  
Given encoded message `"12"`, it could be decoded as `"AB"` (1 2) or `"L"` (12).

The number of ways decoding `"12"` is 2.

#### Solution

0开头的是错误的
12000 也是错误的，不过12000可以分为 12,000 和1 2000-> (2,000)

递归超时
```java
class Solution {
    public int numDecodings(String s) {
        if(null==s)return 0;
        if(s.length()==0)return 0;
        if(s.charAt(0)=='0'){
            return 0;
        }
        if(s.length()==1){
            return 1;
        }
        
        
        // check the second char
        char c1 = s.charAt(0), c2= s.charAt(1);
        
        if(c1>='3' || (c1=='2' && c2>='7')){
            return numDecodings(s.substring( 1, s.length()));
        }
        if(s.length()==2){
            if(c2=='0')return 1;
            return 2;
        }
        return numDecodings(s.substring(2, s.length()))+numDecodings(s.substring(1, s.length()));
    }
}
```

暴力记忆搜索, dp[i]保存剩余长度为i的时候的长度

```java
class Solution {

    public int numDecodings(String s) {
        if(null==s)return 0;
        if(s.length()==0)return 0;
        if(s.charAt(0)=='0'){
            return 0;
        }
        if(s.length()==1){
            return 1;
        }
        int[] dp = new int[s.length()+1];
        
        return find(s, dp);
        

    }
    
    public int find(String s, int[]dp){
        if(null==s)return 0;
        if(s.length()==0)return 0;
        if(s.charAt(0)=='0'){
            return 0;
        }
        if(s.length()==1){
            return 1;
        }
        
        if(dp[s.length()]>0)return dp[s.length()];
        
        // check the second char
        char c1 = s.charAt(0), c2= s.charAt(1);
        
        if(c1>='3' || (c1=='2' && c2>='7')){
            int r = find(s.substring(1, s.length()), dp);
            dp[s.length()] = r;
            return r;
        }
        if(s.length()==2){
            if(c2=='0')return 1;
            return 2;
        }
        int r =  find(s.substring(2, s.length()), dp)+find(s.substring(1, s.length()),dp);
        dp[s.length()]=r;
        return r;
    }
}
```

动态规划
```java
public class Solution {
    public int numDecodings(String s) {
        int n = s.length();
        if (n == 0) return 0;
        
        int[] memo = new int[n+1];
        memo[n]  = 1;
        memo[n-1] = s.charAt(n-1) != '0' ? 1 : 0;
        
        for (int i = n - 2; i >= 0; i--)
            if (s.charAt(i) == '0') continue;
            else memo[i] = (Integer.parseInt(s.substring(i,i+2))<=26) ? memo[i+1]+memo[i+2] : memo[i+1];
        
        return memo[0];
    }
}
```