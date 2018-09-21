title: Count of Smaller Numbers After Self
author: Halfopen
tags:
  - leetcode
  - hard
  - bit
categories:
  - 刷题
date: 2018-09-20 09:38:00
---
### [315\. Count of Smaller Numbers After Self](https://leetcode.com/problems/count-of-smaller-numbers-after-self/description/)

Difficulty: **Hard**



You are given an integer array _nums_ and you have to return a new _counts_ array. The _counts_ array has the property where `counts[i]` is the number of smaller elements to the right of `nums[i]`.

**Example:**

```
**Input:** [5,2,6,1]
**Output:** `[2,1,1,0] 
**Explanation:**`
To the right of 5 there are **2** smaller elements (2 and 1).
To the right of 2 there is only **1** smaller element (1).
To the right of 6 there is **1** smaller element (1).
To the right of 1 there is **0** smaller element.
```



#### Solution

Language: **Java**
使用普通bit的方法
```java
class Solution {
​
    public int[] bits;
    
    public List<Integer> countSmaller(int[] nums) {
        LinkedList<Integer> ret = new LinkedList<>();
        int[] sortednums = nums.clone();
        bits = new int[nums.length+1];
        
        Arrays.sort(sortednums);
        HashMap<Integer, Integer> map = new HashMap<>();
        for(int i=0;i<sortednums.length;++i){
            map.put(sortednums[i], i+1);
        }
        
        for(int i=nums.length-1;i>=0;--i){
            int sum = preSum(map.get(nums[i])-1);
            ret.addFirst(sum);
            add(map.get(nums[i]), 1);
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

用空间换时间
```java
class Solution {
    public List<Integer> countSmaller(int[] nums) {
        
        int min = Integer.MAX_VALUE;
        int max = Integer.MIN_VALUE;
        for (int i = 0; i<nums.length; i++){
            min = Math.min(min, nums[i]);
            max = Math.max(max, nums[i]);
        }
        
        for (int i = 0; i<nums.length; i++){
            nums[i] = nums[i] - min + 1;
        }
        max = max - min + 1;
        
        Integer[] res = new Integer[nums.length];
        int[] tree = new int[max+1];
        for (int i = nums.length-1; i>=0; i--){
            res[i] = search(tree, nums[i]-1);
            add(tree, nums[i]);
        }
        return Arrays.asList(res);
    }
    
    public int search(int[] tree, int val){
        int res = 0;
        while (val != 0){
            res += tree[val];
            val -= (val & -val);
        }
        return res;
    }
    
    public void add(int[] tree, int val){
        while(val < tree.length){
            tree[val]++;
            val += (val & -val);
        }
    }
}
```