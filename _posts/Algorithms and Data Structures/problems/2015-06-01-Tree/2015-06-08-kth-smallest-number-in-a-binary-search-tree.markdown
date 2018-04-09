---
layout:     post
title:      "Problem: kth Smallest in a Binary Search Tree"
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
    - Binary Search Tree
    - Medium
---

## Question

Given a binary search tree, write a function kthSmallest to find the kth smallest element in it.

**Note:**
You may assume k is always valid, 1 ≤ k ≤ BST's total elements.

**Follow up:**
What if the BST is modified (insert/delete operations) often and you need to find the kth smallest frequently? How would you optimize the kthSmallest routine?

## Recursive Solution

TODO

#### Code

Here is a sample solution.

```java
class Solution {
    public int kthSmallest(TreeNode root, int k) {
        int count = 0;
        Stack<TreeNode> s = new Stack();
        TreeNode node = root;
        while(!s.isEmpty() || node != null) {
            if(node != null) {
                s.push(node);
                node = node.left;
            }
            else {
                TreeNode top = s.pop();
                if(++count == k) return top.val;
                node = top.right;
            }
        }
        return 0;
    }
}
```

## Iterative Solution

TODO

#### Code

Here is a sample solution.

```java
class Solution {
    int count = 0;
    int res;
    int k;
    public int kthSmallest(TreeNode root, int k) {
        this.k = k;
        inorder(root);
        return res;
    }

    private void inorder(TreeNode root) {
        if(root == null) return;
        if(count == k) return;
        inorder(root.left);
        count ++;
        if(count == k) res = root.val;
        inorder(root.right);
    }
}
```

## Performance
TODO
