title: Find the Duplicate Number
author: Halfopen
tags:
  - leetcode
  - medium
categories:
  - 刷题
date: 2018-03-18 22:05:00
---
### [287\. Find the Duplicate Number](https://leetcode.com/problems/find-the-duplicate-number/description/)

Difficulty: **Medium**



Given an array _nums_ containing _n_ + 1 integers where each integer is between 1 and _n_ (inclusive), prove that at least one duplicate number must exist. Assume that there is only one duplicate number, find the duplicate one.

**Note:**  

1.  You **must not** modify the array (assume the array is read only).
2.  You must use only constant, _O_(1) extra space.
3.  Your runtime complexity should be less than `O(n<sup>2</sup>)`.
4.  There is only one duplicate number in the array, but it could be repeated more than once.



#### Solution
因为全是正数，所以可以用负数来标记。
```
public class Solution {
    public int findDuplicate(int[] nums) {
        int i=0,index=0,r=-1;
        for(i=0;i<nums.length;i++){
            index = Math.abs(nums[i])-1;
            if(nums[index]<0){
                r= index+1;break;
            }
            
            nums[index] = -nums[index];
        }
        // 还原
        for(i=0;i<nums.length;i++){
            nums[i]=Math.abs(nums[i]);
        }
        return r;
    }
}
```