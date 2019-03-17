---
layout:     post
title:      "Problem: Longest Increasing Path in a Matrix"
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
    - Breath First Search
    - Hard
---

## Question

Given an integer matrix, find the length of the longest increasing path.

From each cell, you can either move to four directions: left, right, up or down. You may NOT move diagonally or move outside of the boundary (i.e. wrap-around is not allowed).

Example 1:
```
Input: nums = 
[
  [9,9,4],
  [6,6,8],
  [2,1,1]
] 
Output: 4 
Explanation: The longest increasing path is [1, 2, 6, 9].
```

#### Solution

DFS + Cache

#### Code
```java
class Solution {
    public int longestIncreasingPath(int[][] matrix) {
        if(matrix.length == 0 || matrix[0].length == 0) return 0;
        int[][] cache = new int[matrix.length][matrix[0].length];
        int max = 0;
        for(int i=0; i<matrix.length; i++) {
            for(int j=0; j<matrix[0].length; j++) {
                max = Math.max(max, dfs(matrix, cache, i, j));
            }
        }
        
        return max;
    }
    
    public int dfs(int[][] matrix, int[][] cache, int i, int j) {
        if(cache[i][j] != 0) return cache[i][j];
        
        int max = 0;
        if(i<matrix.length-1 && matrix[i+1][j] > matrix[i][j])
            max = Math.max(max, dfs(matrix, cache, i+1, j));
        if(i>0 && matrix[i-1][j] > matrix[i][j])
            max = Math.max(max, dfs(matrix, cache, i-1, j));
        if(j<matrix[0].length-1 && matrix[i][j+1] > matrix[i][j])
            max = Math.max(max, dfs(matrix, cache, i, j+1));
        if(j>0 && matrix[i][j-1] > matrix[i][j])
            max = Math.max(max, dfs(matrix, cache, i, j-1));
        
        cache[i][j] = 1 + max;
        
        return cache[i][j];
    }
}
```
