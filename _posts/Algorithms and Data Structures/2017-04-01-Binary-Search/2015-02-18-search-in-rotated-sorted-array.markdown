---
layout:     post
title:      "Problem: Find Minimum in Rotated Sorted Array"
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
---

## Question

Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand.

(i.e., `0 1 2 4 5 6 7` might become `4 5 6 7 0 1 2`).

Find the minimum element.

You may assume no duplicate exists in the array.

## Solution
TODO

#### Code
```java
class Solution {
    public int findMin(int[] nums) {
        int l = 0;
        int r = nums.length-1;
        while(l<r) {
            int m = l + (r-l)/2;
            if(nums[m] > nums[r]) {
                l = m+1;
            }
            else {
                r = m;
            }
        }
        
        return nums[l];
    }
}
```

## Performance
TODO