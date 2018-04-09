---
layout:     post
title:      "Problem: Linked List Cycle"
date:       2015-02-18 00:00:00
author:     "Marcy"
header-img: "img/post-bg-2015.jpg"
catalog: true
category: algnote
algnote-tags:
    - Coding Interview
    - Coding Practice
    - Algorithms and Data Structures
    - Linked List
    - Medium
---

## Question

Given a linked list, determine if it has a cycle in it.

**Follow up:**
Can you solve it without using extra space?

## Solution
TODO

#### Code
```java
public class Solution {
    public boolean hasCycle(ListNode head) {
        if(head == null) return false;
        
        ListNode t1 = head;
        ListNode t2 = head;
        while(t2==null || t2==null || t2.next == null) {
            t1 = t1.next;
            t2 = t2.next.next;
            if(t1==t2) return true;
        }
    }
}
```

## Performance
TODO
