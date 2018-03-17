title: Kth Largest Element in an Array
author: Halfopen
date: 2018-01-03 16:26:00
tags:
---
### [215\. Kth Largest Element in an Array](https://leetcode.com/problems/kth-largest-element-in-an-array/description/)

Difficulty: **Medium**

Find the **k**th largest element in an unsorted array. Note that it is the kth largest element in the sorted order, not the kth distinct element.

For example,  
Given `[3,2,1,5,6,4]` and k = 2, return 5.

**Note:**  
You may assume k is always valid, 1 ≤ k ≤ array's length.



#### Solution
```java
class Solution {
     public int findKthLargest(int[] nums, int k) {
    	// 大小为k+1,多一个位置暂存新加进来的
        PriorityQueue<Integer> pq = new PriorityQueue<>(k+1);
        
        for(int n:nums){
        	pq.add(n);
        	if(pq.size()>k){
            	pq.poll();
            }
        }
        return pq.poll();
    }
}
```