---
layout:     post
title:      "Problem: Unique Paths"
date:       2015-02-18 00:00:00
author:     "Marcy"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - Coding Interview
    - Coding Practice
    - Algorithms and Data Structures
    - Dynamic Programming
---

## Question

A robot is located at the top-left corner of a m x n grid (marked 'Start' in the diagram below).

The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid.

How many possible unique paths are there?

Note: m and n will be at most 100.

## Solution
TODO

#### Code
```java
public class Solution {
    public int uniquePaths(int m, int n) {
        int[] cache = new int[m];
        
        for(int j=0; j<n; j++) {
            for(int i=0; i<m; i++)
                if(i==0 || j==0)
                    cache[i] = 1;
                else
                    cache[i] = cache[i-1] + cache[i];
            }
        
        return cache[m-1];
    }
}
```

## Performance
TODO