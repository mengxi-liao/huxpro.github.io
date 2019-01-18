---
layout:     post
title:      "Problem: Find Duplicate Subtrees"
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

Given a binary tree, return all duplicate subtrees. For each kind of duplicate subtrees, you only need to return the root node of any one of them.

Two trees are duplicate if they have the same structure with same node values.

**Example 1:**
```
        1
       / \
      2   3
     /   / \
    4   2   4
       /
      4
```

The following are two duplicate subtrees:

```
      2
     /
    4
```

and

```
    4
```

Therefore, you need to return above trees' root in the form of a list.


## Solution

Serialize each subtree and add it to a hashmap counter. When a serialized code appears twice, add the root to the results.

#### Code

Here is a sample solution.

```java
class Solution {
    public List<TreeNode> findDuplicateSubtrees(TreeNode root) {
        List<TreeNode> results = new ArrayList<>();
        Map<String, Integer> map = new HashMap<String, Integer>();
        preorder(root, map, results);
        return results;
    }

    public String preorder(TreeNode root, Map<String, Integer> map, List<TreeNode> results) {
        if(root == null) return "#";
        String serialized = root.val + "," +
                            preorder(root.left, map, results) + "," +
                            preorder(root.right, map, results);
        map.put(serialized, map.getOrDefault(serialized, 0)+1);
        if(map.get(serialized) == 2) results.add(root);

        return serialized;
    }
}
```

## Performance
`O(n)`
