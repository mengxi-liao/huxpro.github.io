---
layout:     post
title:      "Problem: Add Two Numbers II"
date:       2015-02-18 00:00:00
author:     "Marcy"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - Coding Interview
    - Coding Practice
    - Algorithms and Data Structures
    - Linked List
    - Hard
---

## Question

You are given two non-empty linked lists representing two non-negative integers. The most significant digit comes first and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

**Follow up:**
What if you cannot modify the input lists? In other words, reversing the lists is not allowed.

**Example:**
```
Input: (7 -> 2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 8 -> 0 -> 7
```

## Solution
TODO

#### Code
```java
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        ListNode n = l1;
        int l1Len = 0;
        while(n != null) {
            l1Len ++;
            n = n.next;
        }

        n = l2;
        int l2Len = 0;
        while(n != null) {
            l2Len ++;
            n = n.next;
        }

        ListNode dummyHead = new ListNode(0);
        int carry = add(l1, l1Len, l2, l2Len, dummyHead);
        if(carry > 0) {
            ListNode newHead = new ListNode(carry);
            newHead.next = dummyHead.next;
            dummyHead.next = newHead;
        }

        return dummyHead.next;
    }

    public int add(ListNode l1, int l1Len, ListNode l2, int l2Len, ListNode dummyHead) {
        if(l1Len == 0 && l2Len == 0) return 0;
        int carry = 0;
        int sum = 0;
        if(l1Len > l2Len) {
            carry = add(l1.next, l1Len-1, l2, l2Len, dummyHead);
            sum = l1.val + carry;
        }
        else if(l1Len < l2Len) {
            carry = add(l1, l1Len, l2.next, l2Len-1, dummyHead);
            sum = l2.val + carry;
        }
        else {
            carry = add(l1.next, l1Len-1, l2.next, l2Len-1, dummyHead);
            sum = l1.val + l2.val + carry;
        }
        ListNode newHead = new ListNode(sum%10);
        newHead.next = dummyHead.next;
        dummyHead.next = newHead;
        return sum / 10;
    }
}
```

## Performance
TODO
