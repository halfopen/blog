title: Validate Binary Search Tree
author: Halfopen
tags:
  - leetcode
  - medium
  - 树
categories:
  - 刷题
date: 2018-01-02 19:34:00
---
### [98\. Validate Binary Search Tree](https://leetcode.com/problems/validate-binary-search-tree/description/)

判断一个树是不是有效的二叉搜索树

Difficulty: **Medium**

Given a binary tree, determine if it is a valid binary search tree (BST).

Assume a BST is defined as follows:

*   The left subtree of a node contains only nodes with keys **less than** the node's key.
*   The right subtree of a node contains only nodes with keys **greater than** the node's key.
*   Both the left and right subtrees must also be binary search trees.

**Example 1:**  

```
    2
   / \
  1   3
```

Binary tree `[2,1,3]`, return true.

**Example 2:**  

```
    1
   / \
  2   3
```

Binary tree `[1,2,3]`, return false.

#### Solution
```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public long MAX = 2147483648L;
    public long MIN = -2147483649L;
    public boolean isValidBST(TreeNode root) {
        if(root==null)return true;
      	// 左右子树空间不同
        return dfs(MIN, root.val, root.left) && dfs(root.val, MAX, root.right);
    }
    
    public boolean dfs(long min, long max, TreeNode node){
        //System.out.println(min+":"+max);
        if(null==node)return true;
        if(node.val>=max || node.val<=min)return false;
        
        return dfs(min, node.val, node.left) && dfs(node.val, max, node.right); 
    }
}
```