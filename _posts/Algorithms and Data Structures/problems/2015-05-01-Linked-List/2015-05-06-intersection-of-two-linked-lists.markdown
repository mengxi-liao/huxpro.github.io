---
layout:     post
title:      "Problem: Intersection of Two Linked Lists"
date:       2015-02-18 00:00:00
author:     "Marcy"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - Coding Interview
    - Coding Practice
    - Algorithms and Data Structures
    - Linked List
    - Medium
---

## Question

Write a program to find the node at which the intersection of two singly linked lists begins.


For example, the following two linked lists:

```
A:          a1 → a2
                   ↘
                     c1 → c2 → c3
                   ↗            
B:     b1 → b2 → b3
```

begin to intersect at node c1.

**Notes:**

- If the two linked lists have no intersection at all, return null.
- The linked lists must retain their original structure after the function returns.
- You may assume there are no cycles anywhere in the entire linked structure.
- Your code should preferably run in O(n) time and use only O(1) memory.

## Solution
TODO

#### Code
```java
public class Solution {
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        ListNode tA = headA;
        ListNode tB = headB;
        int lA = 0;
        int lB = 0;
        while(tA != null) {
            tA = tA.next;
            lA++;
        }
        while(tB != null) {
            tB = tB.next;
            lB++;
        }
        
        int diff = Math.abs(lA - lB);
        ListNode nS = headA;
        ListNode nL = headB;
        if(lA > lB) {
            nS = headB;
            nL = headA;
        }
        
        while(diff > 0) {
            nL = nL.next;
            diff --;
        }
        
        while(nS != nL) {
            nS = nS.next;
            nL = nL.next;
        }
        
        return nS;
    }
}
```

## Performance
TODO
