---
layout:     post
title:      "Problem: Path Sum III"
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

You are given a binary tree in which each node contains an integer value.

Find the number of paths that sum to a given value.

The path does not need to start or end at the root or a leaf, but it must go downwards (traveling only from parent nodes to child nodes).

The tree has no more than 1,000 nodes and the values are in the range -1,000,000 to 1,000,000.

**Example:**
```
root = [10,5,-3,3,2,null,11,3,-2,null,1], sum = 8

      10
     /  \
    5   -3
   / \    \
  3   2   11
 / \   \
3  -2   1

Return 3. The paths that sum to 8 are:

1.  5 -> 3
2.  5 -> 2 -> 1
3. -3 -> 11
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
    public int pathSum(TreeNode root, int sum) {
        // path sum start from all nodes below root
        if(root == null) return 0;
        return pathSum(root.left, sum) + 
               pathSum(root.right, sum) + 
               pathSumFrom(root, sum);
    }

    public int pathSumFrom(TreeNode root, int sum) {
        // path sum start from the specific node
        if(root == null) return 0;
        int count = 0;
        if(root.val == sum) count++;
        count += pathSumFrom(root.left, sum - root.val);
        count += pathSumFrom(root.right, sum - root.val);
        return count;
    }
}
```

```java
class Solution {
    int count = 0;
    public int pathSum(TreeNode root, int sum) {
        dfs(root, sum);
        return count;
    }
    
    private List<Integer> dfs(TreeNode root, int sum) {
        List<Integer> results = new ArrayList<>();
        if(root == null) return results;
        int val = root.val;
        List<Integer> left = dfs(root.left, sum);
        List<Integer> right = dfs(root.right, sum);
        results.add(val);
        for(int v: left) results.add(v+val);
        for(int v: right) results.add(v+val);
        for(int v: results) if(v == sum) count++;
        
        return results;
    }
}
```

## Performance
O(number of nodes)
