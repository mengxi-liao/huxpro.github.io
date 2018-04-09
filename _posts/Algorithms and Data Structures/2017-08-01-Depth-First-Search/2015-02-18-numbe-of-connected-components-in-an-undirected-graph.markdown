---
layout:     post
title:      "Problem: Number of Connected Components in an Undirected Graph"
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

Given `n` nodes labeled from 0 to `n - 1` and a list of undirected edges (each edge is a pair of nodes), write a function to find the number of connected components in an undirected graph.

**Example 1:**

```
     0          3
     |          |
     1 --- 2    4
```
Given `n = 5` and `edges = [[0, 1], [1, 2], [3, 4]]`, return `2`.

**Example 2:**

```
     0           4
     |           |
     1 --- 2 --- 3
```
Given `n = 5` and `edges = [[0, 1], [1, 2], [2, 3], [3, 4]]`, return `1`.

**Note:**
You can assume that no duplicate edges will appear in `edges`. Since all edges are undirected, `[0, 1]` is the same as `[1, 0]` and thus will not appear together in `edges`.

## Solution
TODO

#### Code
```java
class Solution {
    public int countComponents(int n, int[][] edges) {
        int[] roots = new int[n];
        for(int i=0; i<roots.length; i++) {
            roots[i] = i;
        }
        
        int count = n;
        
        for(int[] e : edges) {
            int root1 = findRoot(roots, e[0]);
            int root2 = findRoot(roots, e[1]);
            if(root1 != root2) {
                count--;
                roots[root1] = root2;
            }
        }
        
        return count;
    }
    
    private int findRoot(int[] roots, int idx) {
        while(roots[idx] != idx) {
            roots[idx] = roots[roots[idx]];
            idx = roots[idx];
        }
        
        return idx;
    }
}

```

## Performance
TODO