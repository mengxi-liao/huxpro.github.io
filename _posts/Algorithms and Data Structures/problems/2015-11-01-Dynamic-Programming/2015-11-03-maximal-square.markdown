---
layout:     post
title:      "Problem: Maximal Square"
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
    - Medium
---

## Question

Given a 2D binary matrix filled with 0's and 1's, find the largest square containing only 1's and return its area.

**Example:**
```
Input:

1 0 1 0 0
1 0 1 1 1
1 1 1 1 1
1 0 0 1 0

Output: 4
```
## Solution
TODO

#### Code
```java
class Solution {
    public int maximalSquare(char[][] matrix) {
        if(matrix.length == 0 || matrix[0].length == 0) return 0;
        int max = 0;
        int[][] cache = new int[matrix.length][matrix[0].length];

        for(int i=0; i<matrix.length; i++) {
            for(int j=0; j<matrix[0].length; j++) {
                if(matrix[i][j] == '1') {
                    if(i==0 || j==0) {
                        cache[i][j] = 1;
                    }
                    else {
                        cache[i][j] = Math.min(cache[i-1][j-1], cache[i-1][j]);
                        cache[i][j] = Math.min(cache[i][j], cache[i][j-1]) + 1;
                    }
                    max = Math.max(cache[i][j]*cache[i][j], max);
                }
            }
        }

        return max;
    }
}
```

## Performance
TODO
