title: First Missing Positive
author: Halfopen
date: 2017-12-26 14:59:36
tags:
---
### [41\. First Missing Positive](https://leetcode.com/problems/first-missing-positive/description/)

Difficulty: **Hard**

Given an unsorted integer array, find the first missing positive integer.

For example,  
Given `[1,2,0]` return `3`,  
and `[3,4,-1,1]` return `2`.

Your algorithm should run in _O_(_n_) time and uses constant space.
在O(n)的时间，O(1)的空间内，找出第一个缺失的正数。

#### Solution
没想出答案，这里可以修改数组，因此数组本身就可以存储信息了。

因为原数组有负数，因此把元素标记为负数不能用

但题目中，要求返回第一个缺失的正数，总共数组大小为n,则 可以用a[i]的位置存储i+1

如
 `[1,2,0]` 变成`[1,2,0]` a[2] !=3, 得出3不在
 `[3,4,-1,1]` 变成 `[1,-1,3,4]` a[1]!=2, 得出2不存在
 
```java
class Solution {
    public int firstMissingPositive(int[] nums) {
        for (int i = 0; i < nums.length; i++) {
            while (nums[i] > 0 && nums[i] <= nums.length && nums[nums[i]-1] != nums[i]) {
                swap(nums, i, nums[i]-1);
            }
        }
        
        for(int i = 0; i < nums.length; i++) {
            if (nums[i] != i+1)    return i+1;
        }
        return nums.length+1;
    }
    
    private void swap(int[] nums, int i, int j) {
        int tmp = nums[i];
        nums[i] = nums[j];
        nums[j] = tmp;
    }
}
```