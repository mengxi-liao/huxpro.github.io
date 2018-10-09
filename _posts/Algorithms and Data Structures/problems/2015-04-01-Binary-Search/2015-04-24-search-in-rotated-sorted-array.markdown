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

When `m` and `target` are both greater than `nums[l]`, they are both at the left side. User regular binary search rule to reset `l` or `r`.

When `m` and `target` are both less than `nums[l]`, they are both at the right side. User regular binary search rule to reset `l` or `r`.

When `m` is larger than `nums[l]` and `target` is less than `nums[l]`, `target` is at the right side and `m` is at the left side. Set `l` as `m+1`.
When `m` is less than `nums[l]` and `target` is greater than `nums[l]`, `target` is at the left side and `m` is at the right side. Set `r` as `m-1`.

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
                // m is at the left side
                if(target > nums[m] || target < nums[l]) {
                    l = m+1;
                }
                else {
                    r = m-1;
                }
            } else {
                // m is at the right side
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

`O(n)` time complexity.
