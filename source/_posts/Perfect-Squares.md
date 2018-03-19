title: Perfect Squares
author: Halfopen
tags:
  - leetcode
  - medium
categories:
  - 刷题
date: 2018-03-17 08:49:00
---
### [279\. Perfect Squares](https://leetcode.com/problems/perfect-squares/description/)

Difficulty: **Medium**



Given a positive integer _n_, find the least number of perfect square numbers (for example, `1, 4, 9, 16, ...`) which sum to _n_.

For example, given _n_ = `12`, return `3` because `12 = 4 + 4 + 4`; given _n_ = `13`, return `2` because `13 = 4 + 9`.





#### Solution

主要思想还是动态规划

通过观察可以得出，dp[j*j]=1,目的是求dp[n]

观察 dp[13],比13小的平方数有 1，4，9,

那么dp[13]取：

dp[1]+dp[13-1]、 dp[4]+dp[13-4]、dp[9]+dp[13-9]中最小的那一个

因此，只要从dp[1]计算到dp[n]即可。

```java
class Solution {
    public int numSquares(int n) {
        
        int[] dp = new int[n+1];
        
        
        // 初始化
        for(int i=0;i<=n;i++){
            dp[i] = 0;
        }
        
        for(int i=1;i*i<=n;i++){
            dp[i*i] = 1;
        }
        
        // 计算dp
        for(int i=1;i<=n;i++){
            if(dp[i]==0){
                int min = i;
                // 枚举所有小于n的平方和
                for(int j=1;j*j<i;j++){
                    int n1 = j*j, n2 = i-j*j;
                    int temp = dp[n1] + dp[n2];
                    if(temp<min)min = temp;
                }
                dp[i] = min;
                
            }
        }
        
        return dp[n];
    }
}


```

然后看到一个最优解法， 数学原理：四平方和定理 https://zh.wikipedia.org/wiki/%E5%9B%9B%E5%B9%B3%E6%96%B9%E5%92%8C%E5%AE%9A%E7%90%86


```

class Solution {
    public int numSquares(int n) {
        if (isSquare(n)) return 1;

        while ((n&3) == 0) n >>=2;
        if ((n&7) == 7) return 4;
        int sqrt = (int)Math.sqrt(n);
        for (int i=1;i<=sqrt;i++) 
            if (isSquare(n - i*i)) return 2;
        return 3;
    }

    private boolean isSquare(int n) {
        int sqrt = (int)Math.sqrt(n);
        return (sqrt * sqrt) == n;
    }
}
```

http://www.cnblogs.com/grandyang/p/4800552.html