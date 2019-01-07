title: Intersection of Two Linked Lists
author: Halfopen
tags:
  - easy
  - leetcode
categories:
  - 刷题
date: 2018-10-08 19:19:00
---
### [160\. Intersection of Two Linked Lists](https://leetcode.com/problems/intersection-of-two-linked-lists/description/)

Difficulty: **Easy**



Write a program to find the node at which the intersection of two singly linked lists begins.

For example, the following two linked lists:

```
A:          a1 → a2
                   ↘
                     c1 → c2 → c3
                   ↗            
B:     b1 → b2 → b3
```

begin to intersect at node c1.

**Notes:**

*   If the two linked lists have no intersection at all, return `null`.
*   The linked lists must retain their original structure after the function returns.
*   You may assume there are no cycles anywhere in the entire linked structure.
*   Your code should preferably run in O(n) time and use only O(1) memory.



#### Solution

两个链表的交集，普通做法是先求长度 https://leetcode.com/problems/intersection-of-two-linked-lists/discuss/49792/Concise-JAVA-solution-O(1)-memory-O(n)-time ，如果两个链表交换走两遍，长度就是一样的了，并且第二圈的时候，后半段就一样了

Language: **Java**

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        
        ListNode pa = headA;
        ListNode pb = headB;
        
        while(pa!=pb){
            
            pa = pa == null?headB: pa.next;
            pb = pb == null? headA: pb.next;
        }
        
        return pa;
    }
}
```