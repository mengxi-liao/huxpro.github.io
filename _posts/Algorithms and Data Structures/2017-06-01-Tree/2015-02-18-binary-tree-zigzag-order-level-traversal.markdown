---
layout:     post
title:      "Problem: Binary Tree Zigzag Order Level Traversal"
date:       2015-02-18 00:00:00
author:     "Marcy"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - Coding Interview
    - Coding Practice
    - Algorithms and Data Structures
    - Tree
    - Breadth First Search
---

## Question

Given a binary tree, return the zigzag level order traversal of its nodes' values. (ie, from left to right, then right to the left for the next level and alternate between).

For example:
Given binary tree `[3,9,20,null,null,15,7]`,
```
    3
   / \
  9  20
    /  \
   15   7
```
return its zigzag level order traversal as:
```
[
  [3],
  [20,9],
  [15,7]
]
```

## Solution

The solution is similar to [Binary Tree Level Order Traversal](/2015/02/17/binary-tree-level-order-traversal/). The only difference is we need to use a variable to mark the direction of each level. Swith the direction for each level. If the direction is from left to right, add the node to the end of the current level result. Otherwise, add the node to the beginning of the current level result.

#### Code

```java
class Solution {
    public List<List<Integer>> zigzagLevelOrder(TreeNode root) {
        Queue<TreeNode> q = new LinkedList();
        List<List<Integer>> results = new ArrayList();
        if(root == null) return results;
        q.add(root);
        boolean left2right = true;
        while(!q.isEmpty()) {
            int size = q.size();
            List<Integer> res = new ArrayList();
            results.add(res);
            for(int i=0; i<size; i++) {
                TreeNode n = q.poll();
                if(left2right) {
                    res.add(n.val);
                }
                else {
                    res.add(0, n.val);
                }
                if(n.left != null) q.add(n.left);
                if(n.right != null) q.add(n.right);
            }
            left2right = !left2right;
        }
        return results;
    }
}
```

## Performance

As using **BFS**, both the time complexity and the space complexity are `O(n)`.