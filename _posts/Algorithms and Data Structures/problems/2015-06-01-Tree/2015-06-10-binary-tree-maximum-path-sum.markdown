---
layout:     post
title:      "Problem: Binary Tree Maximum Path Sum"
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

Given a non-empty binary tree, find the maximum path sum.

For this problem, a path is defined as any sequence of nodes from some starting node to any node in the tree along the parent-child connections. The path must contain at least one node and does not need to go through the root.

**Example 1:**
```
Input: [1,2,3]

       1
      / \
     2   3

Output: 6
```

**Example 2:**
```
Input: [-10,9,20,null,null,15,7]

   -10
   / \
  9  20
    /  \
   15   7

Output: 42
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
    int maxSum = Integer.MIN_VALUE;
    public int maxPathSum(TreeNode root) {
        maxPathSumFrom(root);
        return maxSum;
    }
    
    public int maxPathSumFrom(TreeNode root) {
        if(root == null) return Integer.MIN_VALUE;
        int left = maxPathSumFrom(root.left);
        int right = maxPathSumFrom(root.right);
        
        int sum = root.val;
        if(left > 0) sum += left;
        if(right > 0) sum += right;
        
        maxSum = Math.max(sum, maxSum);
        
        if(left < 0 && right < 0) return root.val;
        return Math.max(left, right) + root.val;
    }
}
```

## Performance
`O(n)`
