---
layout:     post
title:      "Problem: Maximum Length of Repeated Subarray"
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

Given two integer arrays A and B, return the maximum length of an subarray that appears in both arrays.

**Example 1:**
```
Input:
A: [1,2,3,2,1]
B: [3,2,1,4,7]
Output: 3
```

**Explanation:**

The repeated subarray with maximum length is `[3, 2, 1]`.

**Note:**
- 1 <= len(A), len(B) <= 1000
- 0 <= A[i], B[i] < 100

## Solution
Use dynamic programming. Let's construct a matrix `M[i][j]` to represent the length of the longest common subarray that ends with `A[i]` and `B[j]`. When `A[i] != B[j]`, `M[i][j]` is `0`. When `A[i] == B[j]`, `M[i][j] = M[i-1][j-1]+1`. The result will be the largest element in `M[i][j]`.

#### Code
```java
class Solution {
    public int findLength(int[] A, int[] B) {
        int[][] M = new int[A.length+1][B.length+1];
        int max = 0;
        for(int i=1; i<=A.length; i++) {
            for(int j=1; j<=B.length; j++) {
                if(A[i-1] == B[j-1]) {
                    M[i][j] = M[i-1][j-1]+1;
                    max = Math.max(max,M[i][j]);
                }
            }
        }
        
        return max;
    }
}
```

## Performance
`O(A.length * B.length)`
