title: Reverse Pairs
author: Halfopen
date: 2018-09-20 10:24:25
tags:
---
### [493\. Reverse Pairs](https://leetcode.com/problems/reverse-pairs/description/)

Difficulty: **Hard**



Given an array `nums`, we call `(i, j)` an **_important reverse pair_** if `i < j` and `nums[i] > 2*nums[j]`.

You need to return the number of important reverse pairs in the given array.

**Example1:**

```
**Input**: [1,3,2,3,1]
**Output**: 2
```

**Example2:**

```
**Input**: [2,4,3,5,1]
**Output**: 3
```

**Note:**  

1.  The length of the given array will not exceed `50,000`.
2.  All the numbers in the input array are in the range of 32-bit integer.



#### Solution
同样使用bit,不过累加的时候，把累加的sum加到nums[i]*2的位置
Language: **Java**

```java
class Solution {
    public int[] bits;
    public int reversePairs(int[] nums) {
        int ret = 0;
        long[] sortednums = new long[nums.length*2];
        long[] longnums = new long[nums.length];
        for(int i=0;i<nums.length;i++){
            longnums[i] = nums[i];
            sortednums[i*2] = longnums[i];
            sortednums[i*2+1] = longnums[i]*2;
        }
        bits = new int[sortednums.length+1];
        Arrays.sort(sortednums);
        HashMap<Long, Integer> map = new HashMap<>();
        for(int i=0;i<sortednums.length;++i){
            //System.out.println(sortednums[i]);
            map.put(sortednums[i], i+1);
        }
        for(int i=longnums.length-1;i>=0;--i){
            int sum = preSum(map.get(longnums[i])-1);
            ret+= sum;
            //System.out.println(longnums[i]*2);
            add(map.get(longnums[i]*2), 1);
        }
        return ret;
    }
    public void add(int i, int val){
        for(int j=i;j<bits.length;j+=j&(-j)){
            bits[j]+=val;
        }
    }
    public int preSum(int i){
        int ret=0;
        for(int j=i;j>0;j-=j&(-j)){
            ret+=bits[j];
        }
        return ret;
    }
}
```