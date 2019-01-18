---
layout:     post
title:      "Problem: Pacific Atlantic Water Flow"
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
    - Medium
---

## Question

Given an m x n matrix of non-negative integers representing the height of each unit cell in a continent, the "Pacific ocean" touches the left and top edges of the matrix and the "Atlantic ocean" touches the right and bottom edges.

Water can only flow in four directions (up, down, left, or right) from a cell to another one with height equal or lower.

Find the list of grid coordinates where water can flow to both the Pacific and Atlantic ocean.

**Note:**
1. The order of returned grid coordinates does not matter.
2. Both m and n are less than 150.

**Example:**
```
Given the following 5x5 matrix:

  Pacific ~   ~   ~   ~   ~ 
       ~  1   2   2   3  (5) *
       ~  3   2   3  (4) (4) *
       ~  2   4  (5)  3   1  *
       ~ (6) (7)  1   4   5  *
       ~ (5)  1   1   2   4  *
          *   *   *   *   * Atlantic

Return:

[[0, 4], [1, 3], [1, 4], [2, 2], [3, 0], [3, 1], [4, 0]] (positions with parentheses in above matrix).
```

#### Code
```java
class Solution {
    public List<int[]> pacificAtlantic(int[][] matrix) {
        List<int[]> results = new ArrayList<>();
        if(matrix.length == 0 || matrix[0].length == 0) return results;
        int[][] cache = new int[matrix.length][matrix[0].length];
        for(int j=0; j<matrix[0].length; j++) dfs(matrix, cache, 0, j, results, -1);
        for(int i=0; i<matrix.length; i++) dfs(matrix, cache, i, 0, results, -1);
        for(int j=0; j<matrix[0].length; j++) dfs(matrix, cache, matrix.length-1, j, results, 1);
        for(int i=0; i<matrix.length; i++) dfs(matrix, cache, i, matrix[0].length-1, results, 1);
        return results;
    }

    private void dfs(int[][] matrix, int[][] cache, int i, int j, List<int[]> results, int mark) {
        if(cache[i][j] == mark) return;
        if(cache[i][j] != 0) results.add(new int[]{i, j});
        cache[i][j] = mark;
        if(i>0 && matrix[i-1][j] >= matrix[i][j]) dfs(matrix, cache, i-1, j, results, mark);
        if(i<matrix.length-1 && matrix[i+1][j] >= matrix[i][j]) dfs(matrix, cache, i+1, j, results, mark);
        if(j>0 && matrix[i][j-1] >= matrix[i][j]) dfs(matrix, cache, i, j-1, results, mark);
        if(j<matrix[0].length-1 && matrix[i][j+1] >= matrix[i][j]) dfs(matrix, cache, i, j+1, results, mark);
    }
}
```
