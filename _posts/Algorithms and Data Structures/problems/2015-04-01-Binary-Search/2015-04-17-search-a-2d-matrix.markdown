---
layout:     post
title:      "Problem: Search a 2D Matrix"
date:       2015-02-18 00:00:00
author:     "Marcy"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - Coding Interview
    - Coding Practice
    - Algorithms and Data Structures
    - Binary Search
    - Medium
---

## Question

Write an efficient algorithm that searches for a value in an m x n matrix. This matrix has the following properties:

- Integers in each row are sorted from left to right.
- The first integer of each row is greater than the last integer of the previous row.

**For example,**

Consider the following matrix:

```
[
  [1,   3,  5,  7],
  [10, 11, 16, 20],
  [23, 30, 34, 50]
]
```
Given `target = 3`, return `true`.


## Solution
TODO

#### Code
```java
public class Solution {

  public boolean searchMatrix(int[][] matrix, int target) {

    int rows = matrix.length;
    int cols = matrix[0].length;

    int begin = 0;
    int end = rows * cols - 1;

    while(begin <= end) {
      int mid = (begin + end) / 2;
      int mid_value = matrix[mid/cols][mid%cols];

      if( mid_value == target)
        return true;
      else if(mid_value < target)
        begin = mid+1;
      else
        end = mid-1;
    }

    return false;
  }
}
```

## Performance
TODO
