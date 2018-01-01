title: Fraction to Recurring Decimal
author: Halfopen
tags:
  - leetcode
  - medium
categories:
  - 刷题
date: 2018-01-01 11:07:00
---
### [166\. Fraction to Recurring Decimal](https://leetcode.com/problems/fraction-to-recurring-decimal/description/)

Difficulty: **Medium**

Given two integers representing the numerator and denominator of a fraction, return the fraction in string format.

If the fractional part is repeating, enclose the repeating part in parentheses.

For example,

*   Given numerator = 1, denominator = 2, return "0.5".
*   Given numerator = 2, denominator = 1, return "2".
*   Given numerator = 2, denominator = 3, return "0.(6)".

求分数的值，如果有无限循环小数，使用括号

#### Solution
```java
public class Solution {
    public String fractionToDecimal(int numerator, int denominator) {
        if (numerator == 0) {
            return "0";
        }
        StringBuilder res = new StringBuilder();
        // "+" or "-"
        res.append(((numerator > 0) ^ (denominator > 0)) ? "-" : "");
        long num = Math.abs((long)numerator);
        long den = Math.abs((long)denominator);
        
        // 整数部分
        res.append(num / den);
        num %= den;
        if (num == 0) {
            return res.toString();
        }
        
        // 小数部分
        res.append(".");
        HashMap<Long, Integer> map = new HashMap<Long, Integer>();
        map.put(num, res.length());
        while (num != 0) {
            num *= 10;
            res.append(num / den);
            num %= den;
            if (map.containsKey(num)) {
                int index = map.get(num);
                res.insert(index, "(");
                res.append(")");
                break;
            }
            else {
            	// 这里记住num的位置
                map.put(num, res.length());
            }
        }
        return res.toString();
    }
}
```