---
layout:     post
title:      "Problem: Symmtric Tree"
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

Given a binary tree, check whether it is a mirror of itself (i.e., symmetric around its center).

For example, this binary tree `[1,2,2,3,4,4,3]` is symmetric:

```
    1
   / \
  2   2
 / \ / \
3  4 4  3
```

But the following `[1,2,2,null,3,null,3]` is not:

```
    1
   / \
  2   2
   \   \
   3    3
```

## Solution

To check if the two trees are symmetric, first, we need to check if the two roots, `n1` and `n2` have the same value. Then we need to check if the `n1.left` is symmetric to `n2.right` and `n1.right` is symmetric to `n2.left`. We could resolve this by recursion.

#### Code

Here is a sample solution.

```java
public class Solution {
  public boolean isSymmetric(TreeNode root) {
    return root == null || isSymmetric(root.left, root.right);
  }
  
  public boolean isSymmetric(TreeNode n1, TreeNode n2) {
    if(n1 == null || n2 == null)
      return n1==n2;
    
    return n1.val == n2.val &&
      isSymmetric(n1.left, n2.right) && 
      isSymmetric(n1.right, n2.left);
  }
}
```

## Performance
- Time complexity : `O(n)`. We traverse over a total of `2 x n` nodes. Here, `n` refers to the smaller of the number of nodes in the two trees.
- Space complexity : `O(n)`. The depth of stack can grow up to `n` in case of a skewed tree, and we need a new tree with `n` nodes.
