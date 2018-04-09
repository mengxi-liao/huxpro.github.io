---
layout:     post
title:      "Problem: Binary Tree Paths"
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
---

## Question

Given a binary tree, return all root-to-leaf paths.

For example, given the following binary tree:

```
   1
 /   \
2     3
 \
  5
```

All root-to-leaf paths are:

`["1->2->5", "1->3"]`

## Solution
TODO

#### Code
```java
class Solution {
    public List<String> binaryTreePaths(TreeNode root) {
        List<String> results = new ArrayList<>();
        List<Integer> traveler = new ArrayList<>();
        travel(traveler, results, root);

        return results;
    }

    public void travel(List<Integer> traveler, List<String> results, TreeNode root) {
        if(root == null) return;
        traveler.add(root.val);

        if(root.left == null && root.right == null) {
            results.add(convertToString(traveler));
        }
        else {
            travel(traveler, results, root.left);
            travel(traveler, results, root.right);
        }

        traveler.remove(traveler.size()-1);
    }

    public String convertToString(List<Integer> traveler) {
        if(traveler.size() == 0) return "";
        StringBuilder sb = new StringBuilder();
        sb.append(String.valueOf(traveler.get(0)));
        for(int i=1; i<traveler.size(); ++i) {
            sb.append("->").append(String.valueOf(traveler.get(i)));
        }

        return sb.toString();
    }
}
```

## Performance
TODO