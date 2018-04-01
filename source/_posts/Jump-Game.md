title: Jump Game
author: Halfopen
tags:
  - leetcode
  - medium
categories:
  - 刷题
date: 2018-04-01 11:03:00
---
### [55\. Jump Game](https://leetcode.com/problems/jump-game/description/)

Difficulty: **Medium**



Given an array of non-negative integers, you are initially positioned at the first index of the array.

Each element in the array represents your maximum jump length at that position.

Determine if you are able to reach the last index.

For example:  
A = `[2,3,1,1,4]`, return `true`.

A = `[3,2,1,0,4]`, return `false`.



#### Solution
使用有向图遍历，超时
```
class Solution {
    public boolean canJump(int[] nums) {
        if(null == nums)return false;
        int len = nums.length;
        if(len==0)return false;
        if(len==1)return true;
        
        List<List<Integer>> graph = new ArrayList<>(len);
        
        // 初始化有向图        
        for(int i=0;i<len-1;i++){
            List<Integer> list = new ArrayList<>();
            graph.add(list);
            int n = nums[i];
            for(int j=1;j<=n&&j<=len-1;j++){
                list.add(i+j);
            }
        }
        
        int[] visited = new int[len];
        LinkedList<Integer> q = new LinkedList<>();
        
        q.add(0);
        while(!q.isEmpty()){
            int pos = q.getFirst();
            q.removeFirst();
            if(visited[pos]==1)continue;
            List<Integer> list = graph.get(pos);
            //System.out.println(list);
            System.out.println(pos);
            for(int n:list){
                //System.out.print(" "+n);
                if(n==len-1)return true;
                q.addLast(n);
            }
            
            visited[pos]=1;
            
        }
        return false;
    }
}
```
直接拓展右边界
```java
class Solution {
    public boolean canJump(int[] nums) {
        if(null == nums)return false;
        int len = nums.length;
        if(len==0)return false;
        if(len==1)return true;
        
        int maxR = 0;    
        for(int i=0;i<len-1;i++){
            
            if(i<=maxR){
                int r = i+nums[i];
                if(maxR<r)maxR = r;
                if(maxR>=len-1)return true;
            }else{
                return false;
            }
        }
        
        
        return false;
    }
}
```