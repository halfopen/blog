title: Length of Last Word
author: Halfopen
tags:
  - leetcode
  - easy
categories:
  - 刷题
date: 2018-07-26 21:11:00
---
### [58\. Length of Last Word](https://leetcode.com/problems/length-of-last-word/description/)

Difficulty: **Easy**



Given a string _s_ consists of upper/lower-case alphabets and empty space characters `' '`, return the length of last word in the string.

If the last word does not exist, return 0.

**Note:** A word is defined as a character sequence consists of non-space characters only.

**Example:**

```
**Input:** "Hello World"
**Output:** 5
```



#### Solution

不用split,遍历一下就行了，找到最后一个空格的下标，用字符长度相减

Language: **Java**

```java
class Solution {
    public int lengthOfLastWord(String s) {
        s = s.trim();
        if(s.length()==0)return 0;
        int j;
        for(j=s.length()-1;j>0;j--){
            if(s.charAt(j)==' '){
                j++;
                break;
            }
        }
        return s.length()-j;
    }
}
```