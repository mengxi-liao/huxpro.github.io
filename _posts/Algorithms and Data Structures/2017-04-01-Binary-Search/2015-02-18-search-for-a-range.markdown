---
layout:     post
title:      "Problem: Search For a Range"
date:       2015-02-18 00:00:00
author:     "Marcy"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - Coding Interview
    - Coding Practice
    - Algorithms and Data Structures
    - Binary Search
---

## Question

A peak element is an element that is greater than its neighbors.

Given an input array where `num[i] ≠ num[i+1]`, find a peak element and return its index.

The array may contain multiple peaks, in that case return the index to any one of the peaks is fine.

You may imagine that `num[-1] = num[n] = -∞`.

For example, in array `[1, 2, 3, 1]`, 3 is a peak element and your function should return the index number 2.

## Solution
TODO

#### Code
```java
class Solution {
    public int findPeakElement(int[] nums) {
        int l = 0;
        int r = nums.length-1;
        while(l<r) {
            int m = l+(r-l)/2;
            if(nums[m] < nums[m+1]) {
                l = m+1;
            }
            else {
                r = m;
            }
        }
        
        return l;
        
    }
}
```

## Performance
TODO