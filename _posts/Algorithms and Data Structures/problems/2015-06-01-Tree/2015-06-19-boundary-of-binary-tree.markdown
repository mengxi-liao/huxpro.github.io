---
layout:     post
title:      "Problem: Boundary of Binary Tree"
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
    - Depth First Search
    - Medium
    - Binary Tree
---

## Question

Given a binary tree, return the values of its boundary in an anti-clockwise direction starting from the root. Boundary includes left boundary, leaves, and right boundary in order without duplicate nodes.

Left boundary is defined as the path from the root to the left-most node. Right boundary is defined as the path from the root to the right-most node. If the root doesn't have left subtree or right subtree, then the root itself is left boundary or right boundary. Note this definition only applies to the input binary tree, and not applies to any subtrees.

The left-most node is defined as a leaf node you could reach when you always firstly travel to the left subtree if exists. If not, travel to the right subtree. Repeat until you reach a leaf node.

The right-most node is also defined by the same way with left and right exchanged.

**Example 1**
```
Input:
  1
   \
    2
   / \
  3   4

Output:
[1, 3, 4, 2]

Explanation:
The root doesn't have left subtree, so the root itself is left boundary.
The leaves are node 3 and 4.
The right boundary is node 1,2,4. Note the anti-clockwise direction means you should output reversed right boundary.
So order them in anti-clockwise without duplicates, and we have [1,3,4,2].
```

**Example 2**
```
Input:
    ____1_____
   /          \
  2            3
 / \          / 
4   5        6   
   / \      / \
  7   8    9  10  
       
Ouput:
[1,2,4,7,8,9,10,6,3]

Explanation:
The left boundary is node 1,2,4. (4 is the left-most node according to definition)
The leaves are node 4,7,8,9,10.
The right boundary is node 1,3,6,10. (10 is the right-most node).
So order them in anti-clockwise without duplicate nodes we have [1,2,4,7,8,9,10,6,3].
```

## Solution

Break down the problem to a few subproblems. The boundary of the tree contains:
- the root
- the left boundary of the left subtree (excluding the leaf)
- the leaves of the left subtree
- the leaves of the right subtree
- the right boundary of the right subtree (excluding the leaf)

All the subproblems can be solved by **Depth First Search(DFS)**.

#### Code

```java
class Solution {
    public List<Integer> boundaryOfBinaryTree(TreeNode root) {
        List<Integer> boundary = new ArrayList<>();
        if(root == null) return boundary;
        boundary.add(root.val);
        leftBound(root.left,boundary);
        leaves(root.left,boundary);
        leaves(root.right,boundary);
        rightBound(root.right,boundary);
        return boundary;
    }

    private void leaves(TreeNode root, List<Integer> boundary) {
        if(root == null) return;
        if(root.left == null && root.right == null) {
            boundary.add(root.val);
            return;
        }
        leaves(root.left, boundary);
        leaves(root.right, boundary);
    }

    private void leftBound(TreeNode root, List<Integer> boundary) {
        if(root == null || root.left == null && root.right == null) return;
        boundary.add(root.val);
        if(root.left != null) leftBound(root.left, boundary);
        else if(root.right != null) leftBound(root.right, boundary);
    }

    private void rightBound(TreeNode root, List<Integer> boundary) {
        if(root == null || root.left == null && root.right == null) return;
        if(root.right != null) rightBound(root.right, boundary);
        else if(root.left != null) rightBound(root.left, boundary);    
        boundary.add(root.val);
    }
}
```

## Performance

Using **DFS** needs `O(n)` time complexity and space complexity.
