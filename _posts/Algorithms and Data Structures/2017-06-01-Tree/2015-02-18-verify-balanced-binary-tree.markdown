---
layout:     post
title:      "Problem: Verify Balanced Binary Tree"
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
    - Balanced Binary Tree
    - Depth First Search
---

## Question

Given a binary tree, determine if it is height-balanced.

For this problem, a height-balanced binary tree is defined as:

**A binary tree in which the depth of the two subtrees of every node never differ by more than 1.**

Example 1:
```
Given the following tree [3,9,20,null,null,15,7]:

    3
   / \
  9  20
    /  \
   15   7
Return true.
```

Example 2:
```
Given the following tree [1,2,2,3,3,null,null,4,4]:

       1
      / \
     2   2
    / \
   3   3
  / \
 4   4
Return false.
```

## Solution 1

This problem is believed to have two solutions: the top-down approach and the bottom-up way.

The first top-down approach checks whether the tree is balanced strictly based on the definition of balanced binary tree: the difference between the heights of the two subtrees are not greater than 1, and both the left subtree and right subtree are also balanced.

#### Code

```java
class Solution {
    public int depth (TreeNode root) {
        if (root == null) return 0;
        return Math.max(depth(root.left), depth (root.right)) + 1;
    }

    public boolean isBalanced(TreeNode root) {
        if (root == null) return true;
        
        int left=depth(root.left);
        int right=depth(root.right);
        
        return Math.abs(left - right) <= 1 
          && isBalanced(root.left) 
          && isBalanced(root.right);
    }
}
```

#### Performance

For the current node root, calling `depth()` for its left and right children may visit all of its children. Thus the complexity is worst case `O(n)`. We do this for each node in the tree, so the overall complexity of isBalanced will be `O(n^2)`.

## Solution 2

Use **Depth First Search (DFS)**. Instead of calling `depth()` explicitly for each child node, return the height of the current node in `DFS` recursion. When the subtree of the current node (inclusive) is balanced, the function `checkHeight()` returns a non-negative value as the height. Otherwise `-1` is returned. According to the left height and right height of the two children, the parent node could check if the subtree is balanced, and decides its return value.

#### Code

Here is a sample solution.

```java
class Solution {
    boolean balanced = true;
    
    public boolean isBalanced(TreeNode root) {
        checkHeight(root);
        return balanced;
    }
    
    public int checkHeight(TreeNode root) {
        if(balanced == false) return -1;
        if(root == null) return 0;
        
        int l = checkHeight(root.left);
        int r = checkHeight(root.right);
        
        if(Math.abs(l-r) > 1) balanced = false;
        return Math.max(l, r)+1;
    }
}
```

#### Performance

In this bottom-up approach, each node in the tree only needs to be accessed once. Thus the time complexity is `O(n)`, better than the first solution.
