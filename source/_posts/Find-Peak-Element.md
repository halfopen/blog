title: Find Peak Element
author: Halfopen
tags:
  - medium
  - leetcode
categories:
  - 刷题
date: 2018-09-17 22:06:00
---
### [162\. Find Peak Element](https://leetcode.com/problems/find-peak-element/description/)

Difficulty: **Medium**



A peak element is an element that is greater than its neighbors.

Given an input array `nums`, where `nums[i] ≠ nums[i+1]`, find a peak element and return its index.

The array may contain multiple peaks, in that case return the index to any one of the peaks is fine.

You may imagine that `nums[-1] = nums[n] = -∞`.

**Example 1:**

```
**Input:** **nums** = `[1,2,3,1]`
**Output:** 2
**Explanation:** 3 is a peak element and your function should return the index number 2.```

**Example 2:**

```
**Input:** **nums** = `[`1,2,1,3,5,6,4]
**Output:** 1 or 5 
**Explanation:** Your function can return either index number 1 where the peak element is 2, 
             or index number 5 where the peak element is 6.
```

**Note:**

Your solution should be in logarithmic complexity.



#### Solution

Language: **Java**

```java
class Solution {
    public int findPeakElement(int[] nums) {
        int l = 0;
        int r = nums.length-1;
        int ret = nums[0];
        while(l<r){
            int mid = (l+r)/2;
            int mid2 = mid+1;
            // keep the bigger one between l and r,l is bigger
            if(nums[mid]<nums[mid2]){
                l = mid2;
            }else{
                r = mid;
            }
        }
        return l;
    }
}
```