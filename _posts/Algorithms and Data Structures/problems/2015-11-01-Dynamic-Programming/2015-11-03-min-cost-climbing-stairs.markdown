---
layout:     post
title:      "Problem: Min Cost Climbing Stairs"
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
    - Easy
---

## Question

On a staircase, the i-th step has some non-negative cost cost[i] assigned (0 indexed).

Once you pay the cost, you can either climb one or two steps. You need to find minimum cost to reach the top of the floor, and you can either start from the step with index 0, or the step with index 1.

**Example 1:**
```
Input: cost = [10, 15, 20]
Output: 15
Explanation: Cheapest is start on cost[1], pay that cost and go to the top.
```

**Example 2:**
```
Input: cost = [1, 100, 1, 1, 1, 100, 1, 1, 100, 1]
Output: 6
Explanation: Cheapest is start on cost[0], and only step on 1s, skipping cost[3].
```

**Note:**
- cost will have a length in the range [2, 1000].
- Every `cost[i]` will be an integer in the range [0, 999].

## Solution
TODO

#### Code
```java
class Solution {
    public int minCostClimbingStairs(int[] cost) {
        int[] cache = new int[cost.length];
        cache[0] = cost[0];
        cache[1] = cost[1];
        for(int i=2; i<cost.length; i++) {
            cache[i] = Math.min(cache[i-2], cache[i-1]) + cost[i];
        }
        return Math.min(cache[cost.length-1], cache[cost.length-2]);
    }
}
```

## Performance
O(n)
