---
layout:     post
title:      "Problem: Rectangle Area"
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

Find the total area covered by two rectilinear rectangles in a 2D plane.

Each rectangle is defined by its bottom left corner and top right corner as shown in the figure.

![](/img/posts/dsa/rectangle_area.png)

Assume that the total area is never beyond the maximum possible value of int.

## Solution
TODO

#### Code
```java
public class Solution {
  public int computeArea(int A, int B, int C, int D, int E, int F, int G, int H) {

    int totalArea = (C - A) * (D - B) + (G - E) * (H - F);

    if(Math.min(C, G)<=Math.max(A, E)) 
      return totalArea;

    int width = Math.min(C, G) - Math.max(A, E);

    if(Math.min(D, H)<=Math.max(B,F)) 
      return totalArea;

    int hight = Math.min(D, H) - Math.max(B,F);

    return totalArea - width * hight;
  }
}
```

## Performance
TODO
