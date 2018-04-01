title: Find Minimum in Rotated Sorted Array
author: Halfopen
tags:
  - leetcode
  - medium
categories:
  - 刷题
date: 2018-03-18 22:04:00
---
### [153\. Find Minimum in Rotated Sorted Array](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/description/)

Difficulty: **Medium**



Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand.

(i.e., `0 1 2 4 5 6 7` might become `4 5 6 7 0 1 2`).

Find the minimum element.

You may assume no duplicate exists in the array.



#### Solution

1. 如果一开始左边比右边小，说明有序，直接返回第一个。
2. 如果不是1,那么分组有两部分，左边大，右边小，最小的数在大和小之间，用二分查找即可。


```java
class Solution {
    public int findMin(int[] nums) {
        int len = nums.length;
        
        if(nums[0]<nums[len-1])return nums[0];
        
        int left = 0, right=len-1, mid=0;
        
        while(left<right-1){
            mid = (right+left)/2;
            if(nums[mid]>nums[right])left=mid;
            else right=mid;
        }
        if(nums[left]>nums[right])return nums[right];
        return nums[left];
    }
}
```