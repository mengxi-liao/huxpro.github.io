---
layout:     post
title:      "Problem: Maximum Width of Binary Tree"
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
    - Binary Tree
    - Medium
---

## Question

Given a binary tree, write a function to get the maximum width of the given tree. The width of a tree is the maximum width among all levels. The binary tree has the same structure as a full binary tree, but some nodes are null.

The width of one level is defined as the length between the end-nodes (the leftmost and right most non-null nodes in the level, where the null nodes between the end-nodes are also counted into the length calculation.

**Example 1:**
```
Input: 

           1
         /   \
        3     2
       / \     \  
      5   3     9 

Output: 4
Explanation: The maximum width existing in the third level with the length 4 (5,3,null,9).
```

**Example 2:**
```
Input: 

          1
         /  
        3    
       / \       
      5   3     

Output: 2
Explanation: The maximum width existing in the third level with the length 2 (5,3).
```

**Example 3:**
```
Input: 

          1
         / \
        3   2 
       /        
      5      

Output: 2
Explanation: The maximum width existing in the second level with the length 2 (3,2).
```

**Example 4:**
```
Input: 

          1
         / \
        3   2
       /     \  
      5       9 
     /         \
    6           7
Output: 8
Explanation:The maximum width existing in the fourth level with the length 8 (6,null,null,null,null,null,null,7).
```

## Solution

TODO

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
    ArrayList<int[]> vlevels = new ArrayList<>();
    int max = 0;
    public int widthOfBinaryTree(TreeNode root) {
        dfs(root, 1, 0);
        return max;
    }

    public void dfs(TreeNode root, int vlevel, int hlevel) {
        if(root == null) return;
        if(hlevel == vlevels.size()) {
            vlevels.add(new int[] { vlevel, vlevel });
        }
        int[] vl = vlevels.get(hlevel);
        if(vl[0] > vlevel) vl[0] = vlevel;
        if(vl[1] < vlevel) vl[1] = vlevel;
        max = Math.max(max, vl[1] - vl[0] + 1);
        dfs(root.left, 2*vlevel, hlevel+1);
        dfs(root.right, 2*vlevel+1, hlevel+1);
    }
}
```

## Performance
O(n)