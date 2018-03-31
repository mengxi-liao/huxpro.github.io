---
layout:     post
title:      "Problem: Number of Islands"
date:       2015-02-18 00:00:00
author:     "Marcy"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - Coding Interview
    - Coding Practice
    - Algorithms and Data Structures
    - Depth First Search
    - Medium
---

## Question

Given a 2d grid map of `'1'`s (land) and `'0'`s (water), count the number of islands. An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

**Example 1:**
```
11110
11010
11000
00000
```
Answer: 1

**Example 2:**
```
11000
11000
00100
00011
```
Answer: 3

## Solution
TODO

#### Code
```java
class Solution {
    public int numIslands(char[][] grid) {
        int lands = 0;
        if(grid.length == 0 || grid[0].length == 0) return lands;
        
        int width = grid.length;
        int height = grid[0].length;
        
        for(int i=0; i<width; i++) {
            for(int j=0; j<height; j++) {
                if(grid[i][j] == '1') {
                    traverse(i, j, grid);
                    lands ++;
                }
            }   
        }
        
        return lands;
    }
    
    public void traverse(int i, int j, char[][] grid) {
        int width = grid.length;
        int height = grid[0].length;
        if(grid[i][j] == '1') {
            // set to 0. so it is visited...
            grid[i][j] = '0';
            if(i > 0) traverse(i-1, j, grid);
            if(i < width-1) traverse(i+1,j, grid);
            if(j > 0) traverse(i, j-1, grid);
            if(j < height-1) traverse(i,j+1, grid);
        }
    }
}
```

## Performance
TODO
