---
layout:     post
title:      "Problem: Maximal Rectangle"
date:       2015-02-18 00:00:00
author:     "Marcy"
header-img: "img/post-bg-2015.jpg"
catalog: true
category: algnote
algnote-tags:
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
        if(matrix.length == 0 || matrix[0].length == 0) return 0;
        int[] row = new int[matrix[0].length];
        
        int max = 0;
        for(int i=0; i<matrix.length; i++) {
            for(int j=0; j<matrix[0].length; j++) {
                if(matrix[i][j] == '0') {
                    row[j] = 0;
                }
                else {
                    row[j] ++;
                }
            }
            
            max = Math.max(rowMax(row), max);
        }
                            
        return max;
    }
                            
    private int rowMax(int[] row) {
        int max = 0;
        Stack<Integer> s = new Stack();
        
        for(int i=0; i<row.length; i++) {
            while(!s.isEmpty() && row[i] < row[s.peek()]) {
                int h = row[s.pop()];
                int l = s.isEmpty()? 0: s.peek()+1;
                int r = i;
                max = Math.max(h*(r-l), max);
            }
            
            s.push(i);
        }
        
        while(!s.isEmpty()) {
            int h = row[s.pop()];
            int r = row.length;
            int l = s.isEmpty()? 0: s.peek()+1;
            max = Math.max(h*(r-l), max);
        }
        
        return max;
    }
}
```

## Performance
TODO
