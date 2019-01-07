title: Shortest Palindrome
author: Halfopen
date: 2018-09-26 19:57:26
tags:
---
### [214\. Shortest Palindrome](https://leetcode.com/problems/shortest-palindrome/description/)

Difficulty: **Hard**



Given a string _**s**_, you are allowed to convert it to a palindrome by adding characters in front of it. Find and return the shortest palindrome you can find by performing this transformation.

**Example 1:**

```
**Input:** `"aacecaaa"`
**Output:** `"aaacecaaa"`
```

**Example 2:**

```
**Input:** `"abcd"`
**Output:** `"dcbabcd"````



#### Solution

Language: **Java**

```java
class Solution {
    public String shortestPalindrome(String s) {
        String reverse = new StringBuilder(s).reverse().toString();
        int i=0;
        for(i=0;i<s.length();i++){
            if(s.startsWith(reverse.substring(i))){
                break; 
            }
        }
        return reverse.substring(0, i)+s;
    }
}
```