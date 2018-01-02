title: Copy List with Random Pointer
author: Halfopen
tags:
  - leetcode
  - medium
categories:
  - 刷题
date: 2018-01-02 21:33:00
---
### [138\. Copy List with Random Pointer](https://leetcode.com/problems/copy-list-with-random-pointer/description/)

Difficulty: **Medium**

A linked list is given such that each node contains an additional random pointer which could point to any node in the list or null.

Return a deep copy of the list.

#### Solution

用两个指针记录新旧链表，然后遍历到random,把新链表的random指过去

每次为了得到新random,都要进行遍历，因此时间复杂度是O(n^2)

但是这样显然时间复杂度太高

下面有一种O(1)额外空间，O(n)时间的做法，

![upload successful](/assets/images/Copy List with Random Pointer/pasted-0.png)

如图所示，在原链表节点之间，插入新链表对应的元素

这样，原链表 node.next就是对应新链表的元素，  random对应的新元素就是random.next

然后把链表还原。

```java
public RandomListNode copyRandomList(RandomListNode head) {
	RandomListNode iter = head, next;

	// First round: make copy of each node,
	// and link them together side-by-side in a single list.
	while (iter != null) {
		next = iter.next;

		RandomListNode copy = new RandomListNode(iter.label);
		iter.next = copy;
		copy.next = next;

		iter = next;
	}

	// Second round: assign random pointers for the copy nodes.
	iter = head;
	while (iter != null) {
		if (iter.random != null) {
			iter.next.random = iter.random.next;
		}
		iter = iter.next.next;
	}

	// Third round: restore the original list, and extract the copy list.
	iter = head;
	RandomListNode pseudoHead = new RandomListNode(0);
	RandomListNode copy, copyIter = pseudoHead;

	while (iter != null) {
		next = iter.next.next;

		// extract the copy
		copy = iter.next;
		copyIter.next = copy;
		copyIter = copy;

		// restore the original list
		iter.next = next;

		iter = next;
	}

	return pseudoHead.next;
}
```

还有直接用HashMap保存新节点的方法

```java
public RandomListNode copyRandomList(RandomListNode head) {
  if (head == null) return null;
  
  Map<RandomListNode, RandomListNode> map = new HashMap<RandomListNode, RandomListNode>();
  
  // loop 1. copy all the nodes
  RandomListNode node = head;
  while (node != null) {
    map.put(node, new RandomListNode(node.label));
    node = node.next;
  }
  
  // loop 2. assign next and random pointers
  node = head;
  while (node != null) {
    map.get(node).next = map.get(node.next);
    map.get(node).random = map.get(node.random);
    node = node.next;
  }
  
  return map.get(head);
}
```