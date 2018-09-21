title: Longest Valid Parentheses
author: Halfopen
tags:
  - leetcode
  - hard
categories:
  - 刷题
date: 2018-09-20 12:17:00
---
### [32\. Longest Valid Parentheses](https://leetcode.com/problems/longest-valid-parentheses/description/)

Difficulty: **Hard**



Given a string containing just the characters `'('` and `')'`, find the length of the longest valid (well-formed) parentheses substring.

**Example 1:**

```
**Input:** "(()"
**Output:** 2
**Explanation:** The longest valid parentheses substring is `"()"`
```

**Example 2:**

```
**Input:** "`)()())`"
**Output:** 4
**Explanation:** The longest valid parentheses substring is `"()()"`
```



#### Solution

Language: **Java**
直接暴力标记会内存溢出
```java
class Solution {
    public int longestValidParentheses(String s) {
        int[][] dp = new int[s.length()][s.length()];
        int[] mark = new int[s.length()];
        int ret = 0;
        
        // 从匹配的括号大小开始，最小的括号长度是2,然后是4,然后是6
        for(int i=2;i<=s.length();i+=2){
            boolean match = false;
            // 合并包含
            for(int j=0;j+i-1<s.length();j++){
                //System.out.println("check "+j+" "+(j+i-1));
                if(mark[j]==0&&s.charAt(j)=='('&&s.charAt(j+i-1)==')'){
                    
                    if((i>2&&dp[j+1][j+i-2]==1)||i==2){
                            dp[j][j+i-1]=1;
                            mark[j]=1;
                            mark[j+i-1]=1;
                    }
                }
                
            }
            int j=0;
            while(j<s.length()){
                if(mark[j]==1){
                    int k=j;
                    while(k+1<s.length()&&mark[k+1]==1){
                        k++;
                    }
                    dp[j][k]=1;
                }
                j++;
            }
            
        }
        for(int j=0;j<s.length();j++){
            //System.out.println(mark[j]);
                if(mark[j]==1){
                    int k = j;
                    while(k<s.length()&&mark[k]==1)k++;
                    dp[j][k-1]=1;
                    ret = ret>k-j?ret:k-j;
                }
                
            }
        return ret;
    }
}
```

使用动态规划

```java
class Solution {
    public int longestValidParentheses(String s) {
        int[] dp = new int[s.length()+1];
        int max = 0;
        int parenCount = 0;
        for (int i=0;i<s.length();++i) {
            char c = s.charAt(i);
            if (c == '(') {
                parenCount++; // 记录(的个数
            } else if (c == ')' && parenCount > 0) {
                parenCount--; // 匹配一个左边的括号
                int prev = dp[i-1]; // 上一个括号的长度
                dp[i] = prev + dp[i - prev - 2] + 2; // 当前括号的长度 = 上一个括号的长度+匹配之前相邻括号的长度+当前的两个括号
                max = Math.max(max, dp[i]);
            }
        }
        return max;

    }
}
```