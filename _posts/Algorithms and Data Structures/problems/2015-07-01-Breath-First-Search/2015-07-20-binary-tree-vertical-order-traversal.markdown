---
layout:     post
title:      "Problem: Binary Tree Vertical Order Traversal"
date:       2015-02-18 00:00:00
author:     "Marcy"
header-img: "img/post-bg-2015.jpg"
catalog: true
category: algnote
algnote-tags:
    - Coding Interview
    - Coding Practice
    - Algorithms and Data Structures
    - Breadth First Search
    - Medium
---

## Question

Given a binary tree, return the vertical order traversal of its nodes' values. (ie, from top to bottom, column by column).

If two nodes are in the same row and column, the order should be from left to right.

**Examples 1:**

```
Input: [3,9,20,null,null,15,7]

   3
  /\
 /  \
 9  20
    /\
   /  \
  15   7 

Output:

[
  [9],
  [3,15],
  [20],
  [7]
]
```

**Examples 2:**
```
Input: [3,9,8,4,0,1,7]

     3
    /\
   /  \
   9   8
  /\  /\
 /  \/  \
 4  01   7 

Output:

[
  [4],
  [9],
  [3,0,1],
  [8],
  [7]
]
```

**Examples 3:**
```
Input: [3,9,8,4,0,1,7,null,null,null,2,5] (0's right child is 2 and 1's left child is 5)

     3
    /\
   /  \
   9   8
  /\  /\
 /  \/  \
 4  01   7
    /\
   /  \
   5   2

Output:

[
  [4],
  [9,5],
  [3,0,1],
  [8,2],
  [7]
]
```

## Solution

TODO

Use BFS.

#### Code

Here is a sample solution.

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
    public List<List<Integer>> verticalOrder(TreeNode root) {
        Map<TreeNode, Integer> colMap = new HashMap<>();
        Map<Integer, List<Integer>> colLists = new HashMap<>();
        Queue<TreeNode> q = new LinkedList<>();
        if(root != null) {
            q.add(root);
            colMap.put(root, 0);
        }
        int minCol = 0;
        while(!q.isEmpty()) {
            TreeNode n = q.poll();
            int col = colMap.get(n);
            if(!colLists.containsKey(col)) colLists.put(col, new ArrayList<Integer>());
            colLists.get(col).add(n.val);
            if(n.left != null) {
                int leftCol = col-1;
                if(minCol > leftCol) minCol = leftCol;
                colMap.put(n.left,col-1);
                q.add(n.left);
            }
            if(n.right != null) {
                colMap.put(n.right,col+1);
                q.add(n.right);
            }
        }

        List<List<Integer>> results = new ArrayList<List<Integer>>();
        for(int i=minCol; colLists.containsKey(i); i++) {
            results.add(colLists.get(i));
        }
        return results;
    }
}
```

## Performance

TODO
