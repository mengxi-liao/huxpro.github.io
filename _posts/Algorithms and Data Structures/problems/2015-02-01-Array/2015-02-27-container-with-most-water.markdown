---
layout:     post
title:      "Problem: Container With Most Water"
date:       2015-02-18 00:00:00
author:     "Marcy"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - Coding Interview
    - Coding Practice
    - Algorithms and Data Structures
    - Array
    - Two Pointers
    - Medium
---

## Question

Given n non-negative integers a1, a2, ..., an, where each represents a point at coordinate (i, ai). n vertical lines are drawn such that the two endpoints of line i is at (i, ai) and (i, 0). Find two lines, which together with x-axis forms a container, such that the container contains the most water.

Note: You may not slant the container and n is at least 2. units of rain water (blue section) are being trapped. Thanks Marcos for contributing this image!

## Solution
TODO

#### Code
```java
class Solution {
    public int maxArea(int[] height) {
        int l = 0, r = height.length-1;
        int max = 0;
        while(l<r) {
            int w = r-l;
            int h = Math.min(height[r],height[l]);
            max = Math.max(max, h*w);
            if(height[l]<height[r]) l++;
            else r--;
        }

        return max;
    }
}
```

## Performance
TODO
