title: 3Sum Closest
author: Halfopen
tags:
  - medium
  - leetcode
categories:
  - 刷题
date: 2017-12-16 11:22:00
---
### [16\. 3Sum Closest](https://leetcode.com/problems/3sum-closest/description/)

Difficulty: **Medium**

在数组中找出和target最接近的三个数的和

Given an array _S_ of _n_ integers, find three integers in _S_ such that the sum is closest to a given number, target. Return the sum of the three integers. You may assume that each input would have exactly one solution.

```
    For example, given array S = {-1 2 1 -4}, and target = 1.

    The sum that is closest to the target is 2\. (-1 + 2 + 1 = 2).
```

#### My Solution O(n^2)
```java
class Solution {
    public int threeSumClosest(int[] nums, int target) {
        int result = Integer.MAX_VALUE;
        int min = result;
        Arrays.sort(nums);
        
        for(int i=0;i<nums.length-2;++i){//length-2,至少有三个数
            int j = i+1, k = nums.length-1;
            // 一个从i后面的位置开始遍历，一个从最后的位置开始遍历
            while(j<k){
                int d = target-nums[i]-nums[j]-nums[k]; // 相加
                if(Math.abs(d)<min){// 
                    min = Math.abs(d);
                    result = nums[i]+nums[j]+nums[k]; // 返回不要写错
                }
                if(d>=0){
                    ++j;
                }else{
                    --k;
                }
            }
        }
        return result;
    }
}
```