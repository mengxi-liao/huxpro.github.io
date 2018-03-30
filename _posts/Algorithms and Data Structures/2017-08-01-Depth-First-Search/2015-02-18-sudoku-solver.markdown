---
layout:     post
title:      "Problem: Sudoku Solver"
date:       2015-02-18 00:00:00
author:     "Marcy"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - Coding Interview
    - Coding Practice
    - Algorithms and Data Structures
    - Depth First Search
---

## Question

Write a program to solve a Sudoku puzzle by filling the empty cells.

Empty cells are indicated by the character '.'.

You may assume that there will be only one unique solution.

## Solution
TODO

#### Code
```java
class Solution {
    public void solveSudoku(char[][] board) {
        solve(board);
    }

    private boolean solve(char[][] board) {
        for(int row=0; row<board.length; row++) {
            for(int col=0; col<board[0].length; col++) {
                if(board[row][col] != '.') continue;
                for(char c='1'; c<='9'; c++) {
                    if(isValid(board, row, col, c)) {
                        board[row][col] = c;
                        if(solve(board)) {
                            return true;
                        }

                        board[row][col] = '.';
                    }
                }

                // this means this '.' can not be filled, tried 1-9 already
                return false;
            }
        }

        // this means every '.' is filled. It happen when a solved board is input.
        return true;
    }

    private boolean isValid(char[][] board, int row, int col, char c) {
        int rowStart = 3 * (row / 3);
        int colStart = 3 * (col / 3);
        for (int i = 0; i < 9; i++) {
            if (board[row][i] != '.' && board[row][i] == c) {
                return false;
            }
            if (board[i][col] != '.' && board[i][col] == c) {
                return false;
            }
            if (board[rowStart + i / 3][colStart + i % 3] != '.' &&
                board[rowStart + i / 3][colStart+ i % 3] == c) {
                return false;
            }
        }
        return true;
    }
}
```

## Performance
TODO