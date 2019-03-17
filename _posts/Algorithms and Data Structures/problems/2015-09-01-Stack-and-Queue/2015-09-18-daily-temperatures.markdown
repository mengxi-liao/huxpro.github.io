---
layout:     post
title:      "Problem: Daily Temperatures"
date:       2015-02-18 00:00:00
author:     "Marcy"
header-img: "img/post-bg-2015.jpg"
catalog: true
category: algnote
algnote-tags:
    - Coding Interview
    - Coding Practice
    - Algorithms and Data Structures
    - Stack
    - Medium
---

## Question

Given a list of daily temperatures T, return a list such that, for each day in the input, tells you how many days you would have to wait until a warmer temperature. If there is no future day for which this is possible, put 0 instead.

For example, given the list of temperatures T = [73, 74, 75, 71, 69, 72, 76, 73], your output should be [1, 1, 4, 2, 1, 1, 0, 0].

## Solution
TODO

#### Code
```java
class Solution {
    public int[] dailyTemperatures(int[] T) {
        int[] results = new int[T.length];
        Stack<Integer> s = new Stack<>();
        for(int i=0; i<T.length; i++) {
            while(!s.isEmpty() && T[s.peek()] < T[i]) {
                int j = s.pop();
                results[j] = i-j;
            }
            s.push(i);
        }
        return results;
    }
}
```

## Performance
O(n)
