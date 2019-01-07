title: Symmetric Tree
author: Halfopen
tags:
  - easy
  - dfs
  - leetcode
categories:
  - 刷题
date: 2018-10-08 20:10:00
---
### [101\. Symmetric Tree](https://leetcode.com/problems/symmetric-tree/description/)

Difficulty: **Easy**



Given a binary tree, check whether it is a mirror of itself (ie, symmetric around its center).

For example, this binary tree `[1,2,2,3,4,4,3]` is symmetric:

```
    1
   / \
  2   2
 / \ / \
3  4 4  3
```

But the following `[1,2,2,null,3,null,3]` is not:  

```
    1
   / \
  2   2
   \   \
   3    3
```

**Note:**  
Bonus points if you could solve it both recursively and iteratively.



#### Solution

Language: **Java**

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public boolean isSymmetric(TreeNode root) {
        if(null==root)return true;
        return dfs(root.left, root.right);
    }
    
    public boolean dfs(TreeNode node1, TreeNode node2){
        if(null==node1 && null==node2)return true;
        if(node1==null || null==node2)return false; // 比较的是节点的内容
        
        // node1==node2 & not null
        return node1.val==node2.val && dfs(node1.left, node2.right) && dfs(node1.right, node2.left); //两个都要满足
    }
}
```