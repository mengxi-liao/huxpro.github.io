---
layout:     post
title:      "Problem: Move Zeroes"
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
    - Easy
---

## Question

Given an array nums, write a function to move all 0's to the end of it while maintaining the relative order of the non-zero elements.

For example, given `nums = [0, 1, 0, 3, 12]`, after calling your function, nums should be `[1, 3, 12, 0, 0]`.

**Note:**
1. You must do this in-place without making a copy of the array.
2. Minimize the total number of operations.


## Solution

A solution could be using an index `i` to traverse the array, and for each iteration, if `nums[i]` is not zero, add the element to the end of result array. Mark the end of the result array as `tail`. As `tail` is always smaller than `i`, the original array could be used as the result array so the algorithm could be done in-place.

#### Code

Here is a sample solution.

```java
class Solution {
    public void moveZeroes(int[] nums) {
        int tail = 0;
        for(int i=0; i<nums.length; i++) 
            if(nums[i] != 0) 
                nums[tail++] = nums[i];
        while(tail<nums.length) 
            nums[tail++] = 0;
    }
}
```

## Performance

Each element in the original array is visited and might be copied at most once. The overall performance is O(n). As this is done in-place, no extra memory space is used.
