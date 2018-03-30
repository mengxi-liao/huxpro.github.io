---
layout:     post
title:      "Problem: Swap Nodes in Pairs"
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

Given a linked list, swap every two adjacent nodes and return its head.

For example,
Given `1->2->3->4`, you should return the list as `2->1->4->3`.

Your algorithm should use only constant space. You may **not** modify the values in the list, only nodes itself can be changed.

## Recursive Solution
TODO

#### Code
```java
class Solution {
    public ListNode swapPairs(ListNode head) {
        if(head == null || head.next == null) return head;
        ListNode n = head.next;
        head.next = head.next.next;
        n.next = head;
        
        head.next = swapPairs(head.next);
        return n;
    }
}
```

#### Performance
TODO

## Iterative Solution
TODO

#### Code
```java
class Solution {
    public ListNode swapPairs(ListNode head) {
        if(head == null || head.next == null) return head;
        
        // again, head can change, so use dummy node
        ListNode dummyHead = new ListNode(0);
        dummyHead.next = head;
        
        ListNode prev = dummyHead;
        ListNode n1 = prev.next;
        ListNode n2 = prev.next.next;
        
        while(n1 != null && n2 != null) {
            n1.next = n2.next;
            n2.next = n1;
            prev.next = n2;
            prev = n1;
            n1 = prev != null ? prev.next : null;
            n2 = n1 != null ? n1.next : null;
        }
        
        return dummyHead.next;
    }
}
```

#### Performance
TODO