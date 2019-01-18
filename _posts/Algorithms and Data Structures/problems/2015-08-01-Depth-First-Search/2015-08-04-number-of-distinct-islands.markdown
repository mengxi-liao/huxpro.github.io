---
layout:     post
title:      "Problem: Number of Distinct Islands"
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

Given a non-empty 2D array grid of 0's and 1's, an island is a group of 1's (representing land) connected 4-directionally (horizontal or vertical.) You may assume all four edges of the grid are surrounded by water.

Count the number of distinct islands. An island is considered to be the same as another if and only if one island can be translated (and not rotated or reflected) to equal the other.

**Example 1:**
```
11000
11000
00011
00011
```
Given the above grid map, return 1.

**Example 2:**
```
11011
10000
00001
11011
```
Given the above grid map, return 3.

**Notice that:**
```
11
1
```
and
```
 1
11
```
are considered different island shapes, because we do not consider reflection / rotation.

**Note:** The length of each dimension in the given grid does not exceed 50.

## Solution
Similar to solving `number of islands`. Here we need to create a unique code for the shape of the island. A dfs traverse log will be a good fit.

#### Code
```java
class Solution {
    public int numDistinctIslands(int[][] grid) {
        if(grid.length == 0 || grid[0].length == 0) return 0;
        Set<String> set = new HashSet<>();
        for(int i=0; i<grid.length; i++) {
            for(int j=0; j<grid[0].length; j++) {
                if(grid[i][j] == 1) {
                    StringBuilder code = new StringBuilder();
                    dfs(grid, i, j, code, 'o');
                    set.add(code.toString());
                }
            }
        }

        return set.size();
    }

    private void dfs(int[][] grid, int i, int j, StringBuilder code, char dir) {
        if(i<0 || i>=grid.length || j<0 || j>=grid[0].length || grid[i][j] == 0) return;
        code.append(dir);
        grid[i][j] = 0;
        dfs(grid, i-1, j, code, 'u');
        dfs(grid, i+1, j, code, 'd');
        dfs(grid, i, j-1, code, 'l');
        dfs(grid, i, j+1, code, 'r');

        // when it hits the wall, we need to backtrace. otherwise
        // 1 1
        // 1
        // and
        // 1 1
        //   1
        // might have the same code "ord"
        // with the back record
        // they are "orbdb" and "ordbb"
        code.append('b');
    }
}
```

## Performance
TODO
