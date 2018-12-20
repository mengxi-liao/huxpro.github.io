---
layout:     post
title:      "Problem: Search in Rotated Sorted Array"
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

Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand.

(i.e., `0 1 2 4 5 6 7` might become `4 5 6 7 0 1 2`).

You are given a target value to search. If found in the array return its index, otherwise return -1.

You may assume no duplicate exists in the array.

## Solution

Use binary search.

When `m` and `target` are on the same side, use binary search rule.
When `m` and `target` are on the different side. Select the side where the `target` belongs.

#### Code
```java
class Solution {
    public int search(int[] nums, int target) {
        int l=0;
        int r=nums.length-1;
        while(l<=r) {
            int m = l + (r-l) / 2;
            if(nums[m] == target) return m;
            if(target < nums[l]) {
                // target is on the right side
                if(nums[m] >= nums[l]) {
                    // m is on the left side
                    l = m+1;
                }
                else {
                    // m is also on the right side
                    if(nums[m] > target) {
                        r = m - 1;
                    }
                    else {
                        l = m + 1;
                    }
                }
            }
            else {
                // target is on the left side
                if(nums[m] >= nums[l]) {
                    // m is also on the left side
                    if(nums[m] > target) {
                        r = m - 1;
                    }
                    else {
                        l = m + 1;
                    }
                }
                else {
                    r = m - 1;
                }
            }
        }
        return -1;
    }
}
```

## Performance

`O(n)` time complexity.
