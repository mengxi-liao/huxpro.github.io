---
layout:     post
title:      "Problem: Rotate Image"
date:       2015-02-18 00:00:00
author:     "Marcy"
header-img: "img/post-bg-2015.jpg"
catalog: true
category: algnote
algnote-tags:
    - Coding Interview
    - Coding Practice
    - Algorithms and Data Structures
    - Array
---

## Question

You are given an n x n 2D matrix representing an image.

Rotate the image by 90 degrees (clockwise).

**Note:**
You have to rotate the image in-place, which means you have to modify the input 2D matrix directly. DO NOT allocate another 2D matrix and do the rotation.

**Example 1:**

```
Given input matrix = 
[
  [1,2,3],
  [4,5,6],
  [7,8,9]
],

rotate the input matrix in-place such that it becomes:
[
  [7,4,1],
  [8,5,2],
  [9,6,3]
]
```

**Example 2:**

```
Given input matrix =
[
  [ 5, 1, 9,11],
  [ 2, 4, 8,10],
  [13, 3, 6, 7],
  [15,14,12,16]
],

rotate the input matrix in-place such that it becomes:
[
  [15,13, 2, 5],
  [14, 3, 4, 1],
  [12, 6, 8, 9],
  [16, 7,10,11]
]
```

## Solution 1

There are two major solutions to the problem. The most obvious idea is to rotate the image from outside to inside.

#### Code

Here is a sample solution.

```java
class Solution {
    public void rotate(int[][] matrix) {
        int s = 0;
        int e = matrix.length-1;

        while(s<e) {
            int len = e-s;
            for(int i = 0; i<len; i++) {
                int tmp = matrix[s][s+i];
                matrix[s][s+i] = matrix[e-i][s];
                matrix[e-i][s] = matrix[e][e-i];
                matrix[e][e-i] = matrix[s+i][e];
                matrix[s+i][e] = tmp;
            }
            s++;
            e--;
        }
    }
}
```

## Solution 2

Another solution is to firstly transpose the image and then flip it symmetrically. For instance:

```
First reverse up to down, then swap the symmetry
 1 2 3     1 4 7     7 4 1
 4 5 6  => 2 5 8  => 8 5 2
 7 8 9     3 6 9     9 6 3
```

#### Code

Here is a sample solution.

```java
public class Solution {
    public void rotate(int[][] matrix) {
        for(int i = 0; i<matrix.length; i++){
            for(int j = i; j<matrix[0].length; j++){
                int temp = matrix[i][j];
                matrix[i][j] = matrix[j][i];
                matrix[j][i] = temp;
            }
        }
        for(int i =0 ; i<matrix.length; i++){
            for(int j = 0; j<matrix.length/2; j++){
                int temp = matrix[i][j];
                matrix[i][j] = matrix[i][matrix.length-1-j];
                matrix[i][matrix.length-1-j] = temp;
            }
        }
    }
}
```

## Performance

Both solutions are O(n x n) time complexity and use constant extra space.
