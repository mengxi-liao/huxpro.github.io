---
layout:     post
title:      "Problem: Recover Binary Search Tree"
date:       2015-02-18 00:00:00
author:     "Marcy"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - Coding Interview
    - Coding Practice
    - Algorithms and Data Structures
    - Depth First Search
    - Tree
    - Binary Search Tree
    - Hard
---

## Question

Two elements of a binary search tree (BST) are swapped by mistake.

Recover the tree without changing its structure.

## Solution

For a binary search tree, we know if we print the nodes via inorder traversal, we should get an ordered sequence. However, as two nodes are swapped, the result sequence won't be sorted. And this gives us the opportunity to identify the swapped nodes.

For example:
```
   1
  / \
 3   4
```

The inorder sequence of the above tree is `3,1,4`. There's one unsorted pair (`3,1`) in the sequence, and `3` and `1` are swapped. However, before we make any conclusion, let's take a look at another example:

```
  3
 / \
4   1
```

The inorder sequence of the above tree is `4,3,1`. There're two unsorted pairs (`4,3`) and (`3,1`) in the sequence, and `4` and `1` are swapped.

So what's the difference between these two trees? Well, for the swapped pair in the first tree, one node is the parent of the other node. This is not the case for the other tree.

Let's take a look for the last example:

```
3
 \
  6
   \
    5
     \
      4
```

The inorder sequence of the above tree is `3,6,5,4`. There're two unsorted pairs (`6,5`) and (`5,4`) in the sequence, and `4` and `6` are swapped. Again, neither `6` is `4`'s parent, or `4` is `6`'s parent.

Here is the conclusion: To get the swapped nodes, we use inorder traversal to traverse the tree. And try to get the first two unsorted pairs. If there's only one unsorted pair, the two nodes of the pair are swapped. If there are two unsorted pairs, the first node in the first pair and the second node in the second pair are the two swapped nodes.

#### Code

```java
class Solution {
    TreeNode n1;
    TreeNode n2;
    TreeNode prev;
    public void recoverTree(TreeNode root) {
        inorderTraversal(root);
        swapNodes(n1, n2);
    }

    public void inorderTraversal(TreeNode n) {
        if(n == null) return;
        inorderTraversal(n.left);
        if(prev != null && prev.val > n.val) {
            if(n1 == null) n1 = prev;
            n2 = n;
        }
        prev = n;
        inorderTraversal(n.right);
    }

    private void swapNodes(TreeNode n1, TreeNode n2) {
        int t = n1.val;
        n1.val = n2.val;
        n2.val = t;
    }
}
```

## Performance

This solution uses inorder traversal (Depth First Search) to traverse the tree, so both its time complexity and space complexity are `O(n)`.
