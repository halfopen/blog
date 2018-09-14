title: Combinations
author: Halfopen
tags:
  - leetcode
  - medium
  - dfs
categories:
  - 刷题
date: 2018-09-12 22:06:00
---
### [77\. Combinations](https://leetcode.com/problems/combinations/description/)

Difficulty: **Medium**



Given two integers _n_ and _k_, return all possible combinations of _k_ numbers out of 1 ... _n_.

**Example:**

```
**Input:** n = 4, k = 2
**Output:**
[
  [2,4],
  [3,4],
  [2,3],
  [1,2],
  [1,3],
  [1,4],
]
```



#### Solution

Language: **Java**

```java
class Solution {
    public List<List<Integer>> combine(int n, int k) {
        List<List<Integer>> result = new LinkedList<>();
        
        dfs(n, k, 1, new LinkedList<Integer>(), result);
        return result;
    }
    
    public void dfs(int n, int k, int pos, LinkedList<Integer>path, List<List<Integer>>result){
        if(path.size() == k){
            result.add(new LinkedList<Integer>(path));
            return;
        }
        
        for(int i=pos;i<=n;i++){
            path.addLast(i);
            dfs(n, k, i+1, path, result);
            path.removeLast();
        }
    }
}
```