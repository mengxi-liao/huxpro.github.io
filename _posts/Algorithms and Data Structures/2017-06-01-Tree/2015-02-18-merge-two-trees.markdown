---
layout:     post
title:      "Problem: Merge Two Trees"
date:       2015-02-18 00:00:00
author:     "Marcy"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - Coding Interview
    - Coding Practice
    - Algorithms and Data Structures
    - Tree
    - Medium
---

## Question

Given two binary trees and imagine that when you put one of them to cover the other, some nodes of the two trees are overlapped while the others are not.

You need to merge them into a new binary tree. The merge rule is that if two nodes overlap, then sum node values up as the new value of the merged node. Otherwise, the NOT null node will be used as the node of the new tree.

```
Example 1:
Input: 
    Tree 1         Tree 2  
          1           2  
         / \         / \  
        3   2       1   3   
       /            \   \ 
      5              4   7
Output: 
Merged tree:
         3
        / \
       4   5
      / \   \ 
     5   4   7
```

Note: The merging process must start from the root nodes of both trees.


## Solution

Start from the roots of both trees, `t1` and `t2`. The merged node will be a new node with value `t1.val + t2.val`. The left subtree will be a merged tree of `t1.left` and `t2.left`. Same to the right subtree, it will have the value of `t1.right + t2.right`. It is apparent this could be resolved by recursion.

One note here is that when merging two trees if the root of one tree is `null`, we could simply return the other tree.

#### Code

Here is a sample solution.

```java
class Solution {
    public TreeNode mergeTrees(TreeNode t1, TreeNode t2) {
        if(t1 == null) return t2;
        if(t2 == null) return t1;
        
        TreeNode n = new TreeNode(t1.val + t2.val);
        n.left = mergeTrees(t1.left, t2.left);
        n.right = mergeTrees(t1.right, t2.right);
        
        return n;
    }
}
```

## Performance

- Time complexity : `O(n)`. We traverse over a total of `n` nodes. Here, `n` refers to the smaller of the number of nodes in the two trees.
- Space complexity : `O(n)`. The depth of stack can grow up to `n` in case of a skewed tree.
