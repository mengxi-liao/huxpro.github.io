---
layout:     post
title:      "Problem: Find First and Last Position of Element in Sorted Array"
date:       2015-02-18 00:00:00
author:     "Marcy"
header-img: "img/post-bg-2015.jpg"
catalog: true
category: algnote
algnote-tags:
    - Coding Interview
    - Coding Practice
    - Algorithms and Data Structures
    - Binary Search
    - Medium
---

## Question

Given an array of integers sorted in ascending order, find the starting and ending position of a given target value.

Your algorithm's runtime complexity must be in the order of O(log n).

If the target is not found in the array, return `[-1, -1]`.

For example,
Given `[5, 7, 7, 8, 8, 10]` and target value 8,
return `[3, 4]`.

## Solution
TODO

#### Code
```java
class Solution {
    public int[] searchRange(int[] nums, int target) {
        int idx = findFirstEqualOrGreater(nums, target);
        if(idx == nums.length || nums[idx] != target) return new int[] {-1, -1};
        int idx2 = findFirstEqualOrGreater(nums, target+1) - 1;
        return new int[] {idx, idx2};
    }

    private int findFirstEqualOrGreater(int[] nums, int target) {
        int l = 0;
        int r = nums.length-1;
        while(l<=r) {
            int m = (l + r) / 2;
            if(nums[m] < target) {
                l = m+1;
            }
            else {
                r = m-1;
            }
        }
        return l;
    }
}
```

## Performance
TODO
