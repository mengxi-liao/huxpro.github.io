---
layout:     post
title:      "Problem: Construct Binary Tree from Preorder and Inorder Traversal"
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

Given preorder and inorder traversal of a tree, construct the binary tree.

**Note:**
You may assume that duplicates do not exist in the tree.

For example, given
```
preorder = [3,9,20,15,7]
inorder = [9,3,15,20,7]
```
Return the following binary tree:

```
    3
   / \
  9  20
    /  \
   15   7
```

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
    public TreeNode buildTree(int[] preorder, int[] inorder) {
        Map<Integer, Integer> inorderMap = new HashMap<>();
        for(int i=0; i<inorder.length; i++) {
            inorderMap.put(inorder[i], i);
        }
        return buildTree(preorder, 0, preorder.length-1, inorderMap, 0, inorder.length-1);
    }

    private TreeNode buildTree(int[] preorder, int p1, int p2, Map<Integer, Integer> inorderMap, int i1, int i2) {
        if(p1 > p2) return null;
        TreeNode root = new TreeNode(preorder[p1]);
        if(p1 == p2) return root;

        int index = inorderMap.get(root.val);

        root.left = buildTree(preorder, p1+1, p1+index-i1, inorderMap, i1, index-1);
        root.right = buildTree(preorder, p1+index-i1+1, p2, inorderMap, index+1, i2);

        return root;
    }
}
```

## Performance
`O(n)` with using hashmap.
