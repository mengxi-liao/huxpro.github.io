---
layout:     post
title:      "Problem: Construct Binary Tree from Inorder and Postorder Traversal"
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

Given inorder and postorder traversal of a tree, construct the binary tree.

**Note:**
You may assume that duplicates do not exist in the tree.

For example, given
```
inorder = [9,3,15,20,7]
postorder = [9,15,7,20,3]
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
    public TreeNode buildTree(int[] inorder, int[] postorder) {
        Map<Integer, Integer> map = new HashMap<>();
        for(int i=0;i<inorder.length; i++) {
            map.put(inorder[i], i);
        }

        Queue<Integer> q = new LinkedList<>();
        for(int i=postorder.length-1; i>=0; i--) {
            q.add(postorder[i]);
        }

        return buildTree(q, map, 0, inorder.length-1);
    }

    private TreeNode buildTree(Queue<Integer> q, Map<Integer, Integer> map, int start, int end) {
        if(q.isEmpty()) return null;
        if(start > end) return null;
        int val = q.poll();
        int index = map.get(val);
        TreeNode n = new TreeNode(val);
        n.right = buildTree(q, map, index+1, end);
        n.left = buildTree(q, map, start, index-1);

        return n;
    }
}
```

## Performance
`O(n)` with using hashmap.
