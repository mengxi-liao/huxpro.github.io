---
layout:     post
title:      "Problem: Merge Two Sorted Lists"
date:       2015-02-18 00:00:00
author:     "Marcy"
header-img: "img/post-bg-2015.jpg"
catalog: true
category: algnote
algnote-tags:
    - Coding Interview
    - Coding Practice
    - Algorithms and Data Structures
    - Sorting
---

## Question

Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.

**Example:**

```
Input: 1->2->4, 1->3->4
Output: 1->1->2->3->4->4
```

## Solution
TODO

#### Code
```java
class Solution {
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        if(l1 == null) return l2;
        if(l2 == null) return l1;
        
        ListNode dummyHead = new ListNode(0);
        ListNode tail = dummyHead;
        while(l1 != null || l2 != null) {
            boolean selectL1 = true;
            if(l1 == null || l2 != null && l1.val > l2.val) selectL1 = false;
            
            if(selectL1) {
                tail.next = l1;
                l1 = l1.next;
            }
            else {
                tail.next = l2;
                l2 = l2.next;
            }
            
            tail = tail.next;
        }
        
        return dummyHead.next;
        
    }
}
```

## Performance
TODO