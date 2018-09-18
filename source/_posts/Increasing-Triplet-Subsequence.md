title: Increasing Triplet Subsequence
author: Halfopen
date: 2018-09-17 22:17:24
tags:
---
### [334\. Increasing Triplet Subsequence](https://leetcode.com/problems/increasing-triplet-subsequence/description/)

Difficulty: **Medium**



Given an unsorted array return whether an increasing subsequence of length 3 exists or not in the array.

Formally the function should:

> Return true if there exists _i, j, k_  
> such that _arr[i]_ < _arr[j]_ < _arr[k]_ given 0 ≤ _i_ < _j_ < _k_ ≤ _n_-1 else return false.

**Note:** Your algorithm should run in O(_n_) time complexity and O(_1_) space complexity.



**Example 1:**

```
**Input:** <span id="example-input-1-1" style="display: inline;">[1,2,3,4,5]</span>
**Output:** <span id="example-output-1" style="display: inline;">true</span>
```



**Example 2:**

```
**Input:** <span id="example-input-2-1" style="display: inline;">[5,4,3,2,1]</span>
**Output:** <span id="example-output-2" style="display: inline;">false</span>
```







#### Solution

Language: **Java**

```java
class Solution {
    public boolean increasingTriplet(int[] nums) {
        if (nums ==  null || nums.length < 3 ){
            return false;
        }
        int first = Integer.MAX_VALUE;
        int second = Integer.MAX_VALUE;
        
        for(int n:nums){
            if(n<=first)
            {
                first = n;
            }else if(n<=second){
                second = n;
            }else{
                return true;
            }
        }
        return false;
    }
}
```