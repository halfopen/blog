title: Container With Most Water
author: Halfopen
tags:
  - medium
  - leetcode
categories:
  - 刷题
date: 2017-12-16 14:55:00
---
### [11\. Container With Most Water](https://leetcode.com/problems/container-with-most-water/description/)

Difficulty: **Medium**

Given _n_ non-negative integers _a<sub style="display: inline;">1</sub>_, _a<sub style="display: inline;">2</sub>_, ..., _a<sub style="display: inline;">n</sub>_, where each represents a point at coordinate (_i_, _a<sub style="display: inline;">i</sub>_). _n_ vertical lines are drawn such that the two endpoints of line _i_ is at (_i_, _a<sub style="display: inline;">i</sub>_) and (_i_, 0). Find two lines, which together with x-axis forms a container, such that the container contains the most water.

Note: You may not slant the container and _n_ is at least 2.

求从数组中，选两个高作为边界，形成一个桶，能装的水最多

如 [6,1,1,4,3,6]  结果是30

#### My Solution
```java
class Solution {
    public int maxArea(int[] height) {
        int i=0,j = height.length-1;
        
        int maxA = 0;
        while(i<j){
            int h=Math.min(height[j],height[i]);
            int s = h*(j-i);
            if(s>maxA){
                maxA = s;
            }
            // 如果左边不是更高的，移动左边
            while(height[i]<=h&&i<j){
                i++;
            }
            
            while(height[j]<=h&&i<j){
                j--;
            }
        }
        return maxA;
    }
}

```