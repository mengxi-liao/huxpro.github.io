---
layout:     post
title:      "Problem: Kth Smallest Element in a Sorted Matrix"
date:       2015-02-18 00:00:00
author:     "Marcy"
header-img: "img/post-bg-2015.jpg"
catalog: true
category: algnote
algnote-tags:
    - Coding Interview
    - Coding Practice
    - Algorithms and Data Structures
    - Heap
    - Medium
---

## Question

Given a n x n matrix where each of the rows and columns are sorted in ascending order, find the kth smallest element in the matrix.

Note that it is the kth smallest element in the sorted order, not the kth distinct element.

**Example:**
```
matrix = [
   [ 1,  5,  9],
   [10, 11, 13],
   [12, 13, 15]
],
k = 8,

return 13.
```

## Solution
Todo

#### Code
```java
class Solution {
    public int kthSmallest(int[][] matrix, int k) {
        if(matrix.length == 0 || matrix[0].length == 0) return 0;
        PriorityQueue<int[]> pq = new PriorityQueue<>(
            (a,b)->matrix[a[0]][a[1]] - matrix[b[0]][b[1]]
        );
        for(int i=0; i<matrix.length; i++) {
            pq.add(new int[]{i, 0});
        }
        int[] idx = null;
        while(!pq.isEmpty() && k != 0) {
            idx = pq.poll();
            if(idx[1] < matrix[0].length-1) pq.offer(new int[]{idx[0], idx[1]+1});
            k--;
        }
        return matrix[idx[0]][idx[1]];
    }
}
```

## Performance
`O(nlogk)`
