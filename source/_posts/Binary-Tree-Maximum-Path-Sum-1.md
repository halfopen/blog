title: Binary Tree Maximum Path Sum
author: Halfopen
tags:
  - hard
  - dfs
  - leetcode
categories:
  - 刷题
date: 2018-10-08 19:53:00
---
### [124\. Binary Tree Maximum Path Sum](https://leetcode.com/problems/binary-tree-maximum-path-sum/description/)

Difficulty: **Hard**



Given a **non-empty** binary tree, find the maximum path sum.

For this problem, a path is defined as any sequence of nodes from some starting node to any node in the tree along the parent-child connections. The path must contain **at least one node** and does not need to go through the root.

**Example 1:**

```
**Input:** [1,2,3]

       **1**
      **/ \**
     **2**   **3**

**Output:** 6
```

**Example 2:**

```
**Input:** [-10,9,20,null,null,15,7]

   -10
   / \
  9  **20**
    **/  \**
   **15   7**

**Output:** 42
```



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
    int maxValue;
    
    public int maxPathSum(TreeNode root) {
        maxValue = Integer.MIN_VALUE;
        dfs(root);
        return maxValue;
    }
    
    private int dfs(TreeNode node) {
        if (node == null) return 0;
        int left = Math.max(0, dfs(node.left));
        int right = Math.max(0, dfs(node.right));
        maxValue = Math.max(maxValue, left + right + node.val);
        // System.out.println(maxValue);
        return Math.max(left, right) + node.val;  // 返回的时候，只返回左右中较大的一个
    }
}
```