---
layout:     post
title:      "Problem: Dungeon Game"
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
    - Hard
---

## Question

The demons had captured the princess (P) and imprisoned her in the bottom-right corner of a dungeon. The dungeon consists of M x N rooms laid out in a 2D grid. Our valiant knight (K) was initially positioned in the top-left room and must fight his way through the dungeon to rescue the princess.

The knight has an initial health point represented by a positive integer. If at any point his health point drops to 0 or below, he dies immediately.

Some of the rooms are guarded by demons, so the knight loses health (negative integers) upon entering these rooms; other rooms are either empty (0's) or contain magic orbs that increase the knight's health (positive integers).

In order to reach the princess as quickly as possible, the knight decides to move only rightward or downward in each step.

Write a function to determine the knight's minimum initial health so that he is able to rescue the princess.

For example, given the dungeon below, the initial health of the knight must be at least 7 if he follows the optimal path RIGHT-> RIGHT -> DOWN -> DOWN.

```
-2(K)   -3     3
-5     -10     1
10      30    -5(P)
```

**Note:**

- The knight's health has no upper bound.
- Any room can contain threats or power-ups, even the first room the knight enters and the bottom-right room where the princess is imprisoned.

## Solution
TODO

Use Dynamic Programming to search min health of the left top conner cell.

#### Code
```java
class Solution {
    public int calculateMinimumHP(int[][] dungeon) {
        int m = dungeon.length;
        if(m==0) return 0;
        int n = dungeon[0].length;
        int[][] minHealth = new int[m][n];

        //DP tip: you are searching for minHealth[0][0], not minHealth[m-1][n-1] ;)
        //
        // minHealth(current) + dungeon(current) >= minHealth(next)
        // -> minHealth(current) >= minHealth(next) - dungeon(current)
        // minHealth(current) >= 1
        //
        // minHealth(current) == max(1, minHealth(next) - dungeon(current))

        for(int i=m-1; i>=0; i--) {
            for(int j=n-1; j>=0; j--) {
                if (i == m-1 && j == n-1) {
                    minHealth[i][j] = Math.max(1, 1 - dungeon[i][j]);
                }
                else if(i==m-1) {
                    minHealth[i][j] = Math.max(1, minHealth[i][j+1] - dungeon[i][j]);
                }
                else if(j==n-1) {
                    minHealth[i][j] = Math.max(1, minHealth[i+1][j] - dungeon[i][j]);
                }
                else {
                    minHealth[i][j] = Math.max(1, Math.min(minHealth[i+1][j], minHealth[i][j+1]) - dungeon[i][j]);
                }
            }
        }

        return minHealth[0][0];
    }
}

/*
Example:
-10  1
30  -5

if at least 1 HP after get to -5. Will need 6 HP.
if at least 6 HP after get to 1 or 30,
  Will need 5 HP on 1.
  Will need 1 HP on 30.
For -1, we need to select the next cell, either 1 or 30.
As 30 needs less HP. We select 30. And it needs 1 HP, so
the HP on -10 will be 11 HP.
*/

```

## Performance
`O(mn)`
