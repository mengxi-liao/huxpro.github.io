---
layout:     post
title:      "Problem: Kth Largest Element in an Array"
date:       2015-02-18 00:00:00
author:     "Marcy"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - Coding Interview
    - Coding Practice
    - Algorithms and Data Structures
    - Heap
    - Medium
---

## Question

Find the kth largest element in an unsorted array. Note that it is the kth largest element in the sorted order, not the kth distinct element.
For example,
Given `[3,2,1,5,6,4]` and k = 2, return 5.

**Note:**
You may assume k is always valid, 1 ≤ k ≤ array's length.

## Solution
TODO

#### Code
```java
class Solution {
    public int findKthLargest(int[] nums, int k) {
        PriorityQueue<Integer> pq = new PriorityQueue();
        for(int num : nums) {
            pq.add(num);
            if(pq.size() > k) pq.poll();
        }
        
        return pq.peek();
    }
}
```

## Performance
TODO
