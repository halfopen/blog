title: Sort Colors 荷兰国旗问题
author: Halfopen
date: 2018-01-19 21:01:14
tags:
---
### [75\. Sort Colors](https://leetcode.com/problems/sort-colors/description/)

Difficulty: **Medium**



Given an array with _n_ objects colored red, white or blue, sort them so that objects of the same color are adjacent, with the colors in the order red, white and blue.

Here, we will use the integers 0, 1, and 2 to represent the color red, white, and blue respectively.


现有红白蓝三个不同颜色的小球，乱序排列在一起，请重新排列这些小球，使得红白蓝三色的同颜色的球在一起。这个问题之所以叫荷兰国旗问题，是因为我们可以将红白蓝三色小球想象成条状物，有序排列后正好组成荷兰国旗。

**Note:**  
You are not suppose to use the library's sort function for this problem.



**Follow up:**  
A rather straight forward solution is a two-pass algorithm using counting sort.  
First, iterate the array counting number of 0's, 1's, and 2's, then overwrite array with total number of 0's, then 1's and followed by 2's.

Could you come up with an one-pass algorithm using only constant space?  





#### Solution
【思路一】

（1）遍历数组，统计红白蓝三色球（0，1，2）的个数

（2）根据红白蓝三色球（0，1，2）的个数重排数组

时间复杂度：O(n)

【最佳思路】
遍历数组，取出当前元素的值nums[k]，保存在v
[1] nums[k]统一设置为2，因为2肯定是在所有元素的后面。
[2] 如果 v<2,那么v可能是0或者1。 统一设置为1，j++。
[3] 如果v==0,nums[i]设置为0, i++。

这里，k是2的位置，j是1的位置，因为0会在1的前面，所以j遇到0和1都要自增。

```python
class Solution(object):
    def sortColors(self, nums):
        """
        :type nums: List[int]
        :rtype: void Do not return anything, modify nums in-place instead.
        """
        i = j = 0
        for k in xrange(len(nums)):
            v = nums[k]
            nums[k] = 2
            if v < 2:
                nums[j] = 1
                j += 1
            if v == 0:
                nums[i] = 0
                i += 1
```
http://blog.csdn.net/sunnyyoona/article/details/43488481