---
layout:     post
title:      "Problem: Maximal Rectangle"
date:       2015-02-18 00:00:00
author:     "Marcy"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - Coding Interview
    - Coding Practice
    - Algorithms and Data Structures
    - Stack
    - Hard
---

## Question

Given a 2D binary matrix filled with 0's and 1's, find the largest rectangle containing only 1's and return its area.

For example, given the following matrix:

```
1 0 1 0 0
1 0 1 1 1
1 1 1 1 1
1 0 0 1 0
```

Return 6.

## Solution
TODO

#### Code
```java
class Solution {
    public int maximalRectangle(char[][] matrix) {
        if(matrix.length == 0) return 0;
        
        int maxSize = 0;
        int[] heights = new int[matrix[0].length];
        for(int i=0; i<matrix.length; i++) {
            for(int j=0; j<heights.length; j++) {
                if(matrix[i][j] == '0') heights[j] = 0;
                else heights[j]++;
            }
            maxSize = Math.max(maxSize, rowMax(heights));
        }
        return maxSize;
    }
    
    int rowMax(int[] heights) {
        int[] stack = new int[heights.length];
        int top = -1;
        int maxArea = 0;
        for(int i=0; i<heights.length; i++) {
            while(top >= 0 && heights[stack[top]] >= heights[i]) {
                int h = heights[stack[top--]];
                int left = top>=0 ? stack[top]: -1;
                
                maxArea = Math.max(maxArea, h * (i - left - 1));
            }
            stack[++top] = i;
        }
        
        while(top >= 0) {
            int h = heights[stack[top--]];
            int left = top>=0 ? stack[top]: -1;
            maxArea = Math.max(maxArea, h * (heights.length - left - 1));
        }
        
        return maxArea;
    }
}
```

## Performance
TODO
