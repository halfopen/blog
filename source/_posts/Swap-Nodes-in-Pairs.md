title: Swap Nodes in Pairs
author: Halfopen
tags:
  - leetcode
  - medium
categories:
  - 刷题
date: 2017-12-22 13:41:00
---
### [24\. Swap Nodes in Pairs](https://leetcode.com/problems/swap-nodes-in-pairs/description/)

Difficulty: **Medium**

Given a linked list, swap every two adjacent nodes and return its head.

For example,  
Given `1->2->3->4`, you should return the list as `2->1->4->3`.

Your algorithm should use only constant space. You may **not** modify the values in the list, only nodes itself can be changed.

把链表对的结点成对替换，不能修改结点的value

#### Solution
```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode swapPairs(ListNode head) {
        if(head==null)return null;
        
        ListNode start = new ListNode(0);
        start.next = head;
        ListNode t1 = start, t2 = start.next; // t1是前一个，选择替换t2和t2.next
        
        while(t2!=null && t2.next!=null){
            // 只要t2不为空，就可以替换
            t1.next = t2.next;
            t2.next = t2.next.next;
            t1.next.next = t2;
            
            // update t1 t2
            t1 = t2;
            t2 = t2.next;
        }
        return start.next;
    }
}
```
