---
layout:     post
title:      "Problem: Set Matrix Zeros"
date:       2015-02-18 00:00:00
author:     "Marcy"
header-img: "img/post-bg-2015.jpg"
catalog: true
category: algnote
algnote-tags:
    - Coding Interview
    - Coding Practice
    - Algorithms and Data Structures
    - Array
    - Medium
---

## Question

Given a m x n matrix, if an element is 0, set its entire row and column to 0. Do it **in-place**.

## Solution

The idea is simple: Store states of each row in the first of that row, and store states of each column in the first of that column. Because the state of the first row, `row0`, and the state of the first column, `col0`, would occupy the same cell, let's leave the cell be the state of `row0`, and use another variable `firstColHasZero` for `col0`. In the first phase, use matrix elements to set states in a top-down way. In the second phase, use states to set matrix elements in a bottom-up way.
#### Code

Here is a sample solution.

```java
public class Solution {
    public void setZeroes(int[][] matrix) {

        boolean firstColHasZero = false;
        // why we don't need firstRowHasZero?
        // it's matrix[0][0]

        int rows = matrix.length;
        int cols = matrix[0].length;

        for (int i = 0; i < rows; i++) {
            if (matrix[i][0] == 0)
                firstColHasZero = true;

            for (int j = 1; j < cols; j++)
                if (matrix[i][j] == 0)
                    matrix[i][0] = matrix[0][j] = 0;
        }

        // check bottom-up to make sure we don't
        // pollute the first row and first col
        for (int i = rows - 1; i >= 0; i--) {

            for (int j = cols - 1; j >= 1; j--)
                if (matrix[i][0] == 0 || matrix[0][j] == 0)
                    matrix[i][j] = 0;

            if (firstColHasZero)
                matrix[i][0] = 0;
        }
    }
}
```

## Solution

An easier to understand version. Use two variables `firstRowHasZero` and `firstColHasZero` to mark if the first row has zero and if the first col has zero. Use the first row and first col to mark if `matrix[row][col]` is zero. When setting zeros, set `matrix[1-rows][1-cols]` first based on if `matrix[row][0]` or `matrix[0][col]` is zero. Then set `matrix[0][col]` based on if 
`firstRowHasZero` and set `matrix[row][0]` based on `firstColHasZero`.

```java
class Solution {
    public void setZeroes(int[][] matrix) {
        boolean firstRowHasZero = false;
        boolean firstColHasZero = false;
        
        for(int r=0; r<matrix.length; r++) {
            for(int c=0; c<matrix[r].length; c++) {
                if(matrix[r][c] == 0) {
                    if(r==0) firstRowHasZero = true;
                    if(c==0) firstColHasZero = true;
                    matrix[0][c] = 0;
                    matrix[r][0] = 0;
                }
            }
        }
        
        for(int r=1; r<matrix.length; r++) {
            for(int c=1; c<matrix[r].length; c++) {
                if(matrix[r][0] == 0 || matrix[0][c] == 0) {
                    matrix[r][c] = 0;
                }
            }
        }
        
        for(int r=0; r<matrix.length; r++) {
            if(firstColHasZero) matrix[r][0] = 0;
        }
        
        for(int c=0; c<matrix[0].length; c++) {
            if(firstRowHasZero) matrix[0][c] = 0;
        }
    }
}
```

## Performance

The algorithm runs through the matrix twice. The time complexity is O(m x n). Only constant extra space is used.
