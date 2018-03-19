title: Palindrome Linked List
author: Halfopen
tags:
  - leetcode
  - easy
categories:
  - 刷题
date: 2018-03-18 22:09:00
---
### [234\. Palindrome Linked List](https://leetcode.com/problems/palindrome-linked-list/description/)

Difficulty: **Easy**



Given a singly linked list, determine if it is a palindrome.

**Follow up:**  
Could you do it in O(n) time and O(1) space?



#### Solution
在O(n)的时间, O(1)的空间内，判断一个链表是不是回文链表。

思路1： 用快慢指针找到中间节点，然后把后面一半反转，进行对比，然后再还原。
```
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public boolean isPalindrome(ListNode head) {
        
    }
}
```