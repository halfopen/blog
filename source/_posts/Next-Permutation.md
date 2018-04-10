title: Next Permutation
author: Halfopen
tags:
  - leetcode
  - medium
  - 字典序
categories:
  - 刷题
date: 2017-12-22 13:41:00
---
### [31\. Next Permutation](https://leetcode.com/problems/next-permutation/description/)

Difficulty: **Medium**

Implement next permutation, which rearranges numbers into the lexicographically next greater permutation of numbers.

If such arrangement is not possible, it must rearrange it as the lowest possible order (ie, sorted in ascending order).

The replacement must be in-place, do not allocate extra memory.

Here are some examples. Inputs are in the left-hand column and its corresponding outputs are in the right-hand column.  
`1,2,3` → `1,3,2`  
`3,2,1` → `1,2,3`  
`1,1,5` → `1,5,1`

求下一个字典序

#### Solution

只要有顺序的，就有下一个比它大的字典序
因此第一步找出最后一个顺序的位置j，然后找到它后面，最后一个比它大的位置k
// 如果从后开始找，j是第一个降序的位置，k是第一个比它大的位置。
交换 j k
再把j+1到最后逆序。

```java
class Solution {
    public void nextPermutation(int[] nums) {
        if(nums.length<2)return;
        int j=-1,k=nums.length-1,temp;
        // find the max increase
        for(int i=0;i<nums.length-1;++i){
            if(nums[i]<nums[i+1]){
                j = i;
            }
        }
        // if nums is all reversed
        if(j==-1){
            Arrays.sort(nums);
        }else{
            // find the largest k with num[k] > nums[j]
            for(int i=j+1;i<nums.length;++i){
                if(nums[i]>nums[j]){
                    k=i;
                }
            }
            
            // swap j,k
            temp = nums[j];
            nums[j] = nums[k];
            nums[k] = temp;
            
            // revease nums[j+1 ~ end]
            
            int left = j+1,right=nums.length-1;
            while(left<right){
                temp=nums[left];
                nums[left] = nums[right];
                nums[right] = temp;
                left++;
                right--;
            }
        }
    }
}
```

```java
class Solution {
    public void nextPermutation(int[] nums) {
        if(nums.length<2)return;
        int j = -1, k=0;
        // 1.从后面开始，找到第一个 nums[j]<nums[j+1]
        for(int i=nums.length-2; i>=0;i--){
            if(nums[i]<nums[i+1]){
                j = i;
                break;
            }
        }
        // 2.如果逆序，直接跳到最后一步
        if(j>=0){
            // 3.从后面开始，找到第一个比 nums[j]大的nums[k]
            for(int i=nums.length-1;i>=0;i--){
                if(nums[i]>nums[j]){
                    k = i;
                    break;
                }
            }
            // 4.交换 nums[j], nums[k]
            int temp;
            temp= nums[j];
            nums[j] = nums[k];
            nums[k] = temp;
        }
        // 5.把nums[j]之后全部逆序
        int left = j+1, right = nums.length-1;
        while(left<right){
            int temp;
            temp = nums[left];
            nums[left] = nums[right];
            nums[right] = temp;
            left++;
            right--;
        }
    }
}
```

https://www.cnblogs.com/lucio_yz/p/5219844.html