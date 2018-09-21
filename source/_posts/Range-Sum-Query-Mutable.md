title: Range Sum Query - Mutable
author: Halfopen
tags:
  - leetcode
  - medium
  - bit
categories:
  - 刷题
date: 2018-09-19 21:35:00
---
### [307\. Range Sum Query - Mutable](https://leetcode.com/problems/range-sum-query-mutable/description/)

Difficulty: **Medium**



Given an integer array _nums_, find the sum of the elements between indices _i_ and _j_ (_i_ ≤ _j_), inclusive.

The _update(i, val)_ function modifies _nums_ by updating the element at index _i_ to _val_.

**Example:**

```
Given nums = [1, 3, 5]

sumRange(0, 2) -> 9
update(1, 2)
sumRange(0, 2) -> 8
```

**Note:**

1.  The array is only modifiable by the _update_ function.
2.  You may assume the number of calls to _update_ and _sumRange_ function is distributed evenly.



#### Solution

一个基本考察BIT的题目 https://blog.csdn.net/Yaokai_AssultMaster/article/details/79492190

https://blog.csdn.net/l664675249/article/details/50157669

Language: **Java**

```java
public class NumArray {
    public int[] nums;
    public int[] arr;
​
    public NumArray(int[] nums) {
        this.nums = nums;
        arr = new int[nums.length+1];
        for(int i=0;i<nums.length;i++){
            add(i+1, nums[i]);
        }
​
    }
    
    public void add(int i, int val){
        for(int j=i;j<arr.length;j += j&(-j)){
            arr[j]+=val;
        }
    }
​
    public void update(int i, int val) {
        add(i+1, val-nums[i]);
        nums[i] = val;
    }
​
    /**
     * 计算 nums[0]+nums[1]...+nums[i]
     * @param i
     * @return
     */
    public int preSum(int i){
        i = i+1;    // 因为要包含nums[i]
        if(i>arr.length||i<=0)return 0;
        int ret = 0;
        // 从后往前推
        for(int j=i;j>0;j-=j&(-j)){
            ret +=arr[j];
        }
        return ret;
    }
​
    /**
     *  计算 nums[i]+nums[i+1]...+nums[j]
     * @param i
     * @param j
     * @return
     */
    public int sumRange(int i, int j) {
        return preSum(j)-preSum(i-1);
    }
}
​
```