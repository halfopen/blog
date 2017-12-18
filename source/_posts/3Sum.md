title: 3Sum
author: Halfopen
tags:
  - leetcode
  - medium
categories:
  - 刷题
date: 2017-12-15 22:20:00
---
### [15\. 3Sum](https://leetcode.com/problems/3sum/description/)

Difficulty: **Medium**

Given an array _S_ of _n_ integers, are there elements _a_, _b_, _c_ in _S_ such that _a_ + _b_ + _c_ = 0? Find all unique triplets in the array which gives the sum of zero.

**Note:** The solution set must not contain duplicate triplets.

```
For example, given array S = [-1, 0, 1, 2, -1, -4],

A solution set is:
[
  [-1, 0, 1],
  [-1, -1, 2]
]
```

#### My Solution
```java
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        List<List<Integer>> result = new ArrayList<>();
            
        int length = nums.length;
        Arrays.sort(nums);

        for(int i=0;i<length;++i){
            int j = i+1, k = length-1;
            int target = -nums[i];
            // 避免出现重复解
            if(i>0 && nums[i]==nums[i-1]){continue;}// 这里不要++i,直接跳过就行

            while(j<k){
                int sum = nums[j]+nums[k];
                if(sum==target){
                    result.add(Arrays.asList(nums[i], nums[j], nums[k]));  
                    --k;++j;
                    // 避免出现重复解
                    while(j<k&&nums[j]==nums[j-1]){
                        ++j;
                    }
                    while(k>j&&nums[k]==nums[k+1]){
                        --k;
                    }
                }else if(sum > target){
                    --k;
                }else{
                    ++j;
                }
            }
        }
        
        return result;
    }
}
```