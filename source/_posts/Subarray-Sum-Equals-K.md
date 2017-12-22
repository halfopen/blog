title: Subarray Sum Equals K
author: Halfopen
tags:
  - medium
  - leetcode
categories:
  - 刷题
date: 2017-12-22 13:41:00
---
### [560\. Subarray Sum Equals K](https://leetcode.com/problems/subarray-sum-equals-k/description/)

Difficulty: **Medium**

Given an array of integers and an integer **k**, you need to find the total number of continuous subarrays whose sum equals to **k**.

**Example 1:**  

```
**Input:**nums = [1,1,1], k = 2
**Output:** 2
```

**Note:**  

1.  The length of the array is in range [1, 20,000].
2.  The range of numbers in the array is [-1000, 1000] and the range of the integer **k** is [-1e7, 1e7].

#### Solution
如果数组是排好序的话，直接从左到右遍历就可以了，一开始以为是这样，写出来的代码如下
```java
class Solution {
    public int subarraySum(int[] nums, int k) {
        int result=0, sum=0,i=0,j=0;
        Arrays.sort(nums);
        sum = nums[i];
        while(i<nums.length){
            if(sum==k){
                result++;
            }
            
            if(sum<=k && j<nums.length-1){
                j++;
                sum+=nums[j];
            }else{
                i++;
                sum-=nums[i-1];
            }
        }
        return result;
    }
}
```
然后系统给出了反例

    Input:
        [1,2,1,2,1]
        3
    Output:
        2
    Expected:
        4
        
如果是无序的话，连续数组nums[i,j]有n^2种可能，如果用穷举可能会超时

如果按连续最大和的解法，每次比较num[i]和sum的话，只要sum小于k,我们就能保证sum一直递增，会慢慢向k接近，也许是个思路

如果sum小于k,保持sum递增

如果sum大于k,加了num[i]之后比k大，暂时没想到怎么做

----
O(n)解法，类似动态规划,用map保存连续和为k的可能数 sum一直累加，sum-k表示
```java
public class Solution {
    public int subarraySum(int[] nums, int k) {
        int sum = 0, result = 0;
        Map<Integer, Integer> preSum = new HashMap<>();
        preSum.put(0, 1); // k may be zero
        
        for (int i = 0; i < nums.length; i++) {
            sum += nums[i];
            // 当前和可以分解和相加和为 sum-k和和为k和两个子序列,而这种可能性的大小，取决于和为sum-k的个数 

            result += preSum.getOrDefault(sum - k,0);  
            preSum.put(sum, preSum.getOrDefault(sum, 0) + 1);
        }
        
        return result;
    }
}
```