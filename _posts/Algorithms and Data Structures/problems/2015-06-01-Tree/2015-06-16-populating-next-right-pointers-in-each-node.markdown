---
layout:     post
title:      "Problem: Populating Next Right Pointers in Each Node II"
date:       2015-02-18 00:00:00
author:     "Marcy"
header-img: "img/post-bg-2015.jpg"
catalog: true
category: algnote
algnote-tags:
    - Coding Interview
    - Coding Practice
    - Algorithms and Data Structures
    - Tree
    - Breadth First Search
    - Medium
    - Binary Tree
---

## Question

Given a binary tree

```
struct TreeLinkNode {
  TreeLinkNode *left;
  TreeLinkNode *right;
  TreeLinkNode *next;
}
```

Populate each next pointer to point to its next right node. If there is no next right node, the next pointer should be set to NULL.

Initially, all next pointers are set to NULL.

**Note:**

- You may only use constant extra space.
- Recursive approach is fine, implicit stack space does not count as extra space for this problem.

**Example:**

Given the following perfect binary tree,
```
     1
   /  \
  2    3
 / \  / \
4  5  6  7
```
After calling your function, the tree should look like:
```
     1 -> NULL
   /  \
  2 -> 3 -> NULL
 / \  / \
4->5->6->7 -> NULL
```

## Solution

TODO

#### Code
```java
/**
 * Definition for binary tree with next pointer.
 * public class TreeLinkNode {
 *     int val;
 *     TreeLinkNode left, right, next;
 *     TreeLinkNode(int x) { val = x; }
 * }
 */
public class Solution {
    public void connect(TreeLinkNode root) {
        TreeLinkNode nextHead = root;
        while(nextHead != null) {
            TreeLinkNode curr = nextHead;
            TreeLinkNode prevChild = null;
            nextHead = null;
            while(curr != null) {
                if(curr.left != null) {
                    if(nextHead == null) nextHead = curr.left;
                    if(prevChild != null) {
                        prevChild.next = curr.left;
                    }
                    prevChild = curr.left;
                }
                if(curr.right != null) {
                    if(nextHead == null) nextHead = curr.right;
                    if(prevChild != null) {
                        prevChild.next = curr.right;
                    }
                    prevChild = curr.right;
                }
                curr = curr.next;
            }

            curr = nextHead;
        }
    }
}
```

## Performance

O(num of nodes)
