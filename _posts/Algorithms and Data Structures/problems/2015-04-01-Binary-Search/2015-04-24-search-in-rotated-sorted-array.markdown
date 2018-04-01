---
layout:     post
title:      "Problem: Search in Rotated Sorted Array"
date:       2015-02-18 00:00:00
author:     "Marcy"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
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
TODO

#### Code
```java
class Solution {
    public int search(int[] nums, int target) {
        int l=0;
        int r=nums.length-1;
        while(l<=r) {
            int m = l + (r-l)/2;
            if(target == nums[m]) return m;
            
            if(nums[m] > nums[r]){
                // m is on the left side
                if(target > nums[m] || target < nums[l]) {
                    l = m+1;
                }
                else {
                    r = m-1;
                }
            } else {
                // m is on the right side
                if(target > nums[m] && target <= nums[r]) {
                    l = m+1;
                }
                else {
                    r = m-1;
                }
            }
        }
        
        return -1;
    }
}
```

## Performance
TODO
