---
layout:     post
title:      "Problem: Lowest Common Ancestor of a Binary Search Trees"
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

Given a binary search tree (BST), find the lowest common ancestor (LCA) of two given nodes in the BST.

According to the definition of LCA on Wikipedia: “The lowest common ancestor is defined between two nodes v and w as the lowest node in T that has both v and w as descendants (where we allow a node to be a descendant of itself).”

```

        _______6______
       /              \
    ___2__          ___8__
   /      \        /      \
   0      _4       7       9
         /  \
         3   5
```

For example, the lowest common ancestor (LCA) of nodes 2 and 8 is 6. Another example is LCA of nodes 2 and 4 is 2, since a node can be a descendant of itself according to the LCA definition.

## Solution

TODO

#### Code

```java
class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        int large = p.val;
        int small = q.val;
        if(q.val > p.val) {
            large = q.val;
            small = p.val;
        }
        
        if(root.val > large) {
            return lowestCommonAncestor(root.left, p, q);
        }
        else if(root.val < small){
            return lowestCommonAncestor(root.right, p, q);
        }
        
        return root;
    }
}
```

## Performance
TODO
