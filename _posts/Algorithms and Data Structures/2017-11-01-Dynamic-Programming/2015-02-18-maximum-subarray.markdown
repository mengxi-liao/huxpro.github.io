---
layout:     post
title:      "Problem: Maximum Subarray"
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
---

## Question

Find the contiguous subarray within an array (containing at least one number) which has the largest sum.

For example, given the array `[-2,1,-3,4,-1,2,1,-5,4]`,
the contiguous subarray `[4,-1,2,1]` has the largest sum = `6`.

## Solution
TODO

#### Code
```java
class Solution {
    public int maxSubArray(int[] nums) {
        int prevMax = Integer.MIN_VALUE;
        int max = Integer.MIN_VALUE;
        for(int i=0; i<nums.length; i++) {
            int currentMax = nums[i];
            if(prevMax > 0) currentMax += prevMax;
            max = Math.max(currentMax, max);
            prevMax = currentMax;
        }

        return max;
    }
}
```

## Performance
TODO