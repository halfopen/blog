title: Letter Combinations of a Phone Number
author: Halfopen
tags:
  - leetcode
  - medium
categories:
  - 刷题
date: 2017-12-16 12:14:00
---
### [17\. Letter Combinations of a Phone Number](https://leetcode.com/problems/letter-combinations-of-a-phone-number/description/)

Difficulty: **Medium**

Given a digit string, return all possible letter combinations that the number could represent.

A mapping of digit to letters (just like on the telephone buttons) is given below.

![](http://upload.wikimedia.org/wikipedia/commons/thumb/7/73/Telephone-keypad2.svg/200px-Telephone-keypad2.svg.png)

```
**Input:**Digit string "23"
**Output:** ["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"].
```

**Note:**  
Although the above answer is in lexicographical order, your answer could be in any order you want.

#### My Solution

直接用一个递归解决

```java
class Solution {
    String digits;
    List<String> l = new ArrayList<>();
    private String[] letter = {"", "", "abc", "def", "ghi", "jkl", "mno", "pqrs", "tuv", "wxyz"};
    public List<String> letterCombinations(String digits) {
        this.digits = digits;
        get("", 0);
        
        return l;
    }
    
    public void get(String temp, int current){
        if(current>this.digits.length()-1){
            if(temp.length()>0)l.add(temp); // 记得判断空的输入
            return;
        }
        
        String value = letter[digits.charAt(current)-'0'];
        for(int i=0;i<value.length();++i){
            get(temp+value.charAt(i), current+1);
        }
    }
}

```