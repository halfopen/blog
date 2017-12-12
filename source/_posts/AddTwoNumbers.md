title: Add Two Numbers
tags:
  - leetcode
  - medium
categories:
  - 刷题
date: 2017-11-20 18:23:00
---
## 题目描述：

You are given two linked lists representing two non-negative numbers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 0 -> 8

## 题目大意：
给定两个链表分别代表两个非负整数。数位以倒序存储，并且每一个节点包含一位数字。将两个数字相加并以链表形式返回。

## 解题思路：
保存进位标志，只要有链表不为空或者有进位标志就一直继续相加

## 代码：
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
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        ListNode prev = new ListNode(0);
        ListNode head = prev;
        int carry = 0;
        
        while(l1!=null || l2!=null || carry!=0){
            ListNode node = new ListNode(0);
            int sum = (l1==null?0:l1.val) + (l2==null?0:l2.val)+carry;
            carry = sum/10;
            sum = sum%10;
            
            node.val = sum;
            
            prev.next = node;
            prev = prev.next;
            l1 = l1==null?null:l1.next;
            l2 = l2==null?null:l2.next;
        }
        return head.next;
    }
}
```