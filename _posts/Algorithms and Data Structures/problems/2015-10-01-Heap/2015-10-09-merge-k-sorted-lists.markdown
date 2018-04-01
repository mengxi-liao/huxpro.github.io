---
layout:     post
title:      "Problem: Merge K Sorted Lists"
date:       2015-02-18 00:00:00
author:     "Marcy"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - Coding Interview
    - Coding Practice
    - Algorithms and Data Structures
    - Heap
    - Divide and Conquer
    - Medium
---

## Question

Merge k sorted linked lists and return it as one sorted list. Analyze and describe its complexity.

## Priority Queue Solution
TODO

#### Code
```java
class Solution {
    public ListNode mergeKLists(ListNode[] lists) {
        if(lists.length == 0) return null;
        PriorityQueue<ListNode> pq = new PriorityQueue(lists.length, new Comparator<ListNode>() {
            @Override
            public int compare(ListNode o1,ListNode o2){
                return o1.val - o2.val;
            }
        });
        
        for (ListNode node:lists)
            if (node!=null)
                pq.add(node);
        
        ListNode dummy = new ListNode(0);
        ListNode tail = dummy;
        while(!pq.isEmpty()) {
            ListNode n = pq.poll();
            tail.next = n;
            tail = n;
            if(tail.next != null) pq.offer(tail.next);
        }
        
        return dummy.next;
    }
}
```

## Performance
TODO

## Divide and Conquer Solution
TODO

#### Code
```java
public class Solution {
    public ListNode mergeKLists(ListNode[] lists) {
        return mL(lists, 0, lists.length - 1);
    }
    
    private ListNode mL(ListNode[] lists, int l, int r) {
        if (r < l) return null;
        if (r == l) return lists[r];
        
        int mid = (l + r) / 2;
        ListNode a = mL(lists, l, mid), b = mL(lists, mid + 1, r);
        ListNode dmHead = new ListNode(0), cur = dmHead;
        while (a != null && b != null) {
            if (a.val < b.val) {
                cur.next = a;
                a = a.next;
            } else {
                cur.next = b;
                b = b.next;
            }
            cur = cur.next;
        }
        cur.next = (a != null) ? a : b;
        
        return dmHead.next;
    }
}
```

## Performance
TODO
