---
layout:     post
title:      "Problem: Number of Boomerangs"
date:       2015-02-18 00:00:00
author:     "Marcy"
header-img: "img/post-bg-2015.jpg"
catalog: true
category: algnote
algnote-tags:
    - Coding Interview
    - Coding Practice
    - Algorithms and Data Structures
    - Hash Table
    - Medium
    - Array
---

## Question

Given n points in the plane that are all pairwise distinct, a "boomerang" is a tuple of points `(i, j, k)` such that the distance between i and j equals the distance between i and k (the order of the tuple matters).

Find the number of boomerangs. You may assume that n will be at most 500 and coordinates of points are all in the range [-10000, 10000] (inclusive).

**Example:**
```
Input:
[[0,0],[1,0],[2,0]]

Output:
2

Explanation:
The two boomerangs are [[1,0],[0,0],[2,0]] and [[1,0],[2,0],[0,0]]
```

## Solution
Use HashMap to keep track of points with same distance to a point.

#### Code
```java
class Solution {
    public int numberOfBoomerangs(int[][] points) {
        int res = 0;
        Map<Integer, Integer> map = new HashMap<>();
        for(int i=0; i<points.length; i++) {
            for(int j=0; j<points.length; j++) {
                if(i==j) continue;
                int d = distance(points[i], points[j]);
                map.put(d, map.getOrDefault(d, 0)+1);
            }
            for(int val: map.values()) {
                res +=  val*(val-1);
            }
            map.clear();
        }
        return res;
    }

    public int distance(int[] p1, int[] p2) {
        int d1 = p1[0]-p2[0];
        int d2 = p1[1]-p2[1];
        return d1*d1 + d2*d2;
    }
}
```

## Performance
O(n)
