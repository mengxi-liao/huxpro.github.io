---
layout:     post
title:      "Problem: Binary Tree Level Order Traversal"
date:       2015-02-18 00:00:00
author:     "Marcy"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - Coding Interview
    - Coding Practice
    - Algorithms and Data Structures
    - Tree
    - Breath First Search
---

## Question

Given a binary tree, return the level order traversal of its nodes' values. (ie, from left to right, level by level).

For example:
Given binary tree `[3,9,20,null,null,15,7]`,
```
    3
   / \
  9  20
    /  \
   15   7
```
return its level order traversal as:
```
[
  [3],
  [9,20],
  [15,7]
]
```


## Solution

**Breath First Search (BFS)** can be used to solve the problem.

#### Code

Here is a sample solution.

```java
public class Solution {
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> res = new ArrayList<>();
        if(root == null) return res;
        
        Queue<TreeNode> q = new LinkedList<>();
        q.add(root);
        
        while(!q.isEmpty()) {
            
            int curLevelCount = q.size();
            List<Integer> layerValues = new ArrayList<>();
            
            while(curLevelCount-- > 0) {
                TreeNode node = q.poll();
                layerValues.add(node.val);
                
                if(node.left != null) 
                    q.add(node.left);
                if(node.right != null) 
                    q.add(node.right);
            }
            
            res.add(layerValues);
        }
        
        return res;
    }
}
```

## Performance

Each node is pushed and polled from the queue once, so the overall time complexity is `O(n)`.
