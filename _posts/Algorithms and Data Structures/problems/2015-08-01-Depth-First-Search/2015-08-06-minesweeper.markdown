---
layout:     post
title:      "Problem: Minesweeper"
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

Let's play the minesweeper game!

You are given a 2D char matrix representing the game board. 'M' represents an unrevealed mine, 'E' represents an unrevealed empty square, 'B' represents a revealed blank square that has no adjacent (above, below, left, right, and all 4 diagonals) mines, digit ('1' to '8') represents how many mines are adjacent to this revealed square, and finally 'X' represents a revealed mine.

Now given the next click position (row and column indices) among all the unrevealed squares ('M' or 'E'), return the board after revealing this position according to the following rules:

1. If a mine ('M') is revealed, then the game is over - change it to 'X'.
2. If an empty square ('E') with no adjacent mines is revealed, then change it to revealed blank ('B') and all of its adjacent unrevealed squares should be revealed recursively.
3. If an empty square ('E') with at least one adjacent mine is revealed, then change it to a digit ('1' to '8') representing the number of adjacent mines.
4. Return the board when no more squares will be revealed.

**Example 1:**
```
Input: 

[['E', 'E', 'E', 'E', 'E'],
 ['E', 'E', 'M', 'E', 'E'],
 ['E', 'E', 'E', 'E', 'E'],
 ['E', 'E', 'E', 'E', 'E']]

Click : [3,0]

Output: 

[['B', '1', 'E', '1', 'B'],
 ['B', '1', 'M', '1', 'B'],
 ['B', '1', '1', '1', 'B'],
 ['B', 'B', 'B', 'B', 'B']]
```

**Example 2:**
```
Input: 

[['B', '1', 'E', '1', 'B'],
 ['B', '1', 'M', '1', 'B'],
 ['B', '1', '1', '1', 'B'],
 ['B', 'B', 'B', 'B', 'B']]

Click : [1,2]

Output: 

[['B', '1', 'E', '1', 'B'],
 ['B', '1', 'X', '1', 'B'],
 ['B', '1', '1', '1', 'B'],
 ['B', 'B', 'B', 'B', 'B']]
```

**Note:**
1. The range of the input matrix's height and width is [1,50].
2. The click position will only be an unrevealed square ('M' or 'E'), which also means the input board contains at least one clickable square.
3. The input board won't be a stage when game is over (some mines have been revealed).
4. For simplicity, not mentioned rules should be ignored in this problem. For example, you don't need to reveal all the unrevealed mines when the game is over, consider any cases that you will win the game or flag any squares.


## Solution
TODO

#### Code
```java
class Solution {
    public char[][] updateBoard(char[][] board, int[] click) {
        int x = click[0];
        int y = click[1];
        
        if(board[x][y] == 'M') {
            board[x][y] = 'X';
        }
        else {
            dfsUpdate(board, x, y);
        }
        
        
        return board;
    }
    
    private void dfsUpdate(char[][] board, int x, int y) {
        if(!valid(board,x,y) || board[x][y] != 'E') return;
        
        int[][] shifts = new int[][] {
            {-1,-1}, {-1,0}, {-1, 1}, {0,-1}, {0,1}, {1,-1}, {1,0}, {1,1}
        };
        
        int count = 0;
        for(int[] shift : shifts) {
            int nx = x + shift[0];
            int ny = y + shift[1];
            if(valid(board, nx, ny) && board[nx][ny] == 'M')
                count ++;
        }
        
        if(count == 0) {
            board[x][y] = 'B';
            for(int[] shift : shifts) {
                dfsUpdate(board, x + shift[0], y + shift[1]);
            }
        }
        else {
            board[x][y] = (char)('0' + count);
        }
    }
    
    private boolean valid(char[][] board, int x, int y) {
        return x>=0 && x<board.length && y>=0 && y<board[0].length;
    }
}
```

## Performance
TODO
