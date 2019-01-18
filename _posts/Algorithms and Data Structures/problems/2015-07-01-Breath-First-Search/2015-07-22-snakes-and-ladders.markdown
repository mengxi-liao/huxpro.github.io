---
layout:     post
title:      "Problem: Snakes and Ladders"
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
    - Medium
---

## Question

On an `N x N` board, the numbers from `1` to `N*N` are written boustrophedonically starting from the bottom left of the board, and alternating direction each row.  For example, for a `6 x 6` board, the numbers are written as follow example `1`.

You start on square 1 of the board (which is always in the last row and first column).  Each move, starting from square x, consists of the following:

You choose a destination square S with number `x+1`, `x+2`, `x+3`, `x+4`, `x+5`, or `x+6`, provided this number is `<= N*N`.
(This choice simulates the result of a standard 6-sided die roll: ie., there are always at most 6 destinations.)
If `S` has a snake or ladder, you move to the destination of that snake or ladder.  Otherwise, you move to `S`.
A board square on row r and column c has a "snake or ladder" if `board[r][c] != -1`.  The destination of that snake or ladder is `board[r][c]`.

Note that you only take a snake or ladder at most once per move: if the destination to a snake or ladder is the start of another snake or ladder, you do not continue moving.  (For example, if the board is ``[[4,-1],[-1,3]]``, and on the first move your destination square is `2`, then you finish your first move at `3`, because you do not continue moving to `4`.)

Return the least number of moves required to reach square `N*N`.  If it is not possible, return `-1`.

**Example 1:**

```
Input: [
[-1,-1,-1,-1,-1,-1],
[-1,-1,-1,-1,-1,-1],
[-1,-1,-1,-1,-1,-1],
[-1,35,-1,-1,13,-1],
[-1,-1,-1,-1,-1,-1],
[-1,15,-1,-1,-1,-1]]
```

Output: 4

Explanation:

- At the beginning, you start at square 1 [at row 5, column 0].
- You decide to move to square 2, and must take the ladder to square 15.
- You then decide to move to square 17 (row 3, column 5), and must take the snake to square 13.
- You then decide to move to square 14, and must take the ladder to square 35.
- You then decide to move to square 36, ending the game.
- It can be shown that you need at least 4 moves to reach the N*N-th square, so the answer is 4.

**Note:**

- 2 <= `board.length` = `board[0].length` <= 20
- `board[i][j]` is between 1 and N*N or is equal to -1.
- The board square with number 1 has no snake or ladder.
- The board square with number N*N has no snake or ladder.

- Only one letter can be changed at a time.
- Each transformed word must exist in the word list. Note that beginWord is not a transformed word.

For example,

Given:
beginWord = `"hit"`
endWord = `"cog"`
wordList = `["hot","dot","dog","lot","log","cog"]`
As one shortest transformation is `"hit" -> "hot" -> "dot" -> "dog" -> "cog"`,
return its length `5`.

Note:
- Return 0 if there is no such transformation sequence.
- All words have the same length.
- All words contain only lowercase alphabetic characters.
- You may assume no duplicates in the word list.
- You may assume beginWord and endWord are non-empty and are not the same.

## Solution

Use BFS

#### Code

Here is a sample solution.

```java
class Solution {
    public int snakesAndLadders(int[][] board) {
        if(board.length == 0 || board[0].length == 0) return 0;
        int destination = board.length * board[0].length;
        Set<Integer> visited = new HashSet<>();

        Queue<Integer> q = new LinkedList<Integer>();
        q.add(1);
        visited.add(1);

        int level = 0;
        while(!q.isEmpty()) {
            int size = q.size();
            for(int i=0; i<size; i++) {
                int x = q.poll();
                if(x == destination) return level;
                for(int j=1; j<=6 && x+j<=destination; j++) {
                    int adj = find(x+j, board);
                    if(!visited.contains(adj)) {
                        visited.add(adj);
                        q.offer(adj);
                    }
                }

            }

            level ++;
        }

        return -1;
    }

    private int find(int x, int[][] board) {
        int idx = x-1;
        int i = board.length - 1 - idx / board[0].length;
        int j;
        if((board.length - i) % 2 == 1) {
            j = idx % board[0].length;
        }
        else {
            j = board[0].length - 1 - idx % board[0].length;
        }

        if(board[i][j] != -1) {
            return board[i][j];
        }
        else {
            return x;
        }
    }
}
```

## Performance

TODO
