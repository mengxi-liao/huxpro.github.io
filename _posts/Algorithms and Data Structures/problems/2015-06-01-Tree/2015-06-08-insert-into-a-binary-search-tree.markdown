---
layout:     post
title:      "Problem: Insert into a BST"
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
    - Binary Tree
    - Medium
---

## Question

Given the root node of a binary search tree (BST) and a value to be inserted into the tree, insert the value into the BST. Return the root node of the BST after the insertion. It is guaranteed that the new value does not exist in the original BST.

Note that there may exist multiple valid ways for the insertion, as long as the tree remains a BST after insertion. You can return any of them.

**For example,**
```
Given the tree:
        4
       / \
      2   7
     / \
    1   3
And the value to insert: 5
You can return this binary search tree:

         4
       /   \
      2     7
     / \   /
    1   3 5
```

## Solution

TODO

#### Code

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public TreeNode insertIntoBST(TreeNode root, int val) {
        if(val < root.val) {
            if(root.left == null) root.left = new TreeNode(val);
            else insertIntoBST(root.left, val);
        }
        else {
            if(root.right == null) root.right = new TreeNode(val);
            else insertIntoBST(root.right, val);
        }
        return root;
    }
}
```
