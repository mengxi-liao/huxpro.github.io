---
layout:     post
title:      "Problem: Palindrome Linked List"
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
    - Two Pointers
    - Medium
---

## Question

Given a singly linked list, determine if it is a palindrome.

**Follow up:**
Could you do it in O(n) time and O(1) space?

## Solution
TODO

#### Code
```java
class Solution {
    public boolean isPalindrome(ListNode head) {
        ListNode w = head;
        ListNode r = head;
        while(r != null && r.next != null) {
            r = r.next.next;
            w = w.next;
        }
        
        // find the middle of the list
        // skip the middle
        if(r != null) {
            w = w.next;
        }
        
        ListNode head2 = reverse(w);
        
        // head2 should have equal length or 1 node shorter
        while(head2 != null) {
            if(head.val != head2.val) return false;
            head = head.next;
            head2 = head2.next;
        }
        
        return true;
    }
    
    public ListNode reverse(ListNode head) {
        ListNode newHead = null;
        while(head != null) {
            ListNode tmp = head;
            head = head.next;
            tmp.next = newHead;
            newHead = tmp;
        }
        
        return newHead;
    }
}
```

## Performance
TODO
