---
layout:     post
title:      "Problem: Odd Even Linked List"
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

Given a singly linked list, group all odd nodes together followed by the even nodes. Please note here we are talking about the node number and not the value in the nodes.

You should try to do it in place. The program should run in O(1) space complexity and O(nodes) time complexity.

**Example:**
Given `1->2->3->4->5->NULL`,
return `1->3->5->2->4->NULL`.

**Note:**
The relative order inside both the even and odd groups should remain as it was in the input. 
The first node is considered odd, the second node even and so on ...

## Solution
TODO

#### Code
```java
class Solution {
    public ListNode oddEvenList(ListNode head) {
        ListNode oddHead = new ListNode(0), evenHead = new ListNode(0);
        ListNode oddTail = oddHead, evenTail = evenHead;
        boolean oddTurn = true;
        ListNode cur = head;
        
        while(cur != null) {
            if(oddTurn) {
                oddTail.next = cur;
                oddTail = cur;
            }
            else {
                evenTail.next = cur;
                evenTail = cur;
            }
            
            cur = cur.next;
            oddTurn = !oddTurn;
        }
        
        oddTail.next = evenHead.next;
        evenTail.next = null; // remember this !!!!
        
        return oddHead.next;
    }
}
```

## Performance
TODO