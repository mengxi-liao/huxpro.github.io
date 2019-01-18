---
layout:     post
title:      "Problem: Missing Ranges"
date:       2015-02-18 00:00:00
author:     "Marcy"
header-img: "img/post-bg-2015.jpg"
catalog: true
category: algnote
algnote-tags:
    - Coding Interview
    - Coding Practice
    - Algorithms and Data Structures
    - Array
    - Medium
---

## Question

Given a sorted integer array nums, where the range of elements are in the inclusive range [lower, upper], return its missing ranges.

**Example:**
```
Input: nums = [0, 1, 3, 50, 75], lower = 0 and upper = 99,
Output: ["2", "4->49", "51->74", "76->99"]
```
#### Code
```java
class Solution {
    public List<String> findMissingRanges(int[] nums, int lower, int upper) {
        List<String> results = new ArrayList<>();
        long pre = lower;
        for (int n : nums) {
            if(pre < n) results.add(range(pre, n-1));
            pre = (long)n+1;
        }
        if(pre < (long)upper+1) results.add(range(pre, (long)upper));
        return results;
    }

    private String range(long low, long high) {
        return low == high ? Long.toString(low) : low + "->" + high;
    }
}
```

## Performance
O(n)

## Notes

- user long!
- pre always points to the first num of the next range.
- the second num of the next range is next number in the array - 1
