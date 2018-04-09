---
layout:     post
title:      "Problem: Largest Rectangle in Histogram"
date:       2015-02-18 00:00:00
author:     "Marcy"
header-img: "img/post-bg-2015.jpg"
catalog: true
category: algnote
algnote-tags:
    - Coding Interview
    - Coding Practice
    - Algorithms and Data Structures
    - Stack
    - Hard
---

## Question

Given n non-negative integers representing the histogram's bar height where the width of each bar is 1, find the area of largest rectangle in the histogram.

![](/img/posts/dsa/histogram.png)

Above is a histogram where width of each bar is 1, given height = `[2,1,5,6,2,3]`.

![](/img/posts/dsa/histogram_area.png)

The largest rectangle is shown in the shaded area, which has area = `10` unit.

For example,
Given heights = `[2,1,5,6,2,3]`,
return `10`.

## Solution
TODO

#### Code
```java
class Solution {
    int maxSize = 0;
    
    public int largestRectangleArea(int[] heights) {
        Stack<Integer> stack = new Stack();
        int maxArea = 0;
        for(int i=0; i<heights.length+1; i++) {
            int height = 0;
            if(i<heights.length) height = heights[i];
            while(!stack.empty() && heights[stack.peek()] > height) {
                int last = stack.pop();
                int width = stack.empty()? i:(i - stack.peek() - 1);
                int area = heights[last] * width;
                maxArea = Math.max(maxArea, area);
            }
            stack.push(i);
        }
        
        return maxArea;
    }
    
}
```

## Performance
TODO
