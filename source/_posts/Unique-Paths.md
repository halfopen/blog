title: Unique Paths
author: Halfopen
tags:
  - leetcode
  - medium
  - dp
categories:
  - 刷题
date: 2017-12-25 20:24:00
---
### [62\. Unique Paths](https://leetcode.com/problems/unique-paths/description/)

Difficulty: **Medium**

A robot is located at the top-left corner of a _m_ x _n_ grid (marked 'Start' in the diagram below).

The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid (marked 'Finish' in the diagram below).

How many possible unique paths are there?

![](https://leetcode.com/static/images/problemset/robot_maze.png)  

Above is a 3 x 7 grid. How many possible unique paths are there?

**Note:** _m_ and _n_ will be at most 100.

#### Solution
```java
class Solution {
    public int uniquePaths(int m, int n) {
        if(m<=0 || n<=0)return 0;
        int[][] dp = new int[m][n];
        
        for(int i=0;i<m;i++){
            dp[i][0] = 1;
        }
        for(int j=0;j<n;j++){
            dp[0][j] = 1;
        }
        
        for(int i=1;i<m;i++){
            for(int j=1;j<n;j++){//一开始把n写成了m
                dp[i][j] = dp[i-1][j]+ dp[i][j-1];
            }
        }
        
        return dp[m-1][n-1]; 返回的不是dp[m][n]
    }
}
```
初始化可以用 `Arrays.fill(row,1);`

虽然是一个水题，但是有更优的解法,因为对称性，用一维的空间就可以

```java
class Solution {
    public int uniquePaths(int m, int n) {
        int[] row = new int[n];
        Arrays.fill(row,1);
        for ( int i = 1; i < m; i++){
            for ( int j = 1; j < n; j++){
                row[j]+=row[j-1];
            }
        }
        return row[n-1];
    }
}
```