title: Coin Change
author: Halfopen
tags:
  - leetcode
  - medium
  - 背包
  - dp
categories:
  - 刷题
date: 2018-01-03 12:05:00
---
### [322\. Coin Change](https://leetcode.com/problems/coin-change/description/)

Difficulty: **Medium**

You are given coins of different denominations and a total amount of money _amount_. Write a function to compute the fewest number of coins that you need to make up that amount. If that amount of money cannot be made up by any combination of the coins, return `-1`.

**Example 1:**  
coins = `[1, 2, 5]`, amount = `11`  
return `3` (11 = 5 + 5 + 1)

**Example 2:**  
coins = `[2]`, amount = `3`  
return `-1`.

**Note**:  
You may assume that you have an infinite number of each kind of coin.



#### Solution

dp[i] 为amount为i的时候，可以用的硬币最少硬币个数

[1,2,5]  dp[0]=1 dp[1] = 1 dp[2]=1 dp[5]=1 dp[3]=dp[2],dp[1] dp[4] = dp[2],dp[3]

贪心行不行？

```java
class Solution {
    public int coinChange(int[] coins, int amount) {
        if(amount<0)return -1;
        if(amount==0)return 0;
        
        Arrays.sort(coins);
        int[] dp = new int[amount+1];

        for(int i=1;i<=amount;++i){
            int min = -1;
            for(int j=0;j<coins.length && coins[j]<=i;++j){
 
                if(dp[i-coins[j]]>=0){
                    int t = dp[i-coins[j]] + 1; // add coins[j]
                    if(min==-1 || min>t)min=t;
                }

            }
            dp[i] = min;
        }
        return dp[amount];
    }
}
```