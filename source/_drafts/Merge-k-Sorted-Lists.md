title: Merge k Sorted Lists
author: Halfopen
tags:
  - hard
  - leetcode
categories:
  - 刷题
date: 2018-10-08 18:54:00
---
### [23\. Merge k Sorted Lists](https://leetcode.com/problems/merge-k-sorted-lists/description/)

Difficulty: **Hard**



Merge _k_ sorted linked lists and return it as one sorted list. Analyze and describe its complexity.

**Example:**

```
**Input:**
[
  1->4->5,
  1->3->4,
  2->6
]
**Output:** 1->1->2->3->4->4->5->6
```

不用优先队列的话，时间复杂度会变成O(n^2)


#### Solution

Language: **Java**

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode mergeKLists(ListNode[] lists) {
        if (lists==null||lists.length==0) return null;
        PriorityQueue<ListNode> queue= new PriorityQueue<ListNode>(lists.length ,(a,b) -> a.val-b.val);
        ListNode dummy = new ListNode(0);
        ListNode tail=dummy;
        
        for (ListNode node:lists)
            if (node!=null)
                queue.add(node);
            
        while (!queue.isEmpty()){
            tail.next=queue.poll();
            tail=tail.next;
            
            if (tail.next!=null)
                queue.add(tail.next);
        }
        return dummy.next;
    }
}
```