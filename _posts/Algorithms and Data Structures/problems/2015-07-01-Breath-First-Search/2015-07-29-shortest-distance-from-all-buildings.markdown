---
layout:     post
title:      "Problem: Shortest Distance from All Buildings"
date:       2015-02-18 00:00:00
author:     "Marcy"
header-img: "img/post-bg-2015.jpg"
catalog: true
category: algnote
algnote-tags:
    - Coding Interview
    - Coding Practice
    - Algorithms and Data Structures
    - Breadth First Search
    - Hard
---

## Question

You want to build a house on an empty land which reaches all buildings in the shortest amount of distance. You can only move up, down, left and right. You are given a 2D grid of values 0, 1 or 2, where:

- Each 0 marks an empty land which you can pass by freely.
- Each 1 marks a building which you cannot pass through.
- Each 2 marks an obstacle which you cannot pass through.

**Example:**
```
Input: [[1,0,2,0,1],[0,0,0,0,0],[0,0,1,0,0]]

1 - 0 - 2 - 0 - 1
|   |   |   |   |
0 - 0 - 0 - 0 - 0
|   |   |   |   |
0 - 0 - 1 - 0 - 0

Output: 7 

Explanation: Given three buildings at (0,0), (0,4), (2,2), and an obstacle at (0,2),
             the point (1,2) is an ideal empty land to build a house, as the total 
             travel distance of 3+3+1=7 is minimal. So return 7.
```

**Note:**
There will be at least one building. If it is not possible to build such house according to the above rules, return -1.

## Solution

Use bfs to keep track of the distance to all the empty lands for each building.

#### Code

Here is a sample solution.

```java
class Solution {
    public int shortestDistance(int[][] grid) {
        if (grid.length == 0) {
            return -1;
        }

        int row = grid.length;
        int col = grid[0].length;
        int[][] dp = new int[row][col];
        int flag = 0;
        int ret = -1;
        for (int i = 0; i < grid.length; ++i) {
            for (int j = 0; j < grid[i].length; ++j) {
                if (grid[i][j] == 1) {
                    ret = bfs(grid, i, j, flag, dp);
                    --flag;
                    // Use a flag to track the current path
                    // so we don't need a visited hash map
                }
            }
        }

        return ret;
    }

    public int bfs(int[][] grid, int r, int c, int flag, int[][] dp) {
        int ret = Integer.MAX_VALUE;

        Queue<int[]> q = new LinkedList<int[]>();
        int row = grid.length;
        int col = grid[r].length;
        q.add(new int[]{r * col + c, 0});
        while (!q.isEmpty()) {
            int[] node = q.poll();
            int index = node[0];
            int val = node[1];
            int i = index / col;
            int j = index % col;
            int[][] shifts = new int[][]{ {-1,0}, {1,0}, {0,-1}, {0,1} };
            for(int[] shift: shifts) {
                int x = i + shift[0];
                int y = j + shift[1];
                if (x < row && x >=0 && y < col && y >= 0 && grid[x][y] == flag) {
                    dp[x][y] += val + 1;
                    --grid[x][y];
                    // Point to the next building
                    ret = Math.min(ret, dp[x][y]);
                    q.add(new int[]{x * col + y, val + 1});
                }
            }
        }
        return ret == Integer.MAX_VALUE ? -1 : ret;
    }
}
```

## Performance

O(kmn) and no extra space. (k is the number of buildings, m and n are the width and height of the grid).
