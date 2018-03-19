---
layout:     post
title:      "Problem: kth Smallest in a Binary Search Tree"
date:       2015-02-18 00:00:00
author:     "Marcy"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - Coding Interview
    - Coding Practice
    - Algorithms and Data Structures
    - Tree
    - Binary Search Tree
---

## Question

Given a singly linked list where elements are sorted in ascending order, convert it to a height balanced BST.

For this problem, a height-balanced binary tree is defined as a binary tree in which the depth of the two subtrees of every node never differ by more than 1.


**Example:**

```
Given the sorted linked list: [-10,-3,0,5,9],

One possible answer is: [0,-3,9,-10,null,5], which represents the following height balanced BST:

      0
     / \
   -3   9
   /   /
 -10  5
```

## Solution

TODO

#### Code

Here is a sample solution.

```java
public class Solution {
    private ListNode current;

    public TreeNode sortedListToBST(ListNode head) {
        if(head == null) return null;
        
        int length = 0;
        
        ListNode node = head;
        while(node != null) {
            length ++;
            node = node.next;
        }
        
        current = head;
        return sortedListToBST(0, length-1);
    }

    // current will be at end+1 after each call
    public TreeNode sortedListToBST(int start, int end){
        if(start > end) return null;
        
        int mid = start + (end-start) / 2;
        // current at start
        TreeNode left = sortedListToBST(start, mid-1);
        // current at middle
        TreeNode node = new TreeNode(current.val);
        node.left = left;
        current = current.next;
        // current at middle+1
        node.right = sortedListToBST(mid+1, end);
        // current at end
        
        return node;
    }
}
```

## Performance
TODO