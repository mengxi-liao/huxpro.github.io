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
    - Hard
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
    Integer[] cache = new Integer[amount+1];
    cache[0] = 0;

    for(int i=1; i<=amount; i++) {
      for(int c:  coins) {
        if(i-c >= 0 && cache[i-c] != null) {
          if(cache[i]==null)
            cache[i] = cache[i-c]+1;
          else
            cache[i] = Math.min(cache[i], cache[i-c]+1);
        }
      }
    }

    return cache[amount] == null? -1 : cache[amount];
  }
}
```

## Performance
`O(coints*amount)`
