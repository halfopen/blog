title: Subsets
author: Halfopen
tags:
  - leetcode
  - medium
categories:
  - 刷题
date: 2018-03-22 22:01:00
---
### [78\. Subsets](https://leetcode.com/problems/subsets/description/)

Difficulty: **Medium**



Given a set of **distinct** integers, _nums_, return all possible subsets (the power set).

**Note:** The solution set must not contain duplicate subsets.

For example,  
If **_nums_** = `[1,2,3]`, a solution is:

```
[
  [3],
  [1],
  [2],
  [1,2,3],
  [1,3],
  [2,3],
  [1,2],
  []
]
```

求一个集合的所有子集

错误：
1. 忘记返回值
2. 递归忘记返回
3. List是引用传参，改为string

#### Solution
```java
class Solution {
    public List<List<Integer>> subsets(int[] nums) {
        List<List<Integer>> res = new ArrayList<>();
        
        if(null==nums || nums.length==0)return res;
        String temp="0";
        helper(res, nums, temp, 0);
        return res;
    }
    
    public void helper(List<List<Integer>> list, int[] nums, String temp, int cur){
        if(cur >= nums.length){
            // add temp to list
            List<Integer> li = new ArrayList<>();
            String[] tempNums = temp.split(",");
            for(int i=1;i<tempNums.length;i++){
                li.add(Integer.parseInt(tempNums[i]));
            }
            list.add(li);
            return;
        }
                       
        // don't add nums[cur]
        helper(list, nums, temp, cur+1);
        // add nums[cur]
        helper(list, nums, temp+","+nums[cur], cur+1);
    }
}
```
使用List
```java
class Solution {
    public List<List<Integer>> subsets(int[] nums) {
        List<List<Integer>> res = new ArrayList<>();
        
        if(null==nums || nums.length==0)return res;
        List<Integer> temp=new ArrayList<>();
        helper(res, nums, temp, 0);
        return res;
    }
    
    public void helper(List<List<Integer>> list, int[] nums, List<Integer> temp, int cur){
        if(cur >= nums.length){
            // add temp to list
            list.add(new ArrayList<>(temp));
            return;
        }
                       
        // don't add nums[cur]
        helper(list, nums, temp, cur+1);
        // add nums[cur]
        temp.add(nums[cur]);
        helper(list, nums, temp, cur+1);
        temp.remove(temp.indexOf(nums[cur]));
    }
}
```