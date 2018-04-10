title: Remove Duplicates from Sorted List II
author: Halfopen
tags:
  - leetcode
  - medium
categories:
  - 刷题
date: 2018-04-10 21:32:00
---
### [82\. Remove Duplicates from Sorted List II](https://leetcode.com/problems/remove-duplicates-from-sorted-list-ii/description/)

Difficulty: **Medium**



Given a sorted linked list, delete all nodes that have duplicate numbers, leaving only _distinct_ numbers from the original list.

For example,  
Given `1->2->3->3->4->4->5`, return `1->2->5`.  
Given `1->1->1->2->3`, return `2->3`.



#### Solution
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
    public ListNode deleteDuplicates(ListNode head) {
        ListNode nHead = new ListNode(Integer.MAX_VALUE);
        
        ListNode newList = nHead;
        boolean repeat = false;
        for(ListNode cur = head; cur!=null; cur = cur.next){
        	// 遍历重复的
            for(;cur.next!=null && cur.val==cur.next.val;){
                cur = cur.next;
                repeat = true;
            }
            // 跳过重复的最后一个
            if(repeat){
                repeat = false;
                continue;
            }else{
                newList.next = cur;
                newList = cur;
            }
        }
        newList.next = null;
        return nHead.next;
    }
}
```