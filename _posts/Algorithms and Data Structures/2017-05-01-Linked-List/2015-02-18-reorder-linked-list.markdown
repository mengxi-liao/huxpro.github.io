---
layout:     post
title:      "Problem: Reorder List"
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

Given a singly linked list L: `L0→L1→…→Ln-1→Ln`,
reorder it to: `L0→Ln→L1→Ln-1→L2→Ln-2→…`

You must do this in-place without altering the nodes' values.

For example,
Given `{1,2,3,4}`, reorder it to `{1,4,2,3}`.

## Solution
TODO

#### Code
```java
class Solution {
    public void reorderList(ListNode head) {
        if(head == null || head.next == null) return;
        
        ListNode slow = head;
        ListNode fast = head;
        
        while(fast.next != null && fast.next.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }
        
        ListNode h2 = slow.next;
        slow.next = null;
        
        ListNode newHead = null;
        while(h2 != null) {
            ListNode tmp = h2;
            h2 = h2.next;
            tmp.next = newHead;
            newHead = tmp;
        }
        
        ListNode cur = new ListNode(0);
        ListNode n1 = head;
        ListNode n2 = newHead;
        while(n1 != null && n2 != null) {
            cur.next = n1;
            n1 = n1.next;
            cur.next.next = n2;
            n2 = n2.next;
            cur = cur.next.next;
        }
        
        if(n1!=null)
            cur.next = n1;
    }
}
```

## Performance
TODO