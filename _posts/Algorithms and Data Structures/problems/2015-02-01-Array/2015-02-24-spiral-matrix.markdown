---
layout:     post
title:      "Problem: Spiral Matrix"
date:       2015-02-18 00:00:00
author:     "Marcy"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - Coding Interview
    - Coding Practice
    - Algorithms and Data Structures
    - Array
    - Medium
---

## Question

Given a matrix of `m x n` elements (m rows, n columns), return all elements of the matrix in spiral order.

For example,
Given the following matrix:

```
[
 [ 1, 2, 3 ],
 [ 4, 5, 6 ],
 [ 7, 8, 9 ]
]
```
You should return `[1,2,3,6,9,8,7,4,5]`.

## Solution

The idea is to traverse the matrix from outside to inside, use four indices, `top`, `bottom`, `right`, `left`, to point at the side boundaries of the "area" we do not travel yet. Initially, the four indices are pointing to the boundaries of the matrix. Each time we complete traveling a side, we move the corresponding index towards the center of the matrix, so the next time we will travel the inner boundary of that side.

Starting from `matrix[0][0]`. First traverse right and increment `top`, then traverse down and decrement `right`, then traverse left and decrement `bottom`, and finally traverse up and increment `left`.

The only tricky part is that when traversing left or up, we need to check whether the row or col still exists to prevent duplicates.

#### Code

Here is a sample solution.

```java
class Solution {
    public List<Integer> spiralOrder(int[][] matrix) {
        List<Integer> results = new ArrayList();
        if(matrix.length==0 || matrix[0].length==0) return results;

        int top = 0, bottom = matrix.length-1, left=0, right = matrix[0].length-1;

        while(true) {
            for(int i=left; i<=right; i++) {
                results.add(matrix[top][i]);
            }
            top++;

            for(int i=top; i<=bottom; i++) {
                results.add(matrix[i][right]);
            }
            right--;

            if(top>bottom) break;
            // make sure we did not travel
            // the next row to prevent duplicates
            for(int i=right; i>=left; i--) {
                results.add(matrix[bottom][i]);
            }
            bottom--;

            if(right<left) break;
            // make sure we did not travel
            // the next col to prevent duplicates
            for(int i=bottom; i>=top; i--) {
                results.add(matrix[i][left]);
            }
            left++;
        }

        return results;
    }
}
```

## Performance

Each element in the matrix is visited once, so the time complexity is `O(m x n)`. Except for the necessary array for the result, only constant extra space is used.
