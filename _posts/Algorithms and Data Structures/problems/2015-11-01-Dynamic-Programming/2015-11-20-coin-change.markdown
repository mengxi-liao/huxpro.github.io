---
layout:     post
title:      "Problem: Coin Change"
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

You are given coins of different denominations and a total amount of money amount. Write a function to compute the fewest number of coins that you need to make up that amount. If that amount of money cannot be made up by any combination of the coins, return -1.

**Example 1:**

```
Input: coins = [1, 2, 5], amount = 11
Output: 3
Explanation: 11 = 5 + 5 + 1
```

**Example 2:**

```
Input: coins = [2], amount = 3
Output: -1
Note:
You may assume that you have an infinite number of each kind of coin.
```

## Solution I
Use level order breath first search.

#### Code
```java
class Solution {
  public int coinChange(int[] coins, int amount) {
    if(amount == 0) return 0;

    Map<Integer, Integer> prevLevel = new HashMap<>();
    prevLevel.put(0,0);
    while(!prevLevel.isEmpty()) {
      if(prevLevel.containsKey(amount)) return prevLevel.get(amount);
      Set<Integer> keys = prevLevel.keySet();
      Map<Integer, Integer> newLevel = new HashMap<>();
      for(Integer k: keys) {
        for(int i=0; i<coins.length; i++) {
          int c = coins[i];
          if(k+c > amount) continue;
          if(!newLevel.containsKey(k+c)) {
            newLevel.put(k+c, prevLevel.get(k) + 1);
          }
          else {
            int oldCount = newLevel.get(k+c);
            int newCount = prevLevel.get(k)+1;
            if(newCount < oldCount)
              newLevel.put(k+c, newCount);
          }
        }
      }
      prevLevel = newLevel;
  }

    return -1;
  }
}
```

## Performance
Worst case `O(coints*amount)`. But it won't reach some unreachable amount.

## Solution II
Use dynamic programming

#### Code
```java
class Solution {
    public int coinChange(int[] coins, int amount) {
        int[] cache = new int[amount+1];
        Arrays.fill(cache, -1);
        cache[0] = 0;
        for(int v=1; v<=amount; v++) {
            for(int c: coins) {
                if(v == c) cache[v] = 1;
                if(v - c > 0 && cache[v-c] != -1) {
                    if(cache[v] == -1) cache[v] = cache[v-c] + 1;
                    else cache[v] = Math.min(cache[v-c] + 1, cache[v]);
                }
            }
        }

        if(cache[amount] != -1) return cache[amount];
        return -1;
    }
}

/*
when v=0, cache[0] = 0;
for each ci and existing cache[v-ci]:
    cache[v] = min(cache[v-c1] + 1, cache[v-c2] + 1, ..., cache[v-cn]+1)
*/
```

## Performance
`O(coints*amount)`
