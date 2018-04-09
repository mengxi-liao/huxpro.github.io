---
layout:     post
title:      "Problem: Binary Tree Min Depth"
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
    - Breadth First Search
---

## Question

Given a binary tree, find its minimum depth.

The minimum depth is the number of nodes along the shortest path from the root node down to the nearest leaf node.


## Solution 1

Traverse the tree using **Depth First Search(DFS)**. The `minDepth` of the current node is the min value between the `minDepth` of its left subtree and the `minDepth` of its right subtree plus 1.

#### Code

```java
class Solution {
    public int minDepth(TreeNode root) {
       if(root == null){
            return 0;
        }

        if(root.left == null && root.right == null)
            return 1;
        int left = Integer.MAX_VALUE, right = Integer.MAX_VALUE;
        if(root.left != null)
            left = minDepth(root.left);
        if(root.right != null)
            right = minDepth(root.right);

        return 1 + Math.min(left, right);
    }
}
```

## Solution 2

The problem could also be solved by **Breadth First Search(DFS)**. Use **BFS** to traverse the tree level by level. Once a leaf is found, it's guaranteed that the leaf is the nearest leaf from the root.

### Code

```java
class Solution {
    public int minDepth(TreeNode root) {
        if(root == null) return 0;
        Queue<TreeNode> q = new LinkedList<>();
        q.add(root);
        int level = 0;
        while(!q.isEmpty()) {
            level ++;
            int size = q.size();
            for(int i=0; i<size; i++) {
                TreeNode n = q.poll();
                if(n.left == null && n.right == null) return level;
                if(n.left != null) q.add(n.left);
                if(n.right != null) q.add(n.right);
            }
        }

        return -1;
    }
}
```

## Performance

Both **BFS** and **DFS** have `O(n)` time complexity and `O(n)` space complexity. However, for the **DFS** solution, we need to traverse every node to get the minimum depth. For **BFS**, once we reach a leaf, it must be the nearest leaf from the root so we could immediately return the minimum depth.

Optimization for the **DFS** solution could be using a variable to mark the current minimum depth and update it every time a leaf is found. If we reach a node that is deeper than the current minimum depth, we could stop traversing its children. However, this is still less performant than the **BFS** solution.
