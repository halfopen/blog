title: 'Pow(x, n)'
author: Halfopen
tags:
  - leetcode
  - ' medium'
categories:
  - 刷题
date: 2017-12-29 13:13:00
---
### [50\. Pow(x, n)](https://leetcode.com/problems/powx-n/description/)

Difficulty: **Medium**

Implement .

**Example 1:**

```
**Input:** 2.00000, 10
**Output:** 1024.00000
```

**Example 2:**

```
**Input:** 2.10000, 3
**Output:** 9.26100
```

#### Solution
超时
```java
class Solution {
    public double myPow(double x, int n) {
        double result=1.0;
        if(n==0)return 1.0;
        
        int l = Math.abs(n);
        
        // n = 2^a+b
        int a=0,b=0;
        int i=1;
        result = x;
        while(i*2<l){
            i*=2;
            a++;
            result *= result;
        }
        b = l-i;

        while(b-->0){
            result *=x;
        }
        
        
        if(n<0){
            return 1/result;
        }
        return result;
    }
}
```

网上的解法

```c
double myPow(double x, int n) {
    if(n<0) return 1/x * myPow(1/x, -(n+1));
    if(n==0) return 1;
    if(n==2) return x*x;
    if(n%2==0) return myPow( myPow(x, n/2), 2);
    else return x*myPow( myPow(x, n/2), 2);
}
```
double myPow
```c
double myPow(double x, int n) { 
    if(n==0) return 1;
    double t = myPow(x,n/2);
    if(n%2) return n<0 ? 1/x*t*t : x*t*t;
    else return t*t;
}
```
double x
```c
double myPow(double x, int n) { 
    if(n==0) return 1;
    if(n<0){
        n = -n;
        x = 1/x;
    }
    return n%2==0 ? myPow(x*x, n/2) : x*myPow(x*x, n/2);
}
```
iterative one
```c
double myPow(double x, int n) { 
    if(n==0) return 1;
    if(n<0) {
        n = -n;
        x = 1/x;
    }
    double ans = 1;
    while(n>0){
        if(n&1) ans *= x;
        x *= x;
        n >>= 1;
    }
    return ans;
}
```
bit operation
```c++
class Solution {
public:
    double pow(double x, int n) {
    	if(n<0){
    		x = 1.0/x;
    		n = -n;
    	}
    	int unsigned m = n;
        double tbl[32] = {0};
        double result = 1;
        tbl[0] = x;
        for(int i=1;i<32;i++){
            tbl[i] = tbl[i-1]*tbl[i-1];
        }
        for(int i=0;i<32;i++){
            if( m & (0x1<<i) )
            result *= tbl[i];
        }
        return result;
    }
};
```