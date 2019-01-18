---
layout:     post
title:      "Problem: Coin Change 2"
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

You are given coins of different denominations and a total amount of money. Write a function to compute the number of combinations that make up that amount. You may assume that you have infinite number of each kind of coin.

**Example 1:**
```
Input: amount = 5, coins = [1, 2, 5]
Output: 4
Explanation: there are four ways to make up the amount:
5=5
5=2+2+1
5=2+1+1+1
5=1+1+1+1+1
```

**Example 2:**
```
Input: amount = 3, coins = [2]
Output: 0
Explanation: the amount of 3 cannot be made up just with coins of 2.
```

**Example 3:**
```
Input: amount = 10, coins = [10]
Output: 1
```

## Solution I
Use dynamic programming

#### Code
```java
class Solution {
    public int change(int amount, int[] coins) {
        int[][] cache = new int[coins.length+1][amount+1];
        cache[0][0] = 1;
        for(int a=0; a<=amount; a++) {
            for(int c=0; c<=coins.length; c++) {
                if(a==0) cache[c][0] = 1;
                else if(c==0) cache[0][a] = 0;
                else {
                    int ca = coins[c-1];
                    if(ca <= a)
                        cache[c][a] = cache[c][a-ca] + cache[c-1][a];
                    else
                        cache[c][a] = cache[c-1][a];
                }
            }
        }
        return cache[coins.length][amount];
    }
}
```

## Performance
`O(coints*amount)`
