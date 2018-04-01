---
layout:     post
title:      "Problem: Minimum Path Sum"
date:       2015-02-18 00:00:00
author:     "Marcy"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - Coding Interview
    - Coding Practice
    - Algorithms and Data Structures
    - Dynamic Programming
    - Medium
---

## Question

Given a m x n grid filled with non-negative numbers, find a path from top left to bottom right which minimizes the sum of all numbers along its path.

**Note:** You can only move either down or right at any point in time.

**Example 1:**

```
[[1,3,1],
 [1,5,1],
 [4,2,1]]
```
Given the above grid map, return `7`. Because the path `1→3→1→1→1` minimizes the sum.


## Solution
TODO

#### Code
```java
 class Solution {
    public int minPathSum(int[][] grid) {
        if(grid.length == 0 || grid[0].length == 0) return 0;
        int[] cache = grid[0];
        
        for(int i=0; i<grid.length; i++) {
            for(int j=0; j<grid[0].length; j++) {
                if(i==0 && j==0) cache[j] = grid[0][0];
                else if(i==0) cache[j] = cache[j-1] + grid[i][j];
                else if(j==0) cache[j] = cache[j] + grid[i][j];
                else cache[j] = Math.min(cache[j], cache[j-1]) + grid[i][j];
            }
        }
        
        return cache[grid[0].length-1];
    }
}
```

## Performance
TODO
