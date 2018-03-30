---
layout:     post
title:      "Problem: Reverse Linked List"
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

Reverse a singly linked list.

## Solution
TODO

#### Code
```java
class Solution {
    public ListNode reverseList(ListNode head) {
        if(head == null) return null;
        if(head.next == null) return head;

        ListNode next = head.next;
        ListNode newHead = reverseList(next);
        next.next = head;
        head.next = null;

        return newHead;
    }
}
```

#### Performance
TODO

## Solution
TODO

#### Code
```java
class Solution {
    public ListNode reverseList(ListNode head) {
        if(head == null) return null;
        if(head.next == null) return head;

        ListNode newHead = null;
        while(head != null) {
            ListNode temp = newHead;
            newHead = head;
            head = head.next;
            newHead.next = temp;
        }

        return newHead;
    }
}
```

#### Performance
TODO