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
    - Sorting
---

## Question

Given two sorted integer arrays nums1 and nums2, merge nums2 into nums1 as one sorted array.

**Note:**
You may assume that nums1 has enough space (size that is greater or equal to m + n) to hold additional elements from nums2. The number of elements initialized in nums1 and nums2 are m and n respectively.

## Solution
TODO

#### Code
```java
class Solution {
    public void merge(int[] nums1, int m, int[] nums2, int n) {
        int sIndex = m + n - 1;
        int mIndex = m-1;
        int nIndex = n-1;

        for(int i=sIndex; i>=0; i--) {
            if(mIndex < 0) nums1[sIndex--] = nums2[nIndex--]; 
            else if(nIndex < 0) nums1[sIndex--] = nums1[mIndex--]; 
            else if(nums1[mIndex] > nums2[nIndex]) nums1[sIndex--] = nums1[mIndex--]; 
            else nums1[sIndex--] = nums2[nIndex--];  
        }
    }
}
```

## Performance
TODO