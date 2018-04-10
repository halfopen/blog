title: Partition List
author: Halfopen
tags:
  - leetcode
  - medium
categories:
  - 刷题
date: 2018-04-10 20:17:00
---
### [86\. Partition List](https://leetcode.com/problems/partition-list/description/)

Difficulty: **Medium**



Given a linked list and a value _x_, partition it such that all nodes less than _x_ come before nodes greater than or equal to _x_.

You should preserve the original relative order of the nodes in each of the two partitions.

For example,  
Given `1->4->3->2->5->2` and _x_ = 3,  
return `1->2->2->4->3->5`.



#### Solution

用两个链表分别存储，最后合并

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
    public ListNode partition(ListNode head, int x) {
        ListNode l = new ListNode(0);
        ListNode s = new ListNode(0);
        
        // 记住开始位置
        ListNode large = l;
        ListNode small = s;
        
        for(ListNode cur = head; cur!=null;cur = cur.next){
            if(cur.val >=x){
                large.next = cur;
                large = cur;
                //System.out.println("large"+cur.val);
            }else{
                small.next = cur;
                small = cur;
                //System.out.println("small"+cur.val);
            }
        }
        large.next = null; // 不加这句话，next是随机初始化的
        // 合并大小链表
        small.next = l.next;
        return s.next;
    }
}}
}
```