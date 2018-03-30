---
layout:     post
title:      "Problem: Add Two Numbers"
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

You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

**Example:**
```
Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 0 -> 8
Explanation: 342 + 465 = 807.
```

## Solution
TODO

#### Code
```java
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        // dummy head is useful when you need a previous node for iteration
        ListNode dummyHead = new ListNode(0);
        ListNode cur = dummyHead;
        int carry = 0;
        // the trick is here!!
        // enter the while loop we have a value on l1, l2, or carry
        // set it to 0 if one does not have a value
        while(l1!=null || l2!=null || carry > 0) {
            int val1 = 0;
            if(l1 != null) {
                val1 = l1.val;
                l1 = l1.next;
            }
            int val2 = 0;
            if(l2 != null) {
                val2 = l2.val;
                l2 = l2.next;
            }
            int sum = val1 + val2 + carry;
            int val = sum % 10;
            carry = (sum >= 10 ? 1 : 0);
            cur.next = new ListNode(val);
            cur = cur.next;
        }
        
        return dummyHead.next;
    }
}
```

## Performance
TODO