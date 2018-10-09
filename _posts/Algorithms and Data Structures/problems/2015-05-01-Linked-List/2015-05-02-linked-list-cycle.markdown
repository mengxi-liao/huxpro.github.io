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
        ListNode s = head;
        ListNode f = head;
        while(f != null && f.next != null) {
            s = s.next;
            f = f.next.next;
            if(s==f) return true;
        }
        
        return false;
    }
}
```

## Performance
TODO
