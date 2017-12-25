title: 无判断Max
author: Halfopen
tags:
  - 程序员面试金典
  - 牛客网
categories:
  - 刷题
date: 2017-12-25 21:25:00
---
### [无判断Max](https://www.nowcoder.com/practice/b0a82250677a4fabb0bc41053fa05013?tpId=8&tqId=11056&tPage=4&rp=4&ru=/ta/cracking-the-coding-interview&qru=/ta/cracking-the-coding-interview/question-ranking)

#### 题目描述
请编写一个方法，找出两个数字中最大的那个。条件是不得使用if-else等比较和判断运算符。

给定两个int a和b，请返回较大的一个数。若两数相同则返回任意一个。

#### 测试样例：

    1，2
    返回：2
    
#### 代码

##### 思路1

如果a和b都是正数的话，a/b转为int只能是0和>0，因此代码如下

```java
import java.util.*;

public class Max {
    public int getMax(int a, int b) {
        // write code here
        int[] arr = new int[]{a,b};
        try{
            return arr[(int)(b/a+0.1)];
        }catch(Exception e){
            return b;
        } 
    }
}
```

##### 思路2
利用补码性质，正数符号位0，负数符号位1

```java

class Max {
public:
    int getMax(int a, int b) {      
        int ret = b;
        (a-b)>>31||(ret = a);// 利用短路性质

        return ret;
    }
};
```
