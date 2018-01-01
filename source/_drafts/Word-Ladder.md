title: Word Ladder
author: Halfopen
tags:
  - leetcdoe
  - medium
categories:
  - 刷题
date: 2018-01-01 14:27:00
---
### [127\. Word Ladder](https://leetcode.com/problems/word-ladder/description/)

Difficulty: **Medium**

Given two words (_beginWord_ and _endWord_), and a dictionary's word list, find the length of shortest transformation sequence from _beginWord_ to _endWord_, such that:

1.  Only one letter can be changed at a time.
2.  Each transformed word must exist in the word list. Note that _beginWord_ is _not_ a transformed word.

每次只能改变一个字母，改变之后的单词必须在wordlist中

For example,

Given:  
_beginWord_ = `"hit"`  
_endWord_ = `"cog"`  
_wordList_ = `["hot","dot","dog","lot","log","cog"]`  

As one shortest transformation is `"hit" -> "hot" -> "dot" -> "dog" -> "cog"`,  
return its length `5`.

**Note:**  

*   Return 0 if there is no such transformation sequence.
*   All words have the same length.
*   All words contain only lowercase alphabetic characters.
*   You may assume no duplicates in the word list.
*   You may assume _beginWord_ and _endWord_ are non-empty and are not the same.

**<font color="red" style="display: inline;">UPDATE (2017/1/20):</font>**  
The _wordList_ parameter had been changed to a list of strings (instead of a set of strings). Please reload the code definition to get the latest changes.

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

暴力dp, dp[i]保存剩余长度为i的时候的长度

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