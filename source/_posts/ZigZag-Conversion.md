title: ZigZag Conversion
author: Halfopen
tags:
  - leetcode
categories:
  - 刷题
date: 2017-11-21 09:42:00
---
### [6\. ZigZag Conversion](https://leetcode.com/problems/zigzag-conversion/description/)

Difficulty: **Medium**

The string `"PAYPALISHIRING"` is written in a zigzag pattern on a given number of rows like this: (you may want to display this pattern in a fixed font for better legibility)

```
P   A   H   N
A P L S I I G
Y   I   R
```

And then read line by line: `"PAHNAPLSIIGYIR"`

Write the code that will take a string and make this conversion given a number of rows:

```
string convert(string text, int nRows);```

`convert("PAYPALISHIRING", 3)` should return `"PAHNAPLSIIGYIR"`.

#### 解题思路
```
P   A   H   N
A P L S I I G
Y   I   R
```
直接看成三个字符串，遍历原字符串，分别添加到三个字符串，最后再把三个字符串拼接起来

#### My Solution
```java
import java.util.*;
class Solution {
    public String convert(String s, int numRows) {
        if(numRows <=1 )return s;
        String[] zigzag = new String[numRows];
        for(int i=0;i<numRows;++i){
            zigzag[i]="";
        }
        String result="";
        int step=1, row=0;
        for(int i=0;i<s.length();++i){
            System.out.println(s.charAt(i));
            zigzag[row]+=""+s.charAt(i);
            if(row==0){
                step=1;
            }else if(row==numRows-1){
                step=-1;
            }
            row+=step;
        }
        
        for(int i=0;i<numRows;++i){
            result+=zigzag[i];
        }
        return result;
    }
}
```