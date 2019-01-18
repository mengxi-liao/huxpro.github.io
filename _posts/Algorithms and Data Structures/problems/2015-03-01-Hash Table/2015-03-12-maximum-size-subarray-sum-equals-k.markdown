---
layout:     post
title:      "Problem: Maximum Size Subarray Sum Equals k"
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

Given an array nums and a target value k, find the maximum length of a subarray that sums to k. If there isn't one, return 0 instead.

Note:
The sum of the entire nums array is guaranteed to fit within the 32-bit signed integer range.

**Example 1:**

```
Input: nums = [1, -1, 5, -2, 3], k = 3
Output: 4
Explanation: The subarray [1, -1, 5, -2] sums to 3 and is the longest.
```

**Example 2:**

```
Input: nums = [-2, -1, 2, 1], k = 1
Output: 2
Explanation: The subarray [-1, 2] sums to 1 and is the longest.
```

**Follow Up:**

Can you do it in O(n) time?

## Solution
Use HashMap + prefix sum array.

#### Code
```java
class Solution {
    public int maxSubArrayLen(int[] nums, int k) {
        int[] prefixSum = new int[nums.length+1];
        prefixSum[0] = 0;
        for(int i=1; i<=nums.length; i++) {
            prefixSum[i] = prefixSum[i-1] + nums[i-1];
        }

        int max = 0;
        Map<Integer, Integer> map = new HashMap<>();
        for(int i=0; i<prefixSum.length; i++) {
            int target = prefixSum[i]-k;
            if(map.containsKey(target)) {
                max = Math.max(max, i-map.get(target));
            }
            if(!map.containsKey(prefixSum[i])) {
                map.put(prefixSum[i], i);
            }
        }

        return max;
    }
}
```

## Performance
O(n)
