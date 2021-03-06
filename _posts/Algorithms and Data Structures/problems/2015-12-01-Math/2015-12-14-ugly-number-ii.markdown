---
layout:     post
title:      "Problem: Ugly Number II"
date:       2015-02-18 00:00:00
author:     "Marcy"
header-img: "img/post-bg-2015.jpg"
catalog: true
category: algnote
algnote-tags:
    - Coding Interview
    - Coding Practice
    - Algorithms and Data Structures
    - Math
    - Medium
---

## Question

Write a program to find the `n`-th ugly number.

Ugly numbers are positive numbers whose prime factors only include `2, 3, 5`. For example, `1, 2, 3, 4, 5, 6, 8, 9, 10, 12` is the sequence of the first `10` ugly numbers.

Note that `1` is typically treated as an ugly number, and n **does not exceed 1690**.

## Solution
We have an array k of first n ugly number. We only know, at the beginning, the first one, which is `1`. Then
`k[1] = min( k[0]x2, k[0]x3, k[0]x5)`. The answer is `k[0]x2`. So we move 2's pointer to 1. Then we test:
`k[2] = min( k[1]x2, k[0]x3, k[0]x5)`. And so on.
Be careful about the cases such as `6`, in which we need to forward both pointers of 2 and 3.
#### Code
```java
public class Solution {
  public int nthUglyNumber(int n) {
    int [] uglyList = new int[n];

    uglyList[0] = 1;
    int index2 = 0;
    int index3 = 0;
    int index5 = 0;

    for(int i=1; i<uglyList.length; i++) {
      int nextUgly2 = uglyList[index2]*2;
      int nextUgly3 = uglyList[index3]*3;
      int nextUgly5 = uglyList[index5]*5;

      uglyList[i] = Math.min(Math.min(nextUgly2, nextUgly3), nextUgly5);

      if(uglyList[i] == nextUgly2)
        index2 ++;
      if(uglyList[i] == nextUgly3)
        index3 ++;
      if(uglyList[i] == nextUgly5)
        index5 ++;
    }

    return uglyList[n-1];
  }
}
```

## Performance
O(n)
