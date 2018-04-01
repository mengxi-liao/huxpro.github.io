---
layout:     post
title:      "Problem: Trapping Rain Water"
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
    - Hard
---

## Question

Given n non-negative integers representing an elevation map where the width of each bar is 1, compute how much water it is able to trap after raining.

For example,

Given `[0,1,0,2,1,0,1,3,2,1,2,1]`, return `6`.

![](/img/posts/dsa/rainwatertrap.png)

The above elevation map is represented by array [0,1,0,2,1,0,1,3,2,1,2,1]. In this case, 6 units of rain water (blue section) are being trapped. Thanks Marcos for contributing this image!

## Solution
TODO

#### Code
```java
class Solution {
    public int trap(int[] height) {
        if(height.length < 3) return 0;

        int left = 0;
        int right = height.length-1;
        int leftMax = height[left];
        int rightMax = height[right];

        int water = 0;

        while(left < right-1) {
            if(leftMax < rightMax) {
                left++;
                if(height[left] > leftMax) 
                    leftMax = height[left];
                else
                    water += leftMax - height[left];
            }
            else {
                right --;
                if(height[right] >= rightMax) 
                    rightMax = height[right];
                else
                    water += rightMax - height[right];
            }
        }

        return water;
    }
}
```

## Performance
TODO
