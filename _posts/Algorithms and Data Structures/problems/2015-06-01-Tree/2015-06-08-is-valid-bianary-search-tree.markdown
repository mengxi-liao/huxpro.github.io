---
layout:     post
title:      "Problem: Validate Binary Search Tree"
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
    - Binary Search Tree
    - Medium
---

## Question

Given a binary tree, determine if it is a valid binary search tree (BST).

Assume a BST is defined as follows:

The left subtree of a node contains only nodes with keys less than the node's key.
The right subtree of a node contains only nodes with keys greater than the node's key.
Both the left and right subtrees must also be binary search trees.

**Example 1:**
```
    2
   / \
  1   3
Binary tree [2,1,3], return true.
```

**Example 2:**
```
    1
   / \
  2   3
Binary tree [1,2,3], return false.
```

## Solution

TODO

#### Code

```java
class Solution {
    public boolean isValidBST(TreeNode root) {
        return isValidBST(root, Long.MIN_VALUE, Long.MAX_VALUE);
    }

    public boolean isValidBST(TreeNode node, long min, long max) {
        return node == null || node.val > min && node.val < max
            && isValidBST(node.left, min, node.val)
            && isValidBST(node.right, node.val, max);
    }
}
```

## Performance
TODO
