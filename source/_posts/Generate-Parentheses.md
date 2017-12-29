title: Generate Parentheses
author: Halfopen
tags:
  - leetcode
  - medium
categories:
  - 刷题
date: 2017-12-28 21:42:00
---
### [22\. Generate Parentheses](https://leetcode.com/problems/generate-parentheses/description/)

生成匹配的括号

Difficulty: **Medium**

Given _n_ pairs of parentheses, write a function to generate all combinations of well-formed parentheses.

For example, given _n_ = 3, a solution set is:

```
[
  "((()))",
  "(()())",
  "(())()",
  "()(())",
  "()()()"
]
```

#### Solution

每次可以选择左括号或者右括号，用递归比较简单，注意左括号数小于右括号数

```java
class Solution {
    public List<String> generateParenthesis(int n) {
        List<String> l = new ArrayList<>();
        gen(l, "", 0, 0, n);
        return l;
    }
    
    public void gen(List<String>l, String temp, int left, int right, int n){
        if(temp.length()==2*n){ // 不是n
            l.add(temp);
            return;
        }
        
        if(left<n){
            gen(l, temp+"(", left+1, right, n);
        }
        if(right<n && left>right){ // 限制条件
            gen(l, temp+")", left, right+1, n);
        }
        
    }
}
```