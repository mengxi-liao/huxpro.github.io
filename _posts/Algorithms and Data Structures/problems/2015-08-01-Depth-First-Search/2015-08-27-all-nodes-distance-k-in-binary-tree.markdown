---
layout:     post
title:      "Problem: All Nodes Distance K in Binary Tree"
date:       2015-02-18 00:00:00
author:     "Marcy"
header-img: "img/post-bg-2015.jpg"
catalog: true
category: algnote
algnote-tags:
    - Coding Interview
    - Coding Practice
    - Algorithms and Data Structures
    - Depth First Search
    - Breath First Search
    - Medium
---

## Question

We are given a binary tree (with root node root), a target node, and an integer value K.

Return a list of the values of all nodes that have a distance K from the target node.  The answer can be returned in any order.

**Example 1:**
```
Input: root = [3,5,1,6,2,0,8,null,null,7,4], target = 5, K = 2

Output: [7,4,1]

Explanation:
The nodes that are a distance 2 from the target node (with value 5)
have values 7, 4, and 1.

Note that the inputs "root" and "target" are actually TreeNodes.
The descriptions of the inputs above are just serializations of these objects.
```

**Note:**
- The given tree is non-empty.
- Each node in the tree has unique values 0 <= node.val <= 500.
- The target node is a node in the tree.
- 0 <= K <= 1000.

#### Code
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
    public List<Integer> distanceK(TreeNode root, TreeNode target, int K) {
        List<TreeNode> list = dfsFindParents(root, target);
        List<Integer> results = new ArrayList<>();
        results.addAll(dfsFindChildren(target, K));
        TreeNode current = target;
        for(int i=list.size()-2; i>=0 && K>=1; i--) {
            TreeNode parent = list.get(i);
            if(K == 1) {
                results.add(parent.val);
            }
            else if(parent.left == current) {
                results.addAll(dfsFindChildren(parent.right, K-2));
            }
            else {
                results.addAll(dfsFindChildren(parent.left, K-2));
            }
            K--;
            current = parent;
        }
        return results;
    }

    private List<TreeNode> dfsFindParents(TreeNode root, TreeNode target) {
        if(root == null) return null;
        if(root == target) {
            List<TreeNode> list = new ArrayList<>();
            list.add(target);
            return list;
        }
        List list = dfsFindParents(root.left, target);
        if(list == null) list = dfsFindParents(root.right, target);
        if(list != null) list.add(0, root);
        return list;
    }

    private List<Integer> dfsFindChildren(TreeNode root, int k) {
        List<Integer> list = new ArrayList<>();
        if(root == null) return list;
        if(k == 0) {
            list.add(root.val);
        }
        else {
            list.addAll(dfsFindChildren(root.left, k-1));
            list.addAll(dfsFindChildren(root.right, k-1));
        }
        return list;
    }
}
```
