title: Palindrome Number
author: Halfopen
tags:
  - 回文
  - leetcode
  - easy
categories:
  - 刷题
date: 2017-12-16 12:23:00
---
### [9\. Palindrome Number](https://leetcode.com/problems/palindrome-number/description/)

Difficulty: **Easy**

Determine whether an integer is a palindrome. Do this without extra space.
判断一个数字是否为回文数，不使用额外的空间

**Some hints:**

Could negative integers be palindromes? (ie, -1) 负数不是

If you are thinking of converting the integer to string, note the restriction of using extra space. 如果把数字转为字符串，就不满足不使用额外空间

You could also try reversing an integer. However, if you have solved the problem "Reverse Integer", you know that the reversed integer might overflow. How would you handle such case?
直接把数字反转，可能会超出空间
There is a more generic way of solving this problem.



#### My Solution

以12321为例

    rev	0		1		12
    x	12321	1232	123

```java
class Solution {
    public boolean isPalindrome(int x) {
        if(x<0 || (x!=0&& x%10==0))return false;
        if(x<10)return true;
        int rev = 0;
        
        while(x>rev){
            rev = rev*10 + x%10;
            x = x/10;
        }
        return (x==rev || x==rev/10); // 如果数字是偶数，就是x==rev
    }
}
```