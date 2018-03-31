---
layout:     post
title:      "Problem: Merge Sorted Array"
date:       2015-02-18 00:00:00
author:     "Marcy"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - Coding Interview
    - Coding Practice
    - Algorithms and Data Structures
    - Array
    - Easy
---

## Question

Given two sorted integer arrays `nums1` and `nums2`, merge `nums2` into `nums1` as one sorted array.

**Note:**

You may assume that `nums1` has enough space (size that is greater or equal to `m+n`) to hold additional elements from `nums2`. The number of elements initialized in `nums1` and `nums2` is `m` and `n` respectively.

## Solution

Merge the two arrays from the ends of both arrays. Use  3 pointers to mark the end, `i`, of the result array and the ends, `m` and `n`, of the two arrays. Initially, `i = m+n-1`. Each time pick the larger element from `nums1[m]` and `nums2[n]` and place the selected one at `nums1[i]`. Move the index of the selected array forward.

#### Code

Here is a sample solution.

```java
class Solution {
    public void merge(int[] nums1, int m, int[] nums2, int n) {
        int i=m+n-1;
        m--;
        n--;
        while(i>=0) {
            if(m<0)
                nums1[i--] = nums2[n--];
            else if(n<0)
                nums1[i--] = nums1[m--];
            else if(nums1[m]>nums2[n])
                nums1[i--] = nums1[m--];
            else
                nums1[i--] = nums2[n--];
        }
    }
}
```

## Performance

As each element in the array is visited once, the overall time complexity is O(n). And as it modifies the array in place, only constant extra space is used.
