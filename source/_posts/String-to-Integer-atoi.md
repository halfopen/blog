title: String to Integer (atoi)
author: Halfopen
tags:
  - leetcode
  - medium
categories:
  - 刷题
date: 2017-12-30 17:18:00
---
### [8\. String to Integer (atoi)](https://leetcode.com/problems/string-to-integer-atoi/description/)

Difficulty: **Medium**

Implement <span style="font-family: monospace; display: inline;">atoi</span> to convert a string to an integer.

**Hint:** Carefully consider all possible input cases. If you want a challenge, please do not see below and ask yourself what are the possible input cases.

**Notes:** It is intended for this problem to be specified vaguely (ie, no given input specs). You are responsible to gather all the input requirements up front.

**<font color="red" style="display: inline;">Update (2015-02-10):</font>**  
The signature of the `C++` function had been updated. If you still see your function signature accepts a `const char *` argument, please click the reload button <span class="glyphicon glyphicon-refresh" style="display: inline;"></span>to reset your code definition.

**Requirements for atoi:**

The function first discards as many whitespace characters as necessary until the first non-whitespace character is found. Then, starting from this character, takes an optional initial plus or minus sign followed by as many numerical digits as possible, and interprets them as a numerical value.

The string can contain additional characters after those that form the integral number, which are ignored and have no effect on the behavior of this function.

If the first sequence of non-whitespace characters in str is not a valid integral number, or if no such sequence exists because either str is empty or it contains only whitespace characters, no conversion is performed.

If no valid conversion could be performed, a zero value is returned. If the correct value is out of the range of representable values, INT_MAX (2147483647) or INT_MIN (-2147483648) is returned.



#### Solution

没有考虑 `"    010"`

`"  -0012a42"`应该返回-12？？？

```java
class Solution {
    public static int max = 2147483647;
    public static int min = -2147483648;
    public int myAtoi(String str) {
        long ret = 0;
        int flag=1;
        if(null==str)return 0;
        int len = str.length();
        if(len==0)return 0;
        int index=0;
        while(str.charAt(index)==' ' && index<len){
            index++;
        }
        if(str.charAt(index)=='-'){
            flag = -1;
            index++;
        }else if(str.charAt(index)=='+'){
            index++;
        }
        
        
        for(int i=index;i<len;++i){
            if(str.charAt(i)>='0' && str.charAt(i)<='9'){
                ret = ret*10 + str.charAt(i)-'0';
                
                if(ret*flag>max){
                    return max;
                }
                if(ret*flag<min){
                    return min;
                }
            }else{
                return (int)ret*flag;
            }
        }
        
        return (int)ret*flag;
        
    }
}
```