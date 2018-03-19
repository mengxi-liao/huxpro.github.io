---
layout:     post
title:      "Problem: Binary Tree Right Side View"
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
---

## Question

Given a binary tree, imagine yourself standing on the right side of it, return the values of the nodes you can see ordered from top to bottom.

For example:
Given the following binary tree,
```
   1            <---
 /   \
2     3         <---
 \     \
  5     4       <---
  ```
You should return `[1, 3, 4]`.


## Solution

User **Depth First Search(DFS)**

Traverse the binary tree. For a node, first visit its right child, then visit its left child. If it’s the first visit to the layer, add the value of the node to the result.

#### Code

Here is a sample solution.

```java
class Solution {
  public List<Integer> rightSideView(TreeNode root) {
    List<Integer> rightSideView = new ArrayList();
    collectRightSideView(root, rightSideView, 1);
    return rightSideView;
  }

  void collectRightSideView(TreeNode root, List<Integer> rightSideView, int level) {
    if(root == null) return;

    if(level > rightSideView.size()) {
        rightSideView.add(root.val);
    }
    collectRightSideView(root.right, rightSideView, level+1);
    collectRightSideView(root.left, rightSideView, level+1);
  }
}

```

## Performance

Using DFS to traverse a tree needs `O(n)` time complexity and `O(n)` space complexity.
