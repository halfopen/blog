title: Merge Sorted Array
author: Halfopen
tags:
  - leetcode
  - easy
categories:
  - 刷题
date: 2018-12-26 21:33:00
---
### [88\. Merge Sorted Array](https://leetcode.com/problems/merge-sorted-array/)

Difficulty **Easy**

Given two sorted integer arrays _nums1_ and _nums2_, merge _nums2_ into _nums1_ as one sorted array.

**Note:**

**Example:**

```
Input:
nums1 = [1,2,3,0,0,0], m = 3
nums2 = [2,5,6],       n = 3

Output: [1,2,2,3,5,6]
```

#### Solution

Language: **Java**

```java
class Solution {
    public void merge(int[] nums1, int m, int[] nums2, int n) {
        int l1 = m-1;
        int l2 = n-1;
        int i = m+n -1;
        
        while(i>=0 && l1>=0 && l2>=0){
​
    
            if(nums1[l1]>nums2[l2]){
                nums1[i--] = nums1[l1--];
            }else{
                nums1[i--] = nums2[l2--];
            }
        }
        while(l2>=0){
            nums1[i--] =nums2[l2--];
        }
        
    }
}
```