---
layout:     post
title:      "Problem: Word Search"
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

Given a 2D board and a word, find if the word exists in the grid.

The word can be constructed from letters of sequentially adjacent cell, where "adjacent" cells are those horizontally or vertically neighboring. The same letter cell may not be used more than once.

For example,
Given **board** =

```
[
  ['A','B','C','E'],
  ['S','F','C','S'],
  ['A','D','E','E']
]
```
**word** = `"ABCCED"`, -> returns `true`,
**word** = `"SEE"`, -> returns `true`,
**word** = `"ABCB"`, -> returns `false`.


## Solution
TODO

#### Code
```java
class Solution {
    public boolean exist(char[][] board, String word) {
        for(int r=0; r<board.length; r++) {
            for(int c=0; c<board[0].length; c++) {
                if(check(board, r, c, word, 0)) {
                    return true;
                }
            }
        }
        
        return false;
    }
    
    private boolean check(char[][] board, int r, int c, String word, int idx) {
        if(idx == word.length()) return true;
        if(r<0 || r>=board.length || c<0 || c>=board[0].length || 
          board[r][c] != word.charAt(idx)) {
            return false;
        }
        
        char origin = board[r][c];
        board[r][c] = '0';
        boolean found = check(board, r+1, c, word, idx+1) 
            || check(board, r, c+1, word, idx+1)
            || check(board, r-1, c, word, idx+1)
            || check(board, r, c-1, word, idx+1);
        board[r][c] = origin;
        
        return found;
    }
}
```

## Performance
TODO
