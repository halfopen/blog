title: Remove Nth Node From End of List
author: Halfopen
tags:
  - medium
  - leetcode
categories:
  - 刷题
date: 2017-12-22 13:40:00
---
### [19\. Remove Nth Node From End of List](https://leetcode.com/problems/remove-nth-node-from-end-of-list/description/)

Difficulty: **Medium**

Given a linked list, remove the _n_<sup>th</sup> node from the end of list and return its head.

For example,

```
   Given linked list: **1->2->3->4->5**, and **_n_ = 2**.

   After removing the second node from the end, the linked list becomes **1->2->3->5**.
```

在一次遍历中，完成把单向链表的倒数第n个去除

**Note:**  
Given _n_ will always be valid.  
Try to do this in one pass.

#### Solution
一对快慢指针，快指针先走n个节点，然后两个指针同时走，直到快指针走到尾部，这时候慢指针还有n个没走，即在倒数第n的位置。
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
    public ListNode removeNthFromEnd(ListNode head, int n) {
        ListNode start = new ListNode(0);
        start.next = head;
        ListNode fast = start, slow = start;
        
        for(int i=0;i<=n;i++){ //多了一个fast走到null
            fast = fast.next;
        }
        
        while(fast!=null){
            slow = slow.next;
            fast = fast.next;
        }
        
        slow.next = slow.next.next;
        return start.next;
    }
}
```