---
layout:     post
title:      "Problem: Unique Paths II"
date:       2015-02-18 00:00:00
author:     "Marcy"
header-img: "img/post-bg-2015.jpg"
catalog: true
category: algnote
algnote-tags:
    - Coding Interview
    - Coding Practice
    - Algorithms and Data Structures
    - Dynamic Programming
    - Easy
---

## Question

A robot is located at the top-left corner of a m x n grid (marked 'Start' in the diagram below).

The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid.

Now consider if some obstacles are added to the grids. How many unique paths would there be?

An obstacle and empty space is marked as 1 and 0 respectively in the grid.

Note: m and n will be at most 100.
**Example 1:**
```
Input:
[
  [0,0,0],
  [0,1,0],
  [0,0,0]
]
```

Output: 2

Explanation:

There is one obstacle in the middle of the 3x3 grid above.

There are two ways to reach the bottom-right corner:
- Right -> Right -> Down -> Down
- Down -> Down -> Right -> Right

## Solution
TODO

#### Code
```java
class Solution {
    public int uniquePathsWithObstacles(int[][] obstacleGrid) {
        if(obstacleGrid.length == 0 || obstacleGrid[0].length == 0)
            return 0;
        int cache[] = new int[obstacleGrid[0].length];
        cache[0] = 1;
        for(int i=0; i<obstacleGrid.length; i++) {
            for(int j=0; j<obstacleGrid[0].length; j++) {
                if(obstacleGrid[i][j] == 1) {
                    cache[j] = 0;
                }
                else if(j==0) {
                    cache[j] = cache[j];
                }
                else {
                    cache[j] = cache[j] + cache[j-1];
                }
            }
        }
        
        return cache[cache.length-1];
    }
}
```

## Performance
TODO
