---
layout:     post
title:      "Problem: Diameter of Binary Tree"
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
    - Binary Tree
    - Medium
---

## Question

Given a binary tree, you need to compute the length of the diameter of the tree. The diameter of a binary tree is the length of the longest path between any two nodes in a tree. This path may or may not pass through the root.

**Example:**
Given a binary tree
```
          1
         / \
        2   3
       / \     
      4   5    
```

Return 3, which is the length of the path [4,2,1,3] or [5,2,1,3].

**Note:** The length of path between two nodes is represented by the number of edges between them.

## Solution

TODO

#### Code

Here is a sample solution.

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
    int max = 0;
    public int diameterOfBinaryTree(TreeNode root) {
        calHeight(root);
        
        return max;
    }
    
    public int calHeight(TreeNode root) {
        if(root == null) return 0;
        int l = calHeight(root.left);
        int r = calHeight(root.right);
        
        max = Math.max(l+r, max);
        
        return Math.max(l, r) + 1;
    }
}
```

## Performance
`O(n)`
