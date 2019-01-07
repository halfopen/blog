title: House Robber
author: Halfopen
tags:
  - leetcode
  - easy
categories:
  - 刷题
date: 2018-12-26 21:43:00
---
### [198\. House Robber](https://leetcode.com/problems/house-robber/)

Difficulty **Easy**

You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, the only constraint stopping you from robbing each of them is that adjacent houses have security system connected and **it will automatically contact the police if two adjacent houses were broken into on the same night**.

Given a list of non-negative integers representing the amount of money of each house, determine the maximum amount of money you can rob tonight **without alerting the police**.

**Example 1:**

**Example 2:**

```
Input: [1,2,3,1]
Output: 4
Explanation: Rob house 1 (money = 1) and then rob house 3 (money = 3).
             Total amount you can rob = 1 + 3 = 4.Input: [2,7,9,3,1]
Output: 12
Explanation: Rob house 1 (money = 2), rob house 3 (money = 9) and rob house 5 (money = 1).
             Total amount you can rob = 2 + 9 + 1 = 12.
```

不相邻的数，相加最大


#### Solution

Language: **Java**

直接递归会超时

```java
class Solution {
	int max = 0;
    public int rob(int[] nums) {
        if(null==nums || nums.length==0)return 0;
        rob(nums, 1, 0);
        rob(nums, 2, nums[0]);
        return max;
    }
    
    public void rob(int[] nums, int i, int sum){
    	if(i>=nums.length){
        	if(sum>max)max = sum;
            return;
        }
        // 不抢
        rob(nums, i+1, sum);
        // 抢这一家
        rob(nums, i+2, sum+nums[i]);
    }
}
```

```java
class Solution {
	int max = 0;
    public int rob(int[] nums) {
        if(nums==null || nums.length==0)return 0;
        int rob = 0;
        int nrob = 0;
        
        for(int i=0;i<nums.length;i++){
            int lastrob = rob;
            // rob
            rob = nrob+nums[i];
            
            // don't rob
            nrob = Math.max(lastrob, nrob);
            
            //System.out.println(rob+" "+nrob);
        }
        return Math.max(rob, nrob);
    }
}
```

