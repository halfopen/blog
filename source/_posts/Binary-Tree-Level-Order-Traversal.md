title: Binary Tree Level Order Traversal
author: Halfopen
tags:
  - leetcode
  - medium
categories:
  - 刷题
date: 2018-03-22 21:20:00
---
### [102\. Binary Tree Level Order Traversal](https://leetcode.com/problems/binary-tree-level-order-traversal/description/)

Difficulty: **Medium**



Given a binary tree, return the _level order_ traversal of its nodes' values. (ie, from left to right, level by level).

For example:  
Given binary tree `[3,9,20,null,null,15,7]`,  

```
    3
   / \
  9  20
    /  \
   15   7
```

return its level order traversal as:  

```
[
  [3],
  [9,20],
  [15,7]
]
```

错误：
1. 不了解双向队列数据结构
2. 忘记加分号结尾



#### Solution

    只要进行层次遍历即可，但是要记住每一层的最后一个节点。
    当一层遍历完成，也就是添加的节点是最后一个节点时，新一层的最后一个结点就是队列的尾部。

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
    public List<List<Integer>> levelOrder(TreeNode root) {
        
        List<List<Integer>> list = new ArrayList<>();
        // 层次遍历二叉树
        Deque<TreeNode> queue = new ArrayDeque<>();
        // 记录层次尾，出队时，更新为队尾
        
        if(null==root)return list;
        
        TreeNode end = root;
        queue.addLast(root);
        List<Integer> floor = new ArrayList<>();
        while(!queue.isEmpty()){
            // 取出节点
            TreeNode node = queue.pollFirst();
            floor.add(node.val);

            if(null!= node.left){
                queue.addLast(node.left);
            }
            if(null!=node.right){
                queue.addLast(node.right);
            }
            // 一层结束
            if(end == node){
                end = queue.peekLast();
                list.add(floor);
                floor = new ArrayList<>();
            }
            
        }
        return list;
    }
}
```

不用双向队列也能做

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
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> res = new LinkedList<>();
        Queue<TreeNode> queue = new LinkedList<>();
        if(root == null)
            return res;
        queue.offer(root);
        while(!queue.isEmpty()) {
            int levelNum = queue.size();
            List<Integer> list = new LinkedList<>();
            // 遍历一层
            for(int i=0; i<levelNum; i++) {
                TreeNode cur = queue.peek();
                list.add(queue.poll().val);
                if(cur.left != null)
                    queue.offer(cur.left);
                if(cur.right != null)
                    queue.offer(cur.right);    
            }
            // 添加一层
            res.add(list);
        }
        return res;
        
    }
}

```

递归dfs反而是最快的代码

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
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> res = new ArrayList<>();
        if(root == null)
            return res;
        helper(res,root,0);
        return res;
    }
    
    private void helper(List<List<Integer>> res, TreeNode root, int level){
        if(root == null)
            return;
        if(level >= res.size())res.add(new ArrayList<Integer>());
        res.get(level).add(root.val);
        helper(res,root.left,level+1);
        helper(res,root.right,level+1);
    }
}

```