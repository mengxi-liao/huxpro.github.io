---
layout:     post
title:      "Problem: Number of Islands II"
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
    - Union Find
    - Hard
---

## Question

A 2d grid map of m rows and n columns is initially filled with water. We may perform an addLand operation which turns the water at position (row, col) into a land. Given a list of positions to operate, count the number of islands after each addLand operation. An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

**Example:**
```
Input: m = 3, n = 3, positions = [[0,0], [0,1], [1,2], [2,1]]
Output: [1,1,2,3]
```

**Explanation:**

Initially, the 2d grid grid is filled with water. (Assume 0 represents water and 1 represents land).

```
0 0 0
0 0 0
0 0 0
```

Operation #1: addLand(0, 0) turns the water at `grid[0][0]` into a land.

```
1 0 0
0 0 0   Number of islands = 1
0 0 0
```

Operation #2: addLand(0, 1) turns the water at `grid[0][1]` into a land.

```
1 1 0
0 0 0   Number of islands = 1
0 0 0
```

Operation #3: addLand(1, 2) turns the water at `grid[1][2]` into a land.

```
1 1 0
0 0 1   Number of islands = 2
0 0 0
```

Operation #4: addLand(2, 1) turns the water at `grid[2][1]` into a land.

```
1 1 0
0 0 1   Number of islands = 3
0 1 0
```

**Follow up:**
Can you do it in time complexity O(k log mn), where k is the length of the positions?

## Solution 1

Use Union Find.

#### Code
```java
class Solution {
    public List<Integer> numIslands2(int m, int n, int[][] positions) {
        int[] roots = new int[positions.length];
        List<Integer> output = new ArrayList<>();
        int count = 0;
        int[][] map = new int[m][n];
        for(int i=0; i<roots.length; i++) roots[i] = i+1;
        for(int i=0; i<positions.length; i++) {
            int x = positions[i][0];
            int y = positions[i][1];
            map[x][y] = i+1;
            Set<Integer> adjRoots = new HashSet<Integer>();
            if(x>0 && map[x-1][y] != 0) adjRoots.add(findRoot(roots, map[x-1][y]));
            if(x<m-1 && map[x+1][y] != 0) adjRoots.add(findRoot(roots, map[x+1][y]));
            if(y>0 && map[x][y-1] != 0) adjRoots.add(findRoot(roots, map[x][y-1]));
            if(y<n-1 && map[x][y+1] != 0) adjRoots.add(findRoot(roots, map[x][y+1]));

            for(int adjRoot:adjRoots) {
                roots[adjRoot-1] = i+1;
            }

            count += 1;
            count -= adjRoots.size();
            output.add(count);
        }

        return output;
    }

    private int findRoot(int[] roots, int v) {
        while(roots[v-1] != v) {
            v = roots[v-1];
            roots[v-1] = roots[roots[v-1]-1];
        }
        return v;
    }
}

```

#### Performance
TODO
