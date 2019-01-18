---
layout:     post
title:      "Problem: Climbing Stairs"
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

You are climbing a stair case. It takes n steps to reach to the top.

Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?

Note: Given n will be a positive integer.

**Example 1:**
```
Input: 2
Output: 2
Explanation: There are two ways to climb to the top.
1. 1 step + 1 step
2. 2 steps
```
**Example 2:**
```
Input: 3
Output: 3
Explanation: There are three ways to climb to the top.
1. 1 step + 1 step + 1 step
2. 1 step + 2 steps
3. 2 steps + 1 step
```
## Solution
TODO

#### Code
```java
class Solution {
    public int climbStairs(int n) {
        if(n==1) return 1;

        int first = 1;
        int second = 2;

        for(int i=2; i<n; i++) {
            int third = first + second;
            first = second;
            second = third;
        }

        return second;
    }
}
```

## Performance
TODO
