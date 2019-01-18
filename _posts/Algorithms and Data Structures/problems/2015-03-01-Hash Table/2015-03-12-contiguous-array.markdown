---
layout:     post
title:      "Problem: Contiguous Array"
date:       2015-02-18 00:00:00
author:     "Marcy"
header-img: "img/post-bg-2015.jpg"
catalog: true
category: algnote
algnote-tags:
    - Coding Interview
    - Coding Practice
    - Algorithms and Data Structures
    - Hash Table
    - Medium
    - Array
---

## Question

Given a binary array, find the maximum length of a contiguous subarray with equal number of 0 and 1.

**Example 1:**
```
Input: [0,1]
Output: 2
Explanation: [0, 1] is the longest contiguous subarray with equal number of 0 and 1.
```
**Example 2:**
```
Input: [0,1,0]
Output: 2
Explanation: [0, 1] (or [1, 0]) is a longest contiguous subarray with equal number of 0 and 1.
```

## Solution
Use HashMap + prefix sum array.

#### Code
```java
class Solution {
    public int findMaxLength(int[] nums) {
        int[] counts = new int[nums.length+1];
        for(int i = 1; i <= nums.length; i++) {
            int delta = nums[i-1] == 0 ? 1:-1;
            counts[i] = counts[i-1] + delta;
        }

        int longest = 0;
        Map<Integer, Integer> map = new HashMap<>();
        for(int i=0; i<counts.length; i++) {
            if(map.containsKey(counts[i])) {
                longest = Math.max(longest, i-map.get(counts[i]));
            }
            else {
                map.put(counts[i], i);
            }
        }

        return longest;
    }
}
```

## Performance
O(n)
