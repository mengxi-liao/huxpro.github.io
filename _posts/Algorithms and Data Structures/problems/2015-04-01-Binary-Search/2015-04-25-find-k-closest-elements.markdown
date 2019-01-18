---
layout:     post
title:      "Problem: Find K Closest Elements"
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

Given a sorted array, two integers k and x, find the k closest elements to x in the array. The result should also be sorted in ascending order. If there is a tie, the smaller elements are always preferred.

**Example 1:**
```
Input: [1,2,3,4,5], k=4, x=3
Output: [1,2,3,4]
```
**Example 2:**
```
Input: [1,2,3,4,5], k=4, x=-1
Output: [1,2,3,4]
```
**Note:**
- The value k is positive and will always be smaller than the length of the sorted array.
- Length of the given array is positive and will not exceed 104
- Absolute value of elements in the array and x will not exceed 104

## Solution

Assume we are taking `A[i] ~ A[i + k -1]`.
We can binary research `i`
We compare the distance between `x - A[mid]` and `A[mid + k] - x`

If `x - A[mid] > A[mid + k] - x`,
it means `A[mid + 1] ~ A[mid + k]` is better than `A[mid] ~ A[mid + k - 1]`,
and we have mid smaller than the right `i`.
So assign `left = mid + 1`.

Reversely, it's similar.

#### Code
```java
class Solution {
    public List<Integer> findClosestElements(int[] arr, int k, int x) {
        int l=0;
        int r=arr.length-k;

        while(l<r) {
            int m = l+(r-l)/2;
            if(x-arr[m] > arr[m+k]-x) l = m+1;
            else r = m;
        }

        List<Integer> list = new ArrayList<>();
        for(int i=l; i<l+k && i<arr.length; i++) list.add(arr[i]);

        return list;
    }
}
```

## Performance

`O(log(N - K))`
It's funny that when K increases,
the time complexity decrease instead.
