title: Longest Consecutive Sequence
author: Halfopen
tags:
  - hard
  - leetcode
categories:
  - 刷题
date: 2018-04-07 20:52:00
---
### [128\. Longest Consecutive Sequence](https://leetcode.com/problems/longest-consecutive-sequence/description/)

Difficulty: **Hard**



Given an unsorted array of integers, find the length of the longest consecutive elements sequence.

For example,  
Given `[100, 4, 200, 1, 3, 2]`,  
The longest consecutive elements sequence is `[1, 2, 3, 4]`. Return its length: `4`.

Your algorithm should run in O(_n_) complexity.



#### Solution
```java
class Solution {
       public int longestConsecutive(int[] nums) {
        Map<Integer,Integer> ranges = new HashMap<>();
        int max = 0;
        for (int num : nums) {
            if (ranges.containsKey(num)) continue;
            
            int left = ranges.getOrDefault(num - 1, 0);
            int right = ranges.getOrDefault(num + 1, 0);
            int sum = left + right + 1;
            max = Math.max(max, sum);
            // 直接更新边界,因为下一次碰到的不可能在内部
            if (left > 0) ranges.put(num - left, sum); 
            if (right > 0) ranges.put(num + right, sum);
            ranges.put(num, sum); 
        }
        return max;
    }
}
```