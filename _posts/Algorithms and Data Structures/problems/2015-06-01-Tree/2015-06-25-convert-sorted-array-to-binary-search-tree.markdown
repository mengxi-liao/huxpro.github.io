---
layout:     post
title:      "Problem: Convert Sorted Array to Binary Search Tree"
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
    - Binary Tree
    - Medium
---

## Question

Given an array where elements are sorted in ascending order, convert it to a height balanced BST.

For this problem, a height-balanced binary tree is defined as a binary tree in which the depth of the two subtrees of every node never differs by more than 1.


**Example:**

Given the sorted array: `[-10,-3,0,5,9]`,

One possible answer is: `[0,-3,9,-10,null,5]`, which represents the following height balanced BST:

```
      0
     / \
   -3   9
   /   /
 -10  5
 ```

## Solution

To generate a BST from a sorted array, we could pick a node, `nums[i]`, from the array as the root. And then all the nodes on its left (`nums[0]..nums[i-1]`) will form its left subtree. And all the nodes on the right (`nums[i+1]..nums[n-1]`) will form its right subtree. The left subtree and the right subtree can be generated via the same method recursively.

To make sure the tree is height-balanced, each time we could pick the middle element of the array as the root so the numbers of nodes of its left subtree and its right subtree will never differ more than 1.

#### Code

```java
class Solution {
    public TreeNode sortedArrayToBST(int[] nums) {
        return convert(nums, 0, nums.length-1);
    }

    TreeNode convert(int[] nums, int l, int r) {
        if(l>r) return null;
        int mid = (l+r)/2;
        TreeNode n = new TreeNode(nums[mid]);
        n.left = convert(nums, l,mid-1);
        n.right = convert(nums, mid+1, r);

        return n;
    }
}
```

## Performance

Each element in the array is visited and picked once, so the time complexity is `O(n)`. And its space complexity is `O(n)` as well.
