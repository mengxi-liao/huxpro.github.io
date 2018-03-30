---
layout:     post
title:      "Problem: Remove Nth Node from the End of List"
date:       2015-02-18 00:00:00
author:     "Marcy"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - Coding Interview
    - Coding Practice
    - Algorithms and Data Structures
    - Linked List
---

## Question

Given a linked list, remove the nth node from the end of list and return its head.

For example,
```
   Given linked list: 1->2->3->4->5, and n = 2.

   After removing the second node from the end, the linked list becomes 1->2->3->5.
```
**Note:**
Given n will always be valid.
Try to do this in one pass.

## Solution
TODO

#### Code
```java
class Solution {
    public ListNode removeNthFromEnd(ListNode head, int n) {
        // dummy node is useful when head could be changed,
        // in this case the head could be the node to be deleted.
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        ListNode f = head;
        ListNode s = dummy;
        while(n-->0) {
            f = f.next;
        }
        while(f != null) {
            f = f.next;
            s = s.next;
        }
        
        s.next = s.next.next;
        
        return dummy.next;
    }
}
```

## Performance
TODO