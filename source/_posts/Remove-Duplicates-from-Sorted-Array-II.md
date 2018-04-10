title: Remove Duplicates from Sorted Array II
author: Halfopen
tags:
  - leetcode
  - medium
categories:
  - 刷题
date: 2018-04-07 20:07:00
---
### [80\. Remove Duplicates from Sorted Array II](https://leetcode.com/problems/remove-duplicates-from-sorted-array-ii/description/)

Difficulty: **Medium**



Follow up for "Remove Duplicates":  
What if duplicates are allowed at most _twice_?

For example,  
Given sorted array _nums_ = `[1,1,1,2,2,3]`,

Your function should return length = `5`, with the first five elements of _nums_ being `1`, `1`, `2`, `2` and `3`. It doesn't matter what you leave beyond the new length.



#### Solution
因为是有序的，所以出现不递增的就是重复的
```java
class Solution {
    public int removeDuplicates(int[] nums) {
        if(nums.length<=2)return nums.length;
        int index = 2;
        for(int i=2;i<nums.length;i++){
            
            if(nums[i]>nums[index-2]){
                nums[index] = nums[i];
                index++;
            }
        }
        return index;
    }
}
```