title: Longest Increasing Subsequence
author: Halfopen
tags:
  - dp
  - leetcode
  - medium
categories:
  - 刷题
date: 2017-12-29 18:02:00
---
### [300\. Longest Increasing Subsequence](https://leetcode.com/problems/longest-increasing-subsequence/description/)

计算最长递增子序列

Difficulty: **Medium**

Given an unsorted array of integers, find the length of longest increasing subsequence.

For example,  
Given `[10, 9, 2, 5, 3, 7, 101, 18]`,  
The longest increasing subsequence is `[2, 3, 7, 101]`, therefore the length is `4`. Note that there may be more than one LIS combination, it is only necessary for you to return the length.

Your algorithm should run in O(_n<sup>2</sup>_) complexity.

**Follow up:** Could you improve it to O(_n_ log _n_) time complexity?



#### Solution

搜索
```java
class Solution {

    public int lengthOfLIS(int[] nums) {
        
        int n = nums.length;
        int[] p = new int[n+1];
        for(int i=0;i<n;i++){
            p[i] = nums[i];
        }
        p[n] = Integer.MAX_VALUE;   // 在后面添加一个最大的，确保每个位置都会被比较
        
        return search(n, p)-1;
    }
    
    public int search(int cur, int[] nums){
        if(cur<0){
            return 0;
        }
        int ret = 0;
        
        for(int i=0;i<cur;++i){
            if(nums[cur] > nums[i]){
                ret = Math.max(ret, search(i, nums));
            }
        }
        return ret+1; // 加上那个最小的
    }
}
```

改成dp
```java
class Solution {

    public int lengthOfLIS(int[] nums) {
        
        int n = nums.length;
        int[] p = new int[n+1];
        for(int i=0;i<n;i++){
            p[i] = nums[i];
        }
        int[] dp = new int[n+1];
        p[n] = Integer.MAX_VALUE;   // 在后面添加一个最大的，确保每个位置都会被比较
        
        return search(n, p, dp)-1;
    }
    
    public int search(int cur, int[] nums, int[] dp){
        if(cur<0){
            return 0;
        }
        if(dp[cur]>0)return dp[cur];
        int ret = 0;
        
        for(int i=0;i<cur;++i){
            if(nums[cur] > nums[i]){
                ret = Math.max(ret, search(i, nums, dp));
            }
        }
        dp[cur] = ret+1;
        return dp[cur]; // 加上那个最小的
    }
}
```