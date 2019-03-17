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
        Map<Integer, Integer> map = new HashMap<>();
        for(int i=0; i<inorder.length; i++) {
            map.put(inorder[i], i);
        }
        
        Queue<Integer> q = new LinkedList<Integer>();
        for(int i=0; i<preorder.length; i++) {
            q.add(preorder[i]);
        }
        
        return buildTree(q, map, inorder, 0, inorder.length-1);
    }
    
    private TreeNode buildTree(Queue<Integer> q, Map<Integer, Integer> map, int[] inorder, int s, int e) {
        if(q.isEmpty()) return null;
        if(s>e) return null;
        
        Integer val = q.poll();
        int idx = map.get(val);
        TreeNode node = new TreeNode(val);
        node.left = buildTree(q, map, inorder, s, idx-1);
        node.right = buildTree(q, map, inorder, idx+1, e);
        
        return node;
    }
}
```

## Performance
`O(n)` with using hashmap.
