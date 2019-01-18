---
layout:     post
title:      "Problem: Making A Large Island"
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

In a 2D grid of 0s and 1s, we change at most one 0 to a 1.

After, what is the size of the largest island? (An island is a 4-directionally connected group of 1s).

**Example 1:**
```
Input: [[1, 0], [0, 1]]
Output: 3
Explanation: Change one 0 to 1 and connect two 1s, then we get an island with area = 3.
```
**Example 2:**
```
Input: [[1, 1], [1, 0]]
Output: 4
Explanation: Change the 0 to 1 and make the island bigger, only one island with area = 4.
```
**Example 3:**
```
Input: [[1, 1], [1, 1]]
Output: 4
Explanation: Can't change any 0 to 1, only one island with area = 4.
```

## Solution
TODO

#### Code
```java
class Solution {
    public int largestIsland(int[][] grid) {
        if(grid.length == 0 || grid[0].length == 0) return 0;

        Map<Integer, Integer> areaMap = new HashMap<>();
        int maxArea = 0;
        int flag = -1;
        List<int[]> zeroList = new ArrayList<>();
        for(int i=0; i<grid.length; i++) {
            for(int j=0; j<grid[0].length; j++) {
                if(grid[i][j] == 1) {
                    int area = dfs(grid, i, j, flag);
                    maxArea = Math.max(maxArea, area);
                    areaMap.put(flag, area);
                    flag--;
                }
                else if((grid[i][j] == 0)){
                    zeroList.add(new int[]{i, j});
                }
            }
        }

        for(int[] point: zeroList) {
            int i=point[0];
            int j=point[1];
            int area = 1;
            Set<Integer> set = new HashSet<>();
            set.add(getFlag(grid, i-1, j));
            set.add(getFlag(grid, i+1, j));
            set.add(getFlag(grid, i, j-1));
            set.add(getFlag(grid, i, j+1));
            for(int f: set) area += areaMap.getOrDefault(f, 0);
            maxArea = Math.max(maxArea, area);
        }

        return maxArea;


    }

    private int dfs(int[][] grid, int i, int j, int flag) {
        if(i<0 || i>=grid.length || j<0 || j>=grid[0].length) return 0;
        if(grid[i][j] != 1) return 0;

        int area = 1;
        grid[i][j] = flag;
        area += dfs(grid, i+1, j, flag);
        area += dfs(grid, i-1, j, flag);
        area += dfs(grid, i, j+1, flag);
        area += dfs(grid, i, j-1, flag);

        return area;
    }

    private int getFlag(int[][] grid, int i, int j) {
        if(i<0 || i>=grid.length || j<0 || j>=grid[0].length) return 0;
        if(grid[i][j] == 0) return 0;
        return grid[i][j];
    }
}
```

## Performance
O(m^n)
