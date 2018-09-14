title: Subsets II
author: Halfopen
tags:
  - leetcode
  - medium
  - dfs
categories:
  - 刷题
date: 2018-09-12 22:07:00
---
### [90\. Subsets II](https://leetcode.com/problems/subsets-ii/description/)

Difficulty: **Medium**



Given a collection of integers that might contain duplicates, **_nums_**, return all possible subsets (the power set).

**Note:** The solution set must not contain duplicate subsets.

**Example:**

```
**Input:** [1,2,2]
**Output:**
[
  [2],
  [1],
  [1,2,2],
  [2,2],
  [1,2],
  []
]
```



#### Solution

Language: **Java**

```java
class Solution {
    public List<List<Integer>> subsetsWithDup(int[] nums) {
        List<List<Integer>> result = new LinkedList<>();
        if(nums.length==0)return result;
        
        Arrays.sort(nums);
        
        dfs(nums, 0, new LinkedList<Integer>(), result);
        
        return result;
    }
    
    
    
    public void dfs(int[] nums, int index, LinkedList<Integer>path, List<List<Integer>> result){
        result.add(new LinkedList<Integer>(path));
        
        for(int i=index;i<nums.length;++i){
            if(i>index&& nums[i]==nums[i-1])continue;
            path.addLast(nums[i]);
            dfs(nums, i+1, path, result);
            path.removeLast();
        }
    }
}
```