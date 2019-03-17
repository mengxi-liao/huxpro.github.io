---
layout:     post
title:      "Problem: Graph Valid Tree"
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
    - Union Find
    - Medium
---

## Question

Given n nodes labeled from 0 to n-1 and a list of undirected edges (each edge is a pair of nodes), write a function to check whether these edges make up a valid tree.

**Example 1:**
```
Input: n = 5, and edges = [[0,1], [0,2], [0,3], [1,4]]
Output: true
```

**Example 2:**
```
Input: n = 5, and edges = [[0,1], [1,2], [2,3], [1,3], [1,4]]
Output: false
```

## Solution

Use Union Find.

#### Code
```java
class Solution {
    public boolean validTree(int n, int[][] edges) {
        int[] roots = new int[n];
        for(int i=0; i<n; i++) roots[i] = i;
        for(int[] e:edges) {
            int r1 = find(e[0], roots);
            int r2 = find(e[1], roots);
            if(r1 == r2) return false;
            roots[r1] = r2;
        }

        for(int i=1; i<n; i++) {
            if(find(i,roots) != find(i-1,roots)) return false;
        }

        return true;
    }

    int find(int node, int[] roots) {
        while(roots[node] != node) {
            roots[node] = roots[roots[node]];
            node = roots[node];
        }

        return node;
    }
}

```

#### Performance
TODO
