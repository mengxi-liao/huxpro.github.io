---
layout:     post
title:      "Problem: Rectangle Overlap"
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
    - Easy
---

## Question

A rectangle is represented as a list [x1, y1, x2, y2], where (x1, y1) are the coordinates of its bottom-left corner, and (x2, y2) are the coordinates of its top-right corner.

Two rectangles overlap if the area of their intersection is positive.  To be clear, two rectangles that only touch at the corner or edges do not overlap.

Given two (axis-aligned) rectangles, return whether they overlap.

**Example 1:**
```
Input: rec1 = [0,0,2,2], rec2 = [1,1,3,3]
Output: true
```

**Example 2:**
```
Input: rec1 = [0,0,1,1], rec2 = [1,0,2,1]
Output: false
```

#### Code
```java
class Solution {
    public boolean isRectangleOverlap(int[] rec1, int[] rec2) {
        if(rec1[0] >= rec2[2] || rec2[0] >= rec1[2]) return false;
        if(rec1[1] >= rec2[3] || rec2[1] >= rec1[3]) return false;
        return true;
    }
}
```

## Performance
O(1)
