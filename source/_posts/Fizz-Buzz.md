title: Fizz Buzz
author: Halfopen
tags:
  - leetcode
  - easy
categories:
  - 刷题
date: 2018-12-26 21:40:00
---
### [412\. Fizz Buzz](https://leetcode.com/problems/fizz-buzz/)

Difficulty **Easy**

Write a program that outputs the string representation of numbers from 1 to _n_.

But for multiples of three it should output “Fizz” instead of the number and for the multiples of five output “Buzz”. For numbers which are multiples of both three and five output “FizzBuzz”.

**Example:**

```
n = 15,

Return:
[
    "1",
    "2",
    "Fizz",
    "4",
    "Buzz",
    "Fizz",
    "7",
    "8",
    "Fizz",
    "Buzz",
    "11",
    "Fizz",
    "13",
    "14",
    "FizzBuzz"
]
```

#### Solution

Language: **Java**

```java
class Solution {
    public List<String> fizzBuzz(int n) {
        List<String> l = new ArrayList<>();
        for(int i=1;i<=n;i++){
            String code = ""+i;
            if(i%3==0){
                code = "Fizz";
            }
            if(i%5==0){
                code = "Buzz";
                if(i%3==0){
                    code = "FizzBuzz";
                }
            }
            l.add(code);
        }
        return l;
    }
}
```

不用取余的办法

```java
class Solution {
    public List<String> fizzBuzz(int n) {
        List<String> res = new LinkedList();
        int cnt3 = 3;
        int cnt5 = 5;
        for(int i=1;i<=n;i++){
            if(i == cnt3 && i == cnt5){
                res.add("FizzBuzz");
                cnt3 += 3;
                cnt5 += 5;
            }else if(i == cnt3){
                cnt3 += 3;
                res.add("Fizz");
            }else if(i == cnt5){
                cnt5 += 5;
                res.add("Buzz");
            }else{
                res.add(Integer.toString(i));
            }
        }
        return res;
    }
}
```