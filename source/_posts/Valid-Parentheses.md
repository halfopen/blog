title: Valid Parentheses
author: Halfopen
tags:
  - leetcode
  - easy
categories:
  - 刷题
date: 2017-12-11 21:59:00
---
### [20\. Valid Parentheses](https://leetcode.com/problems/valid-parentheses/discuss/)

Difficulty: **Easy**

Given a string containing just the characters `'('`, `')'`, `'{'`, `'}'`, `'['` and `']'`, determine if the input string is valid.

The brackets must close in the correct order, `"()"` and `"()[]{}"` are all valid but `"(]"` and `"([)]"` are not.

括号匹配，使用栈即可

#### My Solution
```java
class Solution {
    public boolean isValid(String s) {
        Stack<Character> st = new Stack<>();
        Map<Character, Character> map = new HashMap<>();
        map.put('{', '}');
        map.put('[', ']');
        map.put('(', ')');
        for(int i=0;i<s.length();++i){
            char c = s.charAt(i);
            if(c == '['||c=='{'||c=='('){
                st.push(c);
            }else if(!st.empty() && c == map.get(st.peek())){
                st.pop();
            }else{
                return false;
            }
        }
        return st.empty();
    }
}
```

一个不用Map的方法
```java
public boolean isValid(String s) {
	Stack<Character> stack = new Stack<Character>();
	for (char c : s.toCharArray()) {
		if (c == '(')
			stack.push(')');
		else if (c == '{')
			stack.push('}');
		else if (c == '[')
			stack.push(']');
		else if (stack.isEmpty() || stack.pop() != c)
			return false;
	}
	return stack.isEmpty();
}

```