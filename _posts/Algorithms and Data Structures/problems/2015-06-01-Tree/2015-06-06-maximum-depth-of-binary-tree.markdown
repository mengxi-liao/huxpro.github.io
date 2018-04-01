---
layout:     post
title:      "Problem: Maximum Depth of Binary Tree"
date:       2015-02-18 00:00:00
author:     "Marcy"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - Coding Interview
    - Coding Practice
    - Algorithms and Data Structures
    - Tree
    - Depth First Search
    - Easy
---

## Question

Given a binary tree, find its maximum depth.

The maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.

For example:
Given binary tree `[3,9,20,null,null,15,7]`,

```
    3
   / \
  9  20
    /  \
   15   7
```

return its depth = 3.

## Solution

**Depth First Search (BFS)** can be used to solve the problem. The max depth of the current node is the greater one between the maximum depth of the left child and the maximum depth of the right child plus one.

#### Code

Here is a sample solution.

```java
class Solution {
    public int maxDepth(TreeNode root) {
        if(root == null) return 0;
        return Math.max(maxDepth(root.left), maxDepth(root.right)) + 1;
    }
}
```

## Performance

For **DFS**, the time complexity is `O(n)`. And as it is using recursion, it needs `O(n)` extra space.
